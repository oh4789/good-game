# 개발2 DV2-P02 — v0.14 입력 중단·취소 검수

- 작성일: 2026-10-04 UTC
- 상태: DONE(검수·격리 차단안·인계물). 게임 결함 수정/통합/실기기 인수는 미완료.
- 승인 범위: DV2-P01 다음1순위인 누름→회전→release, 포커스 상실, 모달 닫기/잔여 입력 검수. 새 기능 추가 아님.
- 기준: 최신 WORK_START_HERE, CURRENT_IMPLEMENTATION, 개발2 지시서, 협업 규약, 1차 완성 인수표, v0.13 인계 및 Android v0.14 인계.
- 현재 Web v0.13과 Android v0.14는 별도다. 이번 실제 사용 소스는 Android v0.14.
- 소스 커밋/ZIP comment: 8e675d9c1e0a23f144e6e9128378f27e3eb1f7f5.
- 입력: Nightroad-v0.14-SOURCE.zip / 9,462,102bytes.
- SHA256: 0945635b7f7e9922ebd2ecfe495af1e3c510df63789db953d4d587b2be1f2e9b. 직접 대조 일치.
- 브랜치: work/dev2-v14-input-interruption-20261004.
- 선행: [DV2-P01](https://github.com/oh4789/good-game/commit/f1088b2f938ee251ee7210e0e234e6a476b71ed3). 기존 회전 완료 후 검사를 재실행하는 대신 누른 상태의 중단을 추가했다.

## 변경·전달물

사본 workbench/dev2/DV2-01/DV2-P02/ 안에만 작성.
- DV2Interrupt.gd: 실제 화면/모델 API·실제 창 입력 경로에 연결한64개 시나리오.
- DV2InputProbe.gd: 입력/GUI trace 수집과 선택적 harness-only 취소 차단 프로토타입.
- baseline-results.json, guard-results.json, 엔진 로그, source-integrity.json.
- proposal-canceled-pointer.patch: scripts/SquareScreen.gd에 대한 **미적용 제안**.
- prepare.py, README.md: 정확한 입력 ZIP 검증과 재현 절차.

비공개 전달물: Nightroad-DV2-P02-v14-Input-Interruption.zip.
공개 GitHub에는 이 요약만 추가한다. 원본318개 파일이 ZIP과 바이트 동일함을 확인했고 운영 UI·모델·저장·음향·에셋 변경은0개다. 병합·배포 없음.

## 검증 방식과 결과

Ubuntu/Godot4.6.3 headless의 Input.parse_input_event로 합성 마우스·터치를 전달했다.
실제 Android OS가 아니다. AndroidViewportScale의4개 창 scale 설정을 **하네스에서 명시적으로** 적용했다. OS.has_feature(android)는 false이며 Android feature gate를 통과했다고 주장하지 않는다.
물리 크기720×1600 →1600×720, 짧은 변390 논리 단위의 엔진 입력 변환을 사용했다.

4상태(영입·XP·승급·새 원정 확인) ×2입력 ×8중단 방식 =64개 시나리오.
방식: 정상, 중복release, 회전 후 옛 위치release, 회전 후 새 위치release, 누른 중 Back, 포커스 상실, canceled release, 바깥 누름 뒤 회전/release.

| 실행 | 결과 |
|---|---|
| 원본 소스 | 56/64 통과, canceled release8건 실패 |
| 검수 도구의 취소 차단 프로토타입 | 64/64 통과 |
| 취소 후 새 정상 클릭 회복 | 8/8 통과, 위64건에 포함된 추가 검사 |

통과는 하네스의 구체적인 조건을 뜻한다. 중단 입력이 항상 무동작이었다는 의미가 아니다.
- 일반 클릭과 중복release는 한 번만 확정.
- Back 중단과 바깥 눌림/회전은 모델 진행을 바꾸지 않음.
- 회전 후 새 확인 위치에서release하면 한 번 확정될 수 있음.
- 합성 터치는 옛 물리 좌표release도 잡고 있던 버튼을 한 번 확정했다. 마우스 옛 위치release는 확정하지 않았다. 플랫폼 capture 정책의 실제 기기 재현은 미확인.
- 포커스 상실 notification 뒤release는 한 번 확정될 수 있었다. reward 상태의 focus pause는 유지됐다. 실제 OS의 입력 취소/순서까지 재현한 것은 아니다.
- 게임 모델·RNG snapshot에서 paused만 제외해 진행 변경을 비교했다. 저장은 test_mode로 비활성화했다.

## 발견 결함 DV2-P02-CANCEL — P1

재현: 확인 버튼에 pressed=true → 같은 위치로 pressed=false,canceled=true.
영입/XP/승급/새 원정 각각 마우스와 터치에서 재현됐다.
trace에 canceled=true가 원시 입력과 버튼 gui_input 양쪽에 도달한 것이 기록돼 있다. 취소 신호가 누락된 테스트 입력은 아니었다.

영향:
- 영입 기록1건 생성, XP 카드1건 소비, 승급 rank 증가 또는 새 원정 초기화가 발생.
- canceled 이벤트는 확정하지 않아야 한다는 인수 조건을 위반.
- 실제 Android가 이 상황에 같은 이벤트 순서를 내는지는 미검증이다. 휴대폰 진행 소실이 실제 발생했다고 보고하지 않는다.

실제 관련 경로:
- scripts/SquareScreen.gd:915 _input — 취소 입력의 확정 차단 분기 없음.
- scripts/SquareScreen.gd:483 _confirm_details, :616 _gate_new — 실제 확정/초기화 진입점.
- scripts/SkillDetails.gd — 확인 버튼 신호 연결과 모달 입력.

## 개선 제안과 검증 경계

제안: 화면 _input에서 canceled pointer 이벤트를 소비하고, 활성 BaseButton의 누름 상태를 해제한다.
별도 패치에 최소 diff를 제공했다. 이유: 취소 release가 확정 동작에 도달하는 것을 차단.
효과: harness-only 프로토타입에서는8실패 해소 및 새 정상 클릭8회 회복.
작업량S, 위험중간: 토글·오디오/QA 설정·다중 포인터 등 다른 입력에 대한 회귀 필요.
규칙 충돌 없음(경제·성장·저장 규칙 변경 아님). 다만 운영 파일은 두리 소유라 적용 권한 인수 필요.

프로토타입은 별도 관측 Node에서 버튼 상태를 해제했다. 제안 patch의 실제 SquareScreen 통합 실행 순서까지 검증한 것은 아니다. 패치는 운영/실행 사본에 적용하지 않았다.
회귀 인수 조건: 동일64건, 취소 뒤 재클릭, 메뉴/QA/음향 토글 상태, Back·새 원정 취소, 실제 Android ACTION_CANCEL/배경복귀, 저장 보호를 확인할 것.

## 차단·미검증

이번 Xvfb 실행은 X11 Display 연결을 만들지 못했다. 따라서 신규 렌더링 스크린샷은0장이며 이전 이미지를 이번 증거로 재사용하지 않았다. 엔진 입력 trace·상태 JSON이 이번 실행 증거다.
실제 Android 기기·APK 설치/업데이트·OS 회전/Back·브라우저 WASM/IndexedDB·하드웨어 터치·청취·성능은 미검증.
APK 세로 고정 정책과 별개로 resize stress를 검사했다. 사용자가 실제 APK에서 자동 가로 회전을 할 수 있다는 뜻이 아니다.
저장을 비활성화한 UI fixture이며 완주·재미·실제 진행 소실/복구의 증거가 아니다.

## 다른 팀 요청

두리: DV2-P02-CANCEL 재현과 패치를 검토하고, 채택하면 SquareScreen.gd의 정확한 기준/소유권/인수 조건을 지정해 주세요. 이번 전달은 인수 요청이며 자동 수락·반영 완료가 아니다.
QA: 승인된 실제 Android v0.14에서 누른 상태의 시스템 중단/취소가 같은 확정을 유발하는지 확인 필요. 데이터 삭제나 보호 설정 우회는 점검 조건이 아니다.

## 다음 후보

1. P1 **차단안의 설정·배치·잔여 입력 회귀** — 현재 취소 차단 프로토타입이 QA/소리 토글과 배치·모달 재열기에 영향을 주는지 격리 검수. 산출물: 좁은 회귀 도구·통합 주의점. 작업량S–M, 현재 소스로 가능, 운영 수정 권한 불필요. 완료 조건: 허용 입력과 취소 입력을 구분한 상태 증거.
2. P1 **실제 적용·기기 재검증** — 두리의 파일 인수 및 승인된 기기 접근 뒤 적용. 산출물: 실제 수정 커밋·동일 시나리오/실기 증거. 작업량M, 현재 운영 수정 제한과 충돌하므로 인수 전 착수 불가.

마지막 완료 지점: 재현64건·프로토타입64건/회복8건·원본 무결성 확인·비공개 전달물 저장. 결함 자체는 미수정으로 남는다.

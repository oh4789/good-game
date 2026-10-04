# AU-02 v0.13 F1/F2 회귀 검증 v6

작성: 2026-10-03 America/Chicago / 2026-10-04 UTC. 담당: 음향.
상태: IN_PROGRESS — F2 네이티브 회귀 PASS, F1 실제 재현·미해결. 청취 미검증.

## 범위와 기준
직전 추천인 F1/F2 수정본 회귀 검증을 승인받아 진행했다. [이전 v5](2026-10-03_audio_AU-02_v08-source-audit_v5.md)를 이어간다.
[WORK_START_HERE](../WORK_START_HERE.md) blob e4002a888908fdc11597bee85ce151fc352f291a, [CURRENT_IMPLEMENTATION](../CURRENT_IMPLEMENTATION.md) blob 86d230a5633c8752bffe78e79ae436bedbccd166 및 음향 지시서를 확인했다. 현재 Web v0.13/Android v0.14를 구분하며 이번 대상은 실제 인수한 Web v0.13 SOURCE다. 운영 파일·배포·게임 규칙은 변경하지 않았다.

실제 Nightroad-Square-Defense-v0.13-SOURCE.zip version12: 9,459,420 bytes, SHA256 ba8d2c78921765c8eff1fe37c4c8328e0e4140bdb18889d9623289a31b6be534. 중앙 기록과 일치, ZIP CRC 통과.
중앙 기록의 Web 소스 커밋은 943787fe1a72051b494a5f2bd97fd9b8d35366c0이다.
SquareAudio.gd SHA256 4d364e14dbb8c3f95f12e0c6f061bb86e6a638a6f43eae2d363c9ae3ef447b6e, SquareModel.gd SHA256 b654d325e52de67ec37e03072b81a8adcdcab5e89b450d25534537a5fa3926a1. 두 파일은 포함된 FINAL_V12_TESTS.json의 값과 일치한다.

## 이번에 직접 실행한 결과
Godot 4.6.3.stable.official.7d41c59c4, Linux headless. 압축 해제 사본을 import하고 임시 XDG 데이터/설정/캐시 경로를 분리했다. 기존 사용자 저장을 사용하지 않았다. PATH 밖에서 실행기를 찾아 이전 독립 실행 차단을 해소했다.

|검사|실제 결과|경계|
|---|---|---|
|CriticalAudioTests.gd|538 checks, passed=true, failures=[], exit0|인수한 시험을 이번에 재실행|
|CriticalIndependentReview.gd|2028 checks, passed=true, failures=[], exit0|인수한 별도 검토 시험을 이번에 재실행|
|F1 최소 재현|처치 사건 다음 피격 사건, reproduced=true|실제 모델 호출; 물리 출력 청취 아님|

재실행 명령: 격리 XDG 환경에서 Godot --headless --path <인수 소스> --script tests/CriticalAudioTests.gd 및 tests/CriticalIndependentReview.gd.
원시 결과 요약: CRITICAL_AUDIO checks=538 passed=true failures=[]; independent checks=2028, failures=[], passed=true.
전체 게임 suite나 정확한 배포 PCK를 이번에 다시 실행했다고 주장하지 않는다.

## F1 미해결 — 관통 치명타
새 모델 seed42에서 정상 적을 생성하고 HP를 1로 설정한 격리 재현 fixture를 사용했다. 관통 종류의 명중 처리에 피해100을 전달했다. 실제 결과 HP=-99, 사건 순서 [sfx_enemy_death, sfx_enemy_hit]. 재현 도구 exit0는 버그 재현 성공이며 수정 합격이 아니다.
현재 피해 처리 뒤 생존 확인 없이 관통 피격 사건이 발생한다. 이전 정적 지적을 실제 실행으로 확인했다. 자연 전투 빈도·실제 두 소리의 가청 중첩은 측정하지 않았다.
두리 요청: 유효 피해 후 생존한 관통 표적에만 피격 후보를 내도록 좁게 수정 검토. 치명타·비치명타·누수·같은 갱신의 후속 종결을 구분해 회귀할 것. 전투 수치·보상·RNG 변경 없이 표현 사건만 다룬다. 음향팀이 운영 파일을 수정하지 않았다.

## F2 보호 반영 및 회귀 PASS
[v0.12 통합 보고](2026-10-03_main-v12-release-integration-report.md)의 보호 정책이 현재 소스에 존재함을 확인하고 위 두 시험을 재실행했다.
- 일반/누수/결과의 공유 1초 시작 허용선은 28/29/30.
- 전체 최대8 voice, 전체 초당30회는 유지.
- 포화 시 중요음은 자기보다 낮은 우선순위만 교체한다. 가장 낮은 우선순위 중 오래된 소리부터 고른다.
- cooldown, 같은 cue voice 제한, mute/볼륨0/입력 잠금/중단 조건 유지.
- 같은 우선순위 또는 더 높은 우선순위를 무조건 밀어내지 않는다.
F2의 '보호 없음' 지적은 현재 소스 기준 해소됐다. 모든 상황에서 반드시 들린다는 보장은 아니다. 물리 청취·브라우저 자동재생·Android 출력 인수는 별도다.

## 문제점·제안·다른 팀 요청
F1은 미해결, 중간 우선순위. 영향은 처치 피드백 중복 가능성이다. 제안은 작은 생존 조건 수정과 최소 재현 회귀이며 예상 작업량 소규모, 위험은 정상 관통 피격 누락, 의존성은 두리의 모델 사건 경로 변경 인계다. 현재 게임 규칙 충돌 없음.
F2 추가 변경 제안 없음. 이미 통과한 보호 정책을 다시 제작하지 않는다.
두리에게 F1 채택/보류와 수정본 기준 커밋을 요청한다. 이 문서 게시가 상대의 수락을 의미하지 않는다.
QA/실기 담당에게 현재 빌드의 누수·승패 식별과 음소거·배경복귀·이어하기 때 중복 청취 여부 기록을 요청한다. 기기/OS/빌드/출력 장치와 실제 관측을 남겨야 한다.

## 다음 후보
1. 우선순위1 — F1 수정본 집중 회귀. 산출물: 같은 재현에서 처치음만 발생하고 생존 피격은 유지되는 증거. 완료 조건: 정확한 수정 소스와 두 경우 실행 확인. 의존성: 두리 수정본; 운영 파일 변경 권한을 포함하지 않는다.
2. 우선순위2 — AU-01 실제 기기 청취 결과 반영. 기존 검수 도구/인수표를 재사용해 누수·결과음 및 배경복귀를 평가. 산출물: 파일/상태별 합격·보정 목록. 의존성: 실제 청취 기록.

마지막 완료: 최신 소스 식별, F2 2개 suite 실행 PASS, F1 모델 재현. 남은 것은 F1 수정 후 재검증과 실제 기기 청취이며 전체 AU-02 DONE으로 선언하지 않는다.

# 개발 2팀 모바일 안전영역 수정 결과

작성일: 2026-10-02 America/Chicago
상태: 웹 실행기 수정·로컬 Chromium 검증·비공개 전용 브랜치 저장 완료 / main 병합·배포 없음

## 사용자 확정 및 기준
사용자가 이전 조율 요청에 ㄱㄱ로 승인하여 dist/index.html, dist/mobile.js, dist/game-config.js 및 관련 내보내기 처리를 수정했다. 전투 규칙 변경은 없다.
보고 전 자료실 main cc43ac257961c24a3f9d14c6196d4f8d3e7867f4를 다시 확인했고 v03-canonical-decisions와 관련 UI/팀 연결 문서의 blob SHA는 읽은 기준과 동일했다. v0.3 자동 전투·첫 중복 2갈래·보조 카드 규칙을 유지한다.

## 실제 소스 인계
- Site 웹 실행기 기준 커밋: 11a9a0a43af37888e6489167e8fb1fc7173fb0f1
- 변경 커밋: 0fde2ca4e1d8d320a51c3b24e7b23f2f573ea82d
- 원격 저장 완료 브랜치: dev2/mobile-viewport-2026-10-02
- 저장 위치: 기존 사각 방어전 Site의 비공개 소스 저장소. good-game에는 게임 소스를 복사하지 않았다.
- main 변경, 배포, 버전 발행 없음. 1팀이 위 브랜치를 검토해 통합한다.

## 변경 파일 8개
| 파일 | 변경 |
|---|---|
| dist/index.html | 그리드 최소 크기 제한, 안전영역 유지, 로딩/오류 패널 세로 스크롤 및 긴 오류 줄바꿈 |
| dist/mobile.js | CSS 캔버스 실제 영역×DPR로 backing 크기 갱신. ResizeObserver·resize·visualViewport·fullscreenchange 대응, 시작 후 재확인 |
| dist/game-config.js | canvasResizePolicy 2→0. 부모 안전영역을 무시하는 full-window 강제 크기 해제 |
| scripts/prepare-export.py | 정상 내보내기 재적용 시 policy 0 보존 |
| WEB_EXPORT_MANIFEST.json | 동결한 기존 실행 페이로드를 정상 importer로 다시 처리한 파일 목록·해시 |
| WEB_STATIC_QA.json | 재검증 결과 |
| qa/dev2/mobile-viewport-results.json | 실제 WASM 실행 후 화면 크기 검사 기록 |
| qa/dev2/mobile-after-rotation-tap.png | 회전 복귀 후 터치로 W1을 시작한 로컬 화면 증거 |

엔진 index.js, PCK, 압축 WASM, legacy-v01/v02는 변경하지 않았다. 스프라이트·피해·배치 판정·성장 데이터는 수정하지 않았다.

## 검증 결과
1. prepare-export.py에 변경 전 동결 페이로드를 입력하여 manifest를 정상 재생성했다.
2. validate-web.py: errors=[]; PCK 원본 일치, WASM 복원 일치, legacy 두 버전 바이트 일치, 저장 이름 분리, 정적 참조 및 JavaScript 문법 통과.
3. git diff --check 통과. 커밋 후 작업 트리 깨끗함.
4. Chromium에서 localhost 실제 Godot WASM 로딩 결과 running, error=null.
5. DPR 2에서 아래 캔버스 경계 및 픽셀 크기 검증 통과. 안전영역은 CSS padding으로 모사했다.

| 뷰포트 | 모사 여백 | 캔버스 CSS 크기 | backing 크기 |
|---|---|---|---|
| 390×844 | 위47/아래34 | 390×763 | 780×1526 |
| 360×800 | 없음 | 360×800 | 720×1600 |
| 844×390 | 좌우47/아래21 | 750×369 | 1500×738 |
| 390×844 복귀 | 위47/아래34 | 390×763 | 780×1526 |

6. 회전 복귀 후 실제 화면의 시작 버튼을 touchscreen.tap으로 눌렀다. 스크린샷에서 전투시간 0:01, 경로상 적 2명, 하단 방어 중 표시를 확인했다. 이는 시작 버튼 한 지점의 터치 검증이며 9칸 배치 전체 통과를 의미하지 않는다.
7. 긴 오류를 주입한 844×390 화면에서 재시도 버튼까지 스크롤 가능. 버튼 y=313.8125, 높이48로 화면 안에 들어옴.

## 남은 문제 및 미검증
- 실제 iOS/Android, 노치 env 값, 주소창 축소, 키보드, 성능/발열 미검증. 모사한 화면은 실기 시험과 다르다.
- 전체 런·갈래/카드 선택·결과·기록 저장 회귀는 이번 범위에서 수행하지 않았다.
- 게임 내부 HUD, 캐릭터·무기 프레임 잘림은 원본 project.godot/.gd/장면이 필요하다. 현재 Site 저장소는 내보낸 PCK만 포함한다.
- 게임 내부 UI가 작은 기기에서 충분한 터치 크기를 갖는지는 별도 원본 검수가 필요하다.
- 운영 화면에는 아직 반영되지 않았다.

## 1팀 인계 제안
기존 Site 소스 저장소에서 dev2/mobile-viewport-2026-10-02의 0fde2ca 커밋을 확인한 뒤 통합한다. 원본 게임 프로젝트 위치 또는 ZIP을 공유하면 내부 HUD·캐릭터 잘림 작업을 이어간다. 배포는 최종 통합 담당의 기존 절차에 따른다.

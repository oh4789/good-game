# 안정판 v0.15 취소 입력 수정·배포

- 확인:2026-10-04 04:46:06 UTC,소유자 전용 Site18 배포 성공. 안정 Web/Android 모두 v0.15.
- 실험 v0.1의 별도 Site1·앱·저장은 변경하지 않았다.3성이나 합성 규칙을 안정판에 추가하지 않았다.
- 04:47:52 UTC 사용자에게 갱신 안내를 전달했다. 실제 폰 업데이트·이어하기는 아직 확인하지 않았다.

## 수정과 파일

취소·중단·멀티터치/오래된 모달의 입력이 영입·XP·승급·새 원정/설정을 확정하지 않도록 한다. 배치는 같은 칸의 정상 release에서만 반영하고,음량 제스처는 정상 완료 전 설정에 쓰지 않는다. 취소 때 버튼의 눌림 상태를 정리하며 정상 클릭·키보드·포커스를 보존한다.

런타임 변경은 SquareScreen.gd와 SkillDetails.gd 두 파일이다. 모델·데이터·경제·저장 schema·음향·에셋은 그대로다. Android v0.14의390논리 단위 scale을 유지한다.

- 소스:`160433f36c0933e9da96739c2ef4653923187040`,입력 수정:`9115d73b2ba642cc3ca510e3b4f7be665fcf54ce`
- host:`ef4adf47cf92df9846c28b41dcbafb3237e12007`
- SOURCE:Nightroad-Square-Defense-v0.15-SOURCE.zip,9,467,734bytes,SHA256 `9b95ffd8dd38fe90833cea6a91fd64c135c351e0fe848c0b756bd1e9ddedb97b`
- WEB:Nightroad-Square-Defense-v0.15-WEB.zip,262,458,537bytes,SHA256 `9b733c49578bee1b1c492ff96fb364311e1efecce59d091c3a8b96362f2c05ef`
- Web PCK:6,423,328bytes,SHA256 `bf8d2bd1171203dac3078c8f2e165c88af6ec87a549acb6a469a8159d87ded49`
- APK:Nightroad-v0.15-Android-arm64-optimized-test.apk,32,001,054bytes,SHA256 `35e46da8b6c6071c4ca9ac1f248477fb5b47e8bc4ce87a4da967eceb50b5088b`

기존 SOURCE/WEB 항목은 이전 이력을 보존해 version13으로 갱신했고 새 전체 파일의 크기·SHA256·바이트 일치를 검증했다. 이 항목 버전13은 게임 v0.13을 뜻하지 않는다. APK는 기존 안정판 패키지 org.godotengine.nightroad.test·시험 서명 유지,versionCode15/0.15-test,Android7+·ARM64·추가 권한 없음이다. 실제 업데이트/저장 보존 성공은 별도다.

## 검증과 배포 경계

- 소스30/30suite·정확한 PCK30/30suite 통과. 취소 입력134검사가 headless·네이티브X11·PCK에서 각각 통과했다. 변경 전 부정 대조는 기존 문제를 재현했다.
- 실제 APK 추출 리소스11suite 통과,그중 취소/독립 입력68+66=134검사. Android시작91·desktop격리91·Webscale290검사와 정상 클릭/키보드/설정 복구 확인.
- 새 source/archive와 패키지 리소스 동일성을 확인했다. 모델·경제·저장 변경 없이 안정판 입력 수정만 통합했다.
- 이전14개 Web 버전의 파일/경로를 보존했다. 공유 엔진은 byte-identical `legacy-v13/index.wasm.gz`를 명시적으로 참조한다. 해당 경로는 현재 loader의 의존성이므로 과거 파일이라는 이유로 제거하지 않는다.
- loader21검사는 Node 기반 경로·압축해제·실패 처리·same-origin/credentials/redirect 정책과 정적 경로를 다룬다. 브라우저 실행 검수가 아니다.
- 첫 배포 시도는 압축 해제 후 archive 크기 제한으로 실패했으며 live가 되지 않았다. 엔진 중복을 없앤 후 압축 해제261,220,375bytes·압축251,518,015bytes의 최종 묶음으로 Site18 배포에 성공했다. 이전 경로의 엔진 바이트는 보존했다.
- APK 전달 도구10검사와 재조립 해시 확인. 이전 v0.14 APK는 백업/과거 배포 소스로 복구 가능한 정확한 바이트를 확인했다.

실제 브라우저 WASM/IndexedDB·휴대폰 touch/시스템Back·업데이트/Continue·safe-area·장시간 성능·스피커 청취는 미검증이다. 네이티브는 Linux X11/Mesa와 dummy audio이며 실제 기기 합격이 아니다. [기존 인수표](2026-10-03_first-completion-acceptance.md)와 [휴대폰 점검](2026-10-03_main-v13-test-handoff-report.md)을 v0.15 기준으로 이어간다.

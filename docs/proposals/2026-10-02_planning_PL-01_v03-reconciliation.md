# PL-01 — v0.3 현재 규칙과 제안의 차이 정리
- 작성일: 2026-10-02 America/Chicago
- 원본 작업 ID: PL-01
- 상태: DONE (문서 교차 검토 완료, 게임 구현/실행 완료 뜻 아님)
- 지시서: [기획 Work](../work-orders/2026-10-03-planning.md)
- 공통 절차: [WORK_START_HERE](../WORK_START_HERE.md)
- 현재 기준: [v0.3 canonical](2026-10-03_v03-canonical-decisions.md), 기준 커밋 6412c5252f6e6da78f402f32aa47bdf937082f12
- 게임 소스 기준: 922f0808783aa31a88395a80c877e71bce7f0edc
- 배포 기준: 11a9a0a43af37888e6489167e8fb1fc7173fb0f1
- 실제 인수 범위: GitHub 문서. 비공개 게임 소스/PCK·에셋을 이번 작업에서 직접 검증하지 않음.

## 1. 상태를 구분한 현재 규칙
| 분류 | 내용 | 출처 |
|---|---|---|
| 확정 방향 | 사각 경로1회 후 공용HP 손실/퇴장, 안쪽3×3, 최대3명, 준비 중 배치, 단일진영, 자동 전투·수동궁극기 없음, 약7분 목표 | 기준 §2 |
| 확정 방향 | 첫 중복 즉시 승급1과2갈래 선택, 선택 유지, 이후 중복마다 승급, 낮은 상한 환급 성장 없음 | 기준 §2 |
| 확정 방향 | 영웅/승급/갈래/카드/XP/자원은 런 한정, 새 런 초기화 | 기준 §2 |
| 확정 방향 | 처치XP 보조 카드3택1과 별도 자원 영입 분리, 웨이브 종료 성장 이중 지급 없음 | 기준 §2 |
| 현재 구현 보고 | 비비·탄코·로코 각2갈래, 자동 전투, 최고 웨이브 저장, 중간 런 이어하기 없음 | 기준 §3~5 |
| 임시 구현 수치 | 처음 두 영입12씩·미보유 보장, 세 번째24 이후+6, 승급당 기본공격력+18%p, 효과 개수 증가는 승급2까지 | 기준 §4 |
| 후속 제안 | 신규 영웅·공용/전용 카드 후보·대기석·감속·추가진영·표현 정책 | 기준 §7 및 개별 후보 |
| 미검증 | 브라우저/휴대폰 실제 흐름·저장·터치·성능·일반 사용자 시간/재미·최종 에셋 통합 | 기준 §5~6 |

“확정”은 현재 기준 문서가 기록한 사용자 방향이다. 이번 기획팀이 새로 승인했다는 뜻이 아니다.
178항목 및 동일40시나리오의 소스/PCK 결과는 통합 담당 보고이며 이번 독립 재실행 결과가 아니다.

## 2. 00~19 원문별 차이표
파일 번호가 겹치므로 전체 파일명을 링크한다. 아래 “기준 §”는 위 canonical의 절 번호다.
관련 절과 현행 해석을 검토했으며 기존 원문은 수정하지 않는다.

| 기존 파일·관련 절 | 옛 규칙/가정 | 현재 규칙/해석 | 현재 출처 | 적용 여부 |
|---|---|---|---|---|
| [00-reading-guide](2026-10-02_00-reading-guide.md) §2~5 | 초기 읽기 순서·초기 자료 범위 | 현재 기준 우선, 소스는 별도 Site | 기준 §1·5·8 | 저장 원칙만 유지 |
| [01-game-direction-decisions](2026-10-02_01-game-direction-decisions.md) §2~4 | 수동 궁극기·재료·영구 보유 미정 | 자동 전투·즉시 승급·런 한정 | 기준 §2 | 충돌 항목 대체 |
| [02-cogwork-heroes-builds-proposal](2026-10-02_02-cogwork-heroes-builds-proposal.md) §3·6·7 | 3갈래·수동 궁극기·확장 병종 | 기본3종 각2갈래 | 기준 §2·3·7 | 외형 아이디어만 참고 |
| [03-summoning-growth-balance-qa-proposal](2026-10-02_03-summoning-growth-balance-qa-proposal.md) §2·4·6 | 1~3성, 재료1+2, 최대성 환급·구비용 | 중복마다 승급, 환급 성장 없음, 새 비용 | 기준 §2·4 | 구검수 기대값 제외 |
| [04-defense-next-design-agenda](2026-10-02_04-defense-next-design-agenda.md) 사용자 확정/다음 설계 우선순위 | 구기준 기반 설계 순서 | 현행 기획 작업 PL-01/02 | 기준 §8·9 | 과거 작업 목록 보관 |
| [05-enemies-10waves-test-plan](2026-10-02_05-enemies-10waves-test-plan.md) §4~6·8 | 241적·구비용·궁극기 구간 | 현재 소스의 생성/XP 확인 필요 | 기준 §2·4·5 | 웨이브 수치 채택 추정 금지 |
| [06-combat-growth-ultimates-spec](2026-10-02_06-combat-growth-ultimates-spec.md) §3~6 | 전용9종·재료/환급·수동 궁극기 | 첫 중복 갈래, 카드 보조, 자동 | 기준 §2~4 | 구전투 묶음 적용 안 함 |
| [06-defense-experience-work-orders](2026-10-02_06-defense-experience-work-orders.md) §4·5·7 | 궁극기 조작·미사용 피드백 | 수동 궁극기 없음 | 기준 §2·8 | 해당 안내/인계 제외 |
| [07-team-roles-first-production-cycle](2026-10-02_07-team-roles-first-production-cycle.md) §4~7 | 궁극기 포함 첫 제작 주기 | 현재 Work 지시서별 범위 | 기준 §8 | 동작/판정 분리 원칙만 참고 |
| [07-ui-state-art-audio-spec](2026-10-02_07-ui-state-art-audio-spec.md) §1~5·7 | 궁극기 HUD·승급 재료·환급 | 승급 횟수와2갈래·보조 카드 표시 | 기준 §2~4·6 | UI 일반 원칙만 참고 |
| [08-developer-handoff-qa-roadmap](2026-10-02_08-developer-handoff-qa-roadmap.md) §2·5·6·8·9 | star/material/charge, 최대성환급, 확장 | 런 한정 승급·최고 웨이브 저장 | 기준 §2·4·7 | 구데이터/검수 자동이식 금지 |
| [09-integration-review-placement-findings](2026-10-02_09-integration-review-placement-findings.md) §2~4 | 구조준·구사거리 기반 배치 계산 | 실제 현행 사거리/좌표로 확인 | 기준 §3~5 | 계산 방법 참고, 수치 적용 보류 |
| [09-spec-reconciliation-card-pool-fix](2026-10-02_09-spec-reconciliation-card-pool-fix.md) §3~6 | G03충전 상한·궁극기 조준·파쇄 | 궁극기 없음, 로코 유도/관통 | 기준 §2·3 | 구수정안 미적용 |
| [10-common-cards-party-growth-spec](2026-10-02_10-common-cards-party-growth-spec.md) §4~7 | G03충전·전용2+공용1 | 보조 카드3택1, 실제 풀 확인 | 기준 §2·7 | 구ID/추첨안 자동채택 금지 |
| [11-cogwork-roster-promotion-build-framework](2026-10-02_11-cogwork-roster-promotion-build-framework.md) §4~7 | 3성·신규3명·궁극기·카드3갈래 | 기본3명/중복2갈래/계속성장 | 기준 §2~4·7 | 확장 보관 |
| [11-support-heroes-defense-references](2026-10-02_11-support-heroes-defense-references.md) §3~6 | 지원 궁극기·토리 카드갈래·감속 | 지원 영웅 현행 밖 | 기준 §2·7 | 역할 참고만 |
| [12-cogwork-54cards-18builds-catalog](2026-10-02_12-cogwork-54cards-18builds-catalog.md) §1~10 | 54전용·18빌드·소이 제외·파쇄 | 6갈래, 탄코 소이·로코 유도/관통 | 기준 §3·7 | 현재 목록 아님 |
| [13-party-recruitment-release-validation](2026-10-02_13-party-recruitment-release-validation.md) §2~6 | 6종 영입·카드 갈래 투자·확장순서 | 현재3종·첫중복 갈래 | 기준 §2~4·7 | 후속 후보 |
| [14-pin-ash-tori-playstyle-handoff](2026-10-02_14-pin-ash-tori-playstyle-handoff.md) §1~7 | 핀/애쉬/토리·확장 영입·수동궁극기 | 3영웅 검수 우선 | 기준 §3·7·9 | 확장 필수화 금지 |
| [15-new-heroes-focused-test-scenarios](2026-10-02_15-new-heroes-focused-test-scenarios.md) §1~5 | 신규3명·궁극기/카드 빌드 검수 | 현행6갈래 검수 | 기준 §3·7·9 | 이번 완료조건 아님 |
| [15-three-builds-first-implementation-pack](2026-10-02_15-three-builds-first-implementation-pack.md) §1~5 | 대표1갈래·19카드·K/F연쇄 | 첫중복2갈래, 카드 보조 | 기준 §2·3·7 | 현행팩으로 채택 금지 |
| [16-new-build-feasibility-amendments](2026-10-02_16-new-build-feasibility-amendments.md) §2~5 | 애쉬0.75초·핀·토리 보완 | 확장 별도 채택 | 기준 §7 | 미적용 |
| [16-recruit-swap-build-guide-ux](2026-10-02_16-recruit-swap-build-guide-ux.md) §3~7 | 재료·충전·대기석·카드갈래 | 첫중복2갈래, 현행3종 | 기준 §2~4·7 | 충돌 UI 제외 |
| [17-first-run-wave-results-experience](2026-10-02_17-first-run-wave-results-experience.md) §3·4·6·7 | HELP07궁극기/08핵심카드·영구 미정 | 자동·첫중복 선택·런한정 | 기준 §2·4 | 충돌 문구 제외 |
| [17-growth-draft-recruitment-model-results](2026-10-02_17-growth-draft-recruitment-model-results.md) §1~4 | 카드빌드 확률·3성률 | 중복 승급/갈래 성장 | 기준 §2·4 | 계산결과 전용 금지 |
| [18-pilot-integration-scope-handoff](2026-10-02_18-pilot-integration-scope-handoff.md) §3~8 | 19카드·재료·환급·확장 순서 | 현행 기본3종6갈래 | 기준 §2~4·7 | 통째 적용 금지 |
| [18-target-build-opportunity-policy](2026-10-02_18-target-build-opportunity-policy.md) §1~7 | 핵심/완성 카드 목표 보정 | 갈래는 첫중복에서 선택 | 기준 §2·7 | 미채택 구모델 |
| [19-dev-team-state-audio-integration](2026-10-02_19-dev-team-state-audio-integration.md) §3·5·6 | 궁극기 입력·충전 상태 | 자동 전투, 현재 사건 매핑 필요 | 기준 §2·6·8 | 중복방지 원칙만 참고 |

원문에 “사용자 확정”으로 적힌 과거 규칙도 현행 canonical과 충돌하면 현재 규칙으로 사용하지 않는다.
현행 기준에 상세 수치가 없는 항목은 오래된 문서의 숫자를 채택된 값으로 승격하지 않는다.

## 3. 여섯 갈래 — 장단점은 관측할 가설
갈래의 이름/방향은 기준 §3. 아래 장점·약점·측정은 검증 설계다.

| 갈래 | 역할·장점 가설 | 약점 가설 | 관측 항목 |
|---|---|---|---|
| 비비 연사 | 한 표적 지속 집중 | 표적 교체·짧은 노출 | 표적 유지시간·유효/과잉 피해 |
| 비비 탄막 | 여러 표적 처리 | 고립 강적·피해 분산 | 공격당 고유 적중 수·단일대상 시간 |
| 탄코 폭발 | 밀집 무리 순간 제거 | 산개·착탄 전 처치 | 폭발당 적중 수·과잉 피해 |
| 탄코 소이 | 남는 불길로 후속 적 처리 | 빠른 통과·짧은 노출 | 장판 체류·실제 틱·중첩 |
| 로코 유도 | 강한 표적 대응 | 약한 적 다수·과잉 피해 | 강적 피해·표적 소실·보스 시간 |
| 로코 관통 | 직선 적 연속 타격 | 산개·모서리 | 발사당 고유 적중·궤적·누수 |

탄코 소이를 신규 애쉬와 겹친다는 이유로 삭제하지 않는다. 로코를 파쇄 전용으로 고정하지 않는다.
실제 표적 우선순위·탄도·방어 계산·틱은 소스를 인수한 담당의 확인이 필요하다.

## 4. 최신 팀 자료와 추가 충돌
| 자료 | 확인 사항 | 현재 처리 |
|---|---|---|
| [QA v2](2026-10-02_qa-v03-baseline-correction-v2.md) | 로그인 화면에서 실행 검수 차단, 옛19카드 QA 정정 | 게임 버그/불합격으로 해석하지 않음 |
| [디자인 v8](2026-10-02_design-team-hero-motion-review-v8.md) | 재생 검토물 제작, 잘림/정렬 남음, 구18안 참조 | 현재 전투규칙 근거 아님, 최종 에셋 미완료 |
| [음향 v7](2026-10-02_audio-v03-integration-acceptance-v7.md) | 버전 메타데이터 확인, 다운로드 인수 실패, 실제 연결 미검증 | 관통 접촉마다 폭발음 적용 금지 후보 등 실제 사건 확인 후 연결 |
| [6갈래 밸런스](2026-10-02_v03-six-branches-balance-validation.md) | 갈래/경제/확률의 조건부 검토 | PL-02에서 재사용, 새40런 의무 추가 안 함 |
| [12종 카드 후보](2026-10-02_v03-support-card-catalog-proposal.md) | 공용피해+4%p와 승급×카드 곱셈 등 미채택 | 현재 카드 목록 아님 |
| [24 공용 후보](2026-10-02_24-v03-common-card-candidates.md) | +5%p와 승급/카드 가산·HP후보 | 12종안과 동시에 합치지 않음 |
| [후보 부족 검산](2026-10-02_v03-card-pool-exhaustion-audit.md) | 12종안 단독영웅4번째 후보 부족, 공용 허용 수정은 조건부 | 설계 모델 결과, 실제 게임 버그라고 단정하지 않음 |
| [25 토리](2026-10-02_25-v03-support-hero-tori-rework.md) | 2갈래 지원 확장 후보 | 현행 범위 밖, 추가 설계 중단 |

12종안과24안의 충돌은 실제 카드 목록·산식·최대 선택 횟수 인수 후 통합 담당이 유지/대체/보류를 정리해야 한다.
현재 동등한 다른 제안끼리 합성한 세 번째 풀을 만들지 않는다.

## 5. 필요한 결정과 입력
지금 사용자에게 다시 물어야 할 확정 방향 질문: 없음.
이미 확정한 자동 전투·첫중복2갈래·런 한정·최대3명을 다시 묻지 않는다.
미채택 카드안/토리 등 확장 채택은 현재 작업 완료의 선행조건이 아니므로 보류한다.

통합 담당에게 필요한 검수 입력(사용자 새 방향 결정과 구별):
- 현행 카드ID/효과/상한/유효조건/추첨 정책·공속 및 사거리 제한.
- XP 요구량·런 최대XP·초기 자원/처치 수입·영입 확률.
- 갈래/카드 동시 발생 정책 및 접근 가능한 동일 버전 검토 자료.
이 요청은 문서 인계이며 직접 메시지 전송/수락 확인은 아니다.

## 6. 검증·완료 기록
- 00~19 전체28개 파일을 조회하고 관련 절·충돌 항목을 대조했다.
- 차이표28행 각각 원문 링크와 canonical 절 번호를 포함한다.
- 현재6갈래 모두 역할/장점/약점/관측을 포함한다.
- 확정/구현 보고/임시값/제안/미검증을 분리했다.
- 기존 파일·지시서·다른 팀 문서·게임 코드·배포를 변경하지 않았다.
- PL-01 문서 산출 완료. 실행 검수는 PL-01 범위가 아니며 미수행.
- 다음 배정 작업: PL-02 비교표 준비. 사용자 이번 요청에 따라 이어서 완료한다.

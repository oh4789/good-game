# AU-02 현재 이벤트 인계표

작성일: 2026-10-02 America/Chicago / 상태: IN_PROGRESS (의미 기준 manifest 완료, 통합 담당 파일 인수 미확인)

지시서: ../work-orders/2026-10-03-audio.md. 기준/소스/배포 버전은 AU-01 결과와 동일. AU-01의 청취 차단과 독립적인 기존 자산 대응표만 작성했다.

실제 엔진 API 미확인. 아래 event는 의미 기준 제안이며 gain·voice·간격·우선순위는 시험값이다. priority는 큰 수 우선이다. 상대 경로는 Nightroad_Audio_v03.zip을 푼 폴더 기준. 기존 파일의 SHA256을 이번에 다시 계산했다.

|의미 사건|sound ID|파일|gain dB|동시수|최소간격 ms|우선순위|loop|SHA256|
|---|---|---|---:|---:|---:|---:|---|---|
|weapon_fired:BBI|sfx_mg_fire|assets/sfx_mg_fire_v01_a.wav|-12|3|80|50|False|6ef494b7d6b623b28be7b23d5cc378b951b06871287b21f283125e9e471565a6|
|weapon_fired:BBI|sfx_mg_fire|assets/sfx_mg_fire_v01_b.wav|-12|3|80|50|False|e67cef6e10b412c280a9e0dd935b789ed638e2a96f76c2edd68a34601d22664f|
|weapon_fired:BBI|sfx_mg_fire|assets/sfx_mg_fire_v01_c.wav|-12|3|80|50|False|3857594fe2936394b94b7d0116c560a7b7cc38859ff78ce4365ff7604f03b84a|
|weapon_fired:CAN|sfx_cannon_fire|assets/sfx_cannon_fire_v01_a.wav|-9|2|120|50|False|50d6e02fcba850941c2228f98eed3d81d794d8fd9938b6022f32042b2f37c015|
|weapon_fired:CAN|sfx_cannon_fire|assets/sfx_cannon_fire_v01_b.wav|-9|2|120|50|False|49a3d0e3fc782b6b8069554f419489b94c86afb6343b494abb2886f1479644fe|
|projectile_impacted:CAN|sfx_cannon_impact|assets/sfx_cannon_impact_v01_a.wav|-8|2|100|50|False|6efd61aded3036a8ae4c3ac8188ad1362a4476c599ebd4417c324e4aae172d38|
|projectile_impacted:CAN|sfx_cannon_impact|assets/sfx_cannon_impact_v01_b.wav|-8|2|100|50|False|9254dd8b694759a76c77bc6f6503d22f4dfb0d9f0ce914e799209f2bdba928e1|
|weapon_fired:RKT|sfx_rocket_fire|assets/sfx_rocket_fire_v01_a.wav|-9|2|120|50|False|6f031a3a5d279019ee4b2ac8fe641543451cb7c750f3588ad54ae378cc651463|
|weapon_fired:RKT|sfx_rocket_fire|assets/sfx_rocket_fire_v01_b.wav|-9|2|120|50|False|cd050e7ffb7f94a38f3acadb6610951397406099f1dafd44483c385eeca3bde4|
|projectile_impacted:RKT|sfx_rocket_impact|assets/sfx_rocket_impact_v01_a.wav|-8|2|100|50|False|e7b095f01e36707ee39bdec3ed58c15eca2cb967bbc504b994c9ba105cae5796|
|projectile_impacted:RKT|sfx_rocket_impact|assets/sfx_rocket_impact_v01_b.wav|-8|2|100|50|False|c799eeea041095726b1efca3f4a1dddd6d75e76f86708eb6d4ad22f96159ddc8|
|enemy_damaged:survived|sfx_enemy_hit|assets/sfx_enemy_hit_v01_a.wav|-18|2|100|50|False|512ce0fcc75366dbc475c9d3c9651760e0dc06914b6dad8d6262907481af627a|
|enemy_damaged:survived|sfx_enemy_hit|assets/sfx_enemy_hit_v01_b.wav|-18|2|100|50|False|88b82c8686e22e645043108acc8ed1f9f574aeb11ee942c7b800eaf4d8dfbade|
|enemy_killed|sfx_enemy_death|assets/sfx_enemy_death_v01_a.wav|-16|2|100|50|False|bce7b180445830cbc9145ac5ef6e251085e7fcfe5b4c1ef5fe59645ae6dffc7c|
|enemy_killed|sfx_enemy_death|assets/sfx_enemy_death_v01_b.wav|-16|2|100|50|False|573becb87c0435c15bc9acc082dc571a26889529e134605bcb0c789af0ca5710|
|enemy_leaked|sfx_leak|assets/sfx_leak_v01_a.wav|-6|1|250|100|False|ff061963b34c8e0727f3b4bed9ceaf7b0e29bf7afc1801fe0a7080f93e5e2625|
|ui_action_accepted:generic|ui_confirm|assets/ui_confirm_v01.wav|-12|2|120|70|False|6954c9557815e44ea9acc3c2925ea91e9e8a421a659fc31babaf8086dc192da7|
|ui_action_rejected|ui_reject|assets/ui_reject_v01.wav|-14|2|300|70|False|33d3e2c7eb2c239f7337ca2a223776bab6938a4f7ce1fb252438bb4ae8d5139a|
|hero_deployed|ui_deploy|assets/ui_deploy_v01.wav|-10|2|120|70|False|e42dc551d610f45a767bcaf689b7285f58f7ba37f63707caa11c29ff983a8fed|
|recruit_resolved:new|ui_recruit_new|assets/ui_recruit_new_v01.wav|-9|2|120|70|False|9181616b07415956dd97d8cb6742d8ba0ffd9fef5ba150fda8730f4bc08f259a|
|card_panel_opened|ui_level_open|assets/ui_level_open_v01.wav|-10|2|120|70|False|86acf1c38d6de860928d8fd4769363620f0f0cf983149e835c71e785b30f0fee|
|card_selected:accepted|ui_card_apply|assets/ui_card_apply_v01.wav|-10|2|120|70|False|2ec0e20d91debdb5b126a2f8ed361366db63cab7ad2d3dd4457f652f1387303a|
|wave_started|ui_wave_start|assets/ui_wave_start_v01.wav|-10|2|120|70|False|7af77747e6cea5bbb3f42fff86894fda72c3a6bd77d52a3514ea0ce6b97f0f36|
|run_finished:win|ui_victory|assets/ui_victory_v01.wav|-9|1|120|100|False|1423d5921bc86bbc858bc4a34c5f2515dae2db0ca75171c942702161c8438da7|
|run_finished:lose|ui_defeat|assets/ui_defeat_v01.wav|-11|1|120|100|False|4e89db1259b52f29fb362bc55fdcdb67542ad1e60bf09ea0612a3dc863a52895|
|battle_music|bgm_battle|assets/bgm_battle_v01.wav|-18|1|0|20|True|07003d5413693a411393b0aa5983a32165505aa2a182f93ff0ae51732d420d98|
|boss_encountered|bgm_boss|assets/bgm_boss_v01.wav|-20|1|0|20|True|ee1bbcb34fb7e7caa1dd48fbbe838b4a30fccb80d6e0508dd0f0b08dba14c227|
|recruit_resolved:duplicate_promoted|ui_promote|assets/ui_promote_v01_a.wav|-9|1|120|50|False|cfcd2bf5f6b22b90ab3922a79167b9eed22dee175d34bb2812a44a89d6e3757b|
|fire_field_created:CAN|sfx_cannon_incendiary_ignite|assets/sfx_cannon_incendiary_ignite_v01.wav|-13|2|120|50|False|ac7bd0137a00af167379bd22fd050c1b8519fda5ff18f1c45d652d6a4e4117f8|
|fire_fields_active_changed:CAN|sfx_cannon_incendiary_loop|assets/sfx_cannon_incendiary_loop_v01.wav|-24|1|120|50|True|46098699824935a33415cc3e9977f8410849f55d3e8fc320578108beb49f6894|
|branch_panel_opened|ui_branch_open|assets/ui_branch_open_v01.wav|-10|1|0|50|False|2bb598fa912c09a7b8075d33f3a9ad16afd44349ecf2b81a5a6bfbe445df57eb|
|branch_selected:accepted|ui_branch_apply|assets/ui_branch_apply_v01.wav|-10|1|0|50|False|2fd2d68d6bb9960f114254e32707f9d676ce35b4a381a140bf45007ef656f61f|
## 연결 조건 및 비활성 소재
BBI 연사/탄막은 실제 발사를 따르되 한 탄막 묶음의 소리가 과도하게 중첩되지 않도록 위 제한을 시험한다. CAN 폭발은 적별 피해가 아닌 착탄에 연결한다. CAN 소이는 장판 생성 시 ignite, 활성 장판 수 0→양수에서 공용 loop 1개 시작, 양수→0에서 종료한다.
RKT 유도는 실제 착탄에 impact. 관통은 접촉마다 rocket_impact를 재생하지 않는다. 생존 피격은 enemy_hit, 처치는 enemy_death. 종결 착탄의 종류는 두리의 실제 사건 API 확인 후 조건을 확정해야 한다.
신규 영입=ui_recruit_new 1회, 첫/추가 중복=ui_promote 1회, 갈래 확정=ui_branch_apply 1회. 같은 거래에 ui_confirm/duplicate/material 소리를 추가하지 않는다. 첫 승급과 함께 열리는 갈래 창의 ui_branch_open은 억제한다.
카드 선택은 승인된 상태 변경에 ui_card_apply. UI 재렌더/앱 복귀는 새 사건이 아니다. runId+eventId 기반 중복 제거는 API 확인 후 적용한다. 카드·준비에서 전투 지연 재생 큐를 비우고, 정지 사유가 남아 있으면 재개하지 않는다. 새 런·결과에서 이전 런 콜백/소이 루프를 정리한다. 결과음은 1회, BGM fade 300ms는 시험 제안이다.
현재 비활성: 수동 궁극기/준비음, duplicate 재료음, 최대성 환급, PIN/ASH/TOR 전용 사건, 실제 장갑 기제가 확인되지 않은 armor_break. 원본은 보존한다. ASH 점화/루프의 바이트만 CAN 소이 후보로 재사용한다.
## 검증과 인수 상태
현재 WAV 32개의 파일 경로와 해시 일치 확인. AU-01의 46개 기존 소재와 구분하며 두 branch UI는 기존 v03 패키지에서 재사용한다. gain은 파일 샘플 피크와 다른 재생 설정이다. 전체 믹스 클리핑, 엔진 음성 제한, 휴대폰 출력, 7분 청취는 미검증.
기존 승인 전달물 Nightroad_Audio_v03.zip은 로컬 열기/전체 CRC 검사 성공. 다른 Work/두리 환경에서 파일을 열었다는 증거는 없다. 두리가 해당 ZIP을 인수하고 실제 사건 이름 및 연결 지점을 제공하면 런타임 검수로 진행한다. 사용자에게 새 규칙 결정을 요구할 필요는 없다.
저장소에는 이 표만 공개하며 WAV 바이너리는 업로드하지 않았다. 추가 음원 제작·게임 코드 수정·배포 없음.
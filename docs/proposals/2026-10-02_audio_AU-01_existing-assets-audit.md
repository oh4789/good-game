# AU-01 기존 음원 인수·파일 검사 결과

작성일: 2026-10-02 America/Chicago / 상태: BLOCKED (직접 청취), 파일 검사 완료

지시서: ../work-orders/2026-10-03-audio.md

기준: 2026-10-03_v03-canonical-decisions.md (blob 4929e26b4bc7e23b04acd1f0fecf72c933890dba). 소스 922f0808783aa31a88395a80c877e71bce7f0edc, 배포 11a9a0a43af37888e6489167e8fb1fc7173fb0f1. 게임 실행 검수 아님.

## 직접 검사

All_v1 실제 WAV 46개: P0 17, P1 14, 확장 13, BGM 2. wave로 PCM24를 직접 디코딩해 길이·채널·샘플레이트·샘플 피크·비무음·SHA256을 계산했다. 모든 파일이 기존 manifest의 해시/형식/길이와 일치하고 비무음이다. 전부 48kHz PCM24, BGM만 2채널, 나머지 1채널이다. 원본 수정과 새 합성은 하지 않았다.

각 행 청취는 모두 미검증이다. 재사용 후보는 파일 기술 검사 통과를 의미하며 청취 합격이나 게임 적용 승인이 아니다. 보정 필요 여부는 청취 전 미정이다.

## 출처·사용 조건

동봉 manifest에는 NumPy/SciPy 자체 합성, 외부 오디오 샘플 미사용, 독점권 주장 없음으로 적혀 있다. 생성 스크립트의 합성/파일 읽기 부분과 메타데이터를 확인했다. 이는 사용권 계약서 또는 법적 권리 심사 보증이 아니다. 공개 바이너리 업로드는 하지 않는다. 기존 승인된 파일 전달 경로의 ZIP을 재사용한다.

## 파일별 검사
경로는 Nightroad_Audio_All_v1/ 기준. 검사/청취 열의 PASS/미검증은 각각 수치 검사와 직접 청취 상태다.
|파일|초|peak dBFS|분류|검사/청취|SHA256|
|---|---:|---:|---|---|---|
|p0/sfx_mg_fire_v01_a.wav|0.100|-3.000001|재사용 후보|PASS / 미검증|6ef494b7d6b623b28be7b23d5cc378b951b06871287b21f283125e9e471565a6|
|p0/sfx_mg_fire_v01_b.wav|0.100|-3.000001|재사용 후보|PASS / 미검증|e67cef6e10b412c280a9e0dd935b789ed638e2a96f76c2edd68a34601d22664f|
|p0/sfx_mg_fire_v01_c.wav|0.100|-3.000001|재사용 후보|PASS / 미검증|3857594fe2936394b94b7d0116c560a7b7cc38859ff78ce4365ff7604f03b84a|
|p0/sfx_cannon_fire_v01_a.wav|0.260|-3.000001|재사용 후보|PASS / 미검증|50d6e02fcba850941c2228f98eed3d81d794d8fd9938b6022f32042b2f37c015|
|p0/sfx_cannon_fire_v01_b.wav|0.260|-3.000001|재사용 후보|PASS / 미검증|49a3d0e3fc782b6b8069554f419489b94c86afb6343b494abb2886f1479644fe|
|p0/sfx_cannon_impact_v01_a.wav|0.450|-3.000001|재사용 후보|PASS / 미검증|6efd61aded3036a8ae4c3ac8188ad1362a4476c599ebd4417c324e4aae172d38|
|p0/sfx_cannon_impact_v01_b.wav|0.450|-3.000001|재사용 후보|PASS / 미검증|9254dd8b694759a76c77bc6f6503d22f4dfb0d9f0ce914e799209f2bdba928e1|
|p0/sfx_rocket_fire_v01_a.wav|0.360|-3.000001|재사용 후보|PASS / 미검증|6f031a3a5d279019ee4b2ac8fe641543451cb7c750f3588ad54ae378cc651463|
|p0/sfx_rocket_fire_v01_b.wav|0.360|-3.000001|재사용 후보|PASS / 미검증|cd050e7ffb7f94a38f3acadb6610951397406099f1dafd44483c385eeca3bde4|
|p0/sfx_rocket_impact_v01_a.wav|0.320|-3.000001|재사용 후보|PASS / 미검증|e7b095f01e36707ee39bdec3ed58c15eca2cb967bbc504b994c9ba105cae5796|
|p0/sfx_rocket_impact_v01_b.wav|0.320|-3.000001|재사용 후보|PASS / 미검증|c799eeea041095726b1efca3f4a1dddd6d75e76f86708eb6d4ad22f96159ddc8|
|p0/sfx_enemy_hit_v01_a.wav|0.085|-3.000001|재사용 후보|PASS / 미검증|512ce0fcc75366dbc475c9d3c9651760e0dc06914b6dad8d6262907481af627a|
|p0/sfx_enemy_hit_v01_b.wav|0.085|-3.000001|재사용 후보|PASS / 미검증|88b82c8686e22e645043108acc8ed1f9f574aeb11ee942c7b800eaf4d8dfbade|
|p0/sfx_enemy_death_v01_a.wav|0.220|-3.000001|재사용 후보|PASS / 미검증|bce7b180445830cbc9145ac5ef6e251085e7fcfe5b4c1ef5fe59645ae6dffc7c|
|p0/sfx_enemy_death_v01_b.wav|0.220|-3.000001|재사용 후보|PASS / 미검증|573becb87c0435c15bc9acc082dc571a26889529e134605bcb0c789af0ca5710|
|p0/sfx_leak_v01_a.wav|0.420|-3.000001|재사용 후보|PASS / 미검증|ff061963b34c8e0727f3b4bed9ceaf7b0e29bf7afc1801fe0a7080f93e5e2625|
|p0/sfx_armor_break_v01_a.wav|0.280|-3.000001|현재 미사용|PASS / 미검증|2edbe11b8ba6a6001361bda48b12d5be6ea3a0fd505e062d8915be9805027993|
|p1/ui_confirm_v01.wav|0.090|-4.000001|재사용 후보|PASS / 미검증|6954c9557815e44ea9acc3c2925ea91e9e8a421a659fc31babaf8086dc192da7|
|p1/ui_reject_v01.wav|0.140|-4.000001|재사용 후보|PASS / 미검증|33d3e2c7eb2c239f7337ca2a223776bab6938a4f7ce1fb252438bb4ae8d5139a|
|p1/ui_deploy_v01.wav|0.180|-4.000001|재사용 후보|PASS / 미검증|e42dc551d610f45a767bcaf689b7285f58f7ba37f63707caa11c29ff983a8fed|
|p1/ui_recruit_new_v01.wav|0.700|-4.000001|재사용 후보|PASS / 미검증|9181616b07415956dd97d8cb6742d8ba0ffd9fef5ba150fda8730f4bc08f259a|
|p1/ui_recruit_duplicate_v01.wav|0.400|-4.000001|현재 미사용|PASS / 미검증|4798bdaca0fd41a535f5bb5a16c634c5e85d728f80de5791bd04808f1bc23a19|
|p1/ui_level_open_v01.wav|0.360|-4.000001|재사용 후보|PASS / 미검증|86acf1c38d6de860928d8fd4769363620f0f0cf983149e835c71e785b30f0fee|
|p1/ui_card_apply_v01.wav|0.320|-4.000001|재사용 후보|PASS / 미검증|2ec0e20d91debdb5b126a2f8ed361366db63cab7ad2d3dd4457f652f1387303a|
|p1/ui_ultimate_ready_v01.wav|0.300|-4.000001|현재 미사용|PASS / 미검증|3b3c00a5727289e98dd1f5edfeed7abacd2bac56d0330d7ad45d97fa63fc46bc|
|p1/sfx_ultimate_mg_v01.wav|0.380|-4.000001|현재 미사용|PASS / 미검증|b20ee8f5287a9169d9044d8eeed566a15abf70804268e3af70cead889cb170ef|
|p1/sfx_ultimate_cannon_v01.wav|0.430|-4.000001|현재 미사용|PASS / 미검증|7c526193acb045caae4e2b64ea04f8d841bb1672f19c44ed19f716ed1a5694c1|
|p1/sfx_ultimate_rocket_v01.wav|0.430|-4.000001|현재 미사용|PASS / 미검증|0b207808fed6dbecd3e63611906ba560be6df49b84de4b15ee65701432bc5a04|
|p1/ui_wave_start_v01.wav|0.360|-4.000001|재사용 후보|PASS / 미검증|7af77747e6cea5bbb3f42fff86894fda72c3a6bd77d52a3514ea0ce6b97f0f36|
|p1/ui_victory_v01.wav|2.200|-4.000001|재사용 후보|PASS / 미검증|1423d5921bc86bbc858bc4a34c5f2515dae2db0ca75171c942702161c8438da7|
|p1/ui_defeat_v01.wav|1.800|-4.000001|재사용 후보|PASS / 미검증|4e89db1259b52f29fb362bc55fdcdb67542ad1e60bf09ea0612a3dc863a52895|
|bgm/bgm_battle_v01.wav|64.000|-6.000000|재사용 후보|PASS / 미검증|07003d5413693a411393b0aa5983a32165505aa2a182f93ff0ae51732d420d98|
|bgm/bgm_boss_v01.wav|48.000|-6.000000|재사용 후보|PASS / 미검증|ee1bbcb34fb7e7caa1dd48fbbe838b4a30fccb80d6e0508dd0f0b08dba14c227|
|expansion/ui_promote_v01_a.wav|0.650|-4.000001|재사용 후보|PASS / 미검증|cfcd2bf5f6b22b90ab3922a79167b9eed22dee175d34bb2812a44a89d6e3757b|
|expansion/sfx_pin_fire_v01_a.wav|0.240|-4.000001|현재 미사용|PASS / 미검증|f4ffa279354ee6bbfd231af31d350af1e78d6fda0fdba8dc28d95214bbdbf7ee|
|expansion/sfx_pin_fire_v01_b.wav|0.240|-4.000001|현재 미사용|PASS / 미검증|8b567b79dff1ee09898cda88ba5c92f9eeea6995e5b2a95691d1f07bdcc9aa74|
|expansion/sfx_ultimate_pin_v01_a.wav|0.420|-4.000001|현재 미사용|PASS / 미검증|cf632e356673947c8bda32b8a3c1d498526279927daa0d4fbfcb426c06a80bf4|
|expansion/sfx_ash_ignite_v01_a.wav|0.270|-4.000001|재사용 후보|PASS / 미검증|ac7bd0137a00af167379bd22fd050c1b8519fda5ff18f1c45d652d6a4e4117f8|
|expansion/sfx_ash_ignite_v01_b.wav|0.270|-4.000001|현재 미사용|PASS / 미검증|d57b5889e9a44bfc2a943d0a95a11add67f8afeb0ebf9c0051210318a441d61c|
|expansion/sfx_ash_burn_loop_v01_a.wav|2.000|-6.000000|재사용 후보|PASS / 미검증|46098699824935a33415cc3e9977f8410849f55d3e8fc320578108beb49f6894|
|expansion/sfx_ultimate_ash_v01_a.wav|0.500|-4.000001|현재 미사용|PASS / 미검증|0db2952e1886199c526d78e3e69788a37e87470451c30b0f3a8e292c8930bc55|
|expansion/sfx_ember_pop_v01_a.wav|0.160|-4.000001|현재 미사용|PASS / 미검증|6d086f8b14c6641b671353d1a09bdfe3eaf87afdaf244622eee85c66445537d4|
|expansion/sfx_tori_fire_v01_a.wav|0.130|-4.000001|현재 미사용|PASS / 미검증|331119db71075a4bb5e02e71fd793452876cf91b158449f7ae87d2215dde93af|
|expansion/sfx_tori_fire_v01_b.wav|0.130|-4.000001|현재 미사용|PASS / 미검증|a7543ca1c76496b1f5c110b281e08d8dca084b8d7493e73138ec0d0c1b8a2461|
|expansion/sfx_tori_support_v01_a.wav|0.230|-4.000001|현재 미사용|PASS / 미검증|69e9562b8ef65d465b3f6ef46895afc7dc797cbc1bbcb0afde2c725a50adeb75|
|expansion/sfx_ultimate_tori_v01_a.wav|0.480|-4.000001|현재 미사용|PASS / 미검증|0da1c57784a373c0e70f1a818308b2c6f8390b1afa3b955a7e8bd56359aa668b|
## 반복 경계
loop=true인 아래 파일만 반복 후보로 검사. 구간은 프레임 인덱스 [시작,끝), seam은 채널별 첫/마지막 샘플 차이 절댓값의 최대(정규화 PCM). 수치가 작아도 가청 클릭·음악적 연결을 보장하지 않는다.
- bgm/bgm_battle_v01.wav: [0,3072000), 64.0초, seam=0.0004837513.
- bgm/bgm_boss_v01.wav: [0,2304000), 48.0초, seam=0.0008952618.
- expansion/sfx_ash_burn_loop_v01_a.wav: [0,96000), 2.0초, seam=0.0000000000.
## ZIP 인수 확인
3개 ZIP의 전체 CRC 검사 통과. 아래는 파일 자체의 해시이며 내부 WAV 해시와 구분한다.
- Nightroad_Audio_P0_v1.zip: 1739699 bytes, SHA256 8354971789719acb8bbc0b36e2054536f0f6189b22cb0f96bc5918817cb84a38.
- Nightroad_Audio_All_v1.zip: 34187780 bytes, SHA256 045855f14b28ec9126fd3dd5526abd0cb27e997a65dfefe255b7a3ecbcee31c3.
- Nightroad_Audio_v03.zip: 34716604 bytes, SHA256 1d2b63bad9053989be73724fcb5327b05f39e44262b43c45ef8bf2ea424d9432.
## 차단·다음 단계
직접 청취 가능한 입력/재생 결과를 이번 실행 환경에서 확보하지 못했다. 파일 끝 클릭, 고음 피로, 무기 구별, 누수 경고 식별은 판단하지 않았다. 기존 preview.html을 실제로 듣고 파일별 관측을 남길 청취 검수자가 필요하다. 청취 기록 확보 전 AU-01은 DONE으로 바꾸지 않는다. 별도 새 음원 제작 결정은 필요 없다.
마지막 완료 지점: 파일 46개 측정과 ZIP 무결성 검사. 독립적인 AU-02 의미 기준 인계표는 진행 가능하여 별도 결과에 저장한다.
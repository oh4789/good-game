# 카드 성장·승급 기회 분석 — 독립 계산 모델
작성일: 2026-10-02 (America/Chicago)
상태: 추첨 모델 계산 완료 / 전투 시뮬레이션·게임 실행 검수 아님

## 기준과 확정 구분
사용자 확정인 단일 진영·출전3·별도 영입·처치 카드3택1·약7분을 유지한다. 확률보완 정책은 신규 제안이다.
기존10-common-cards-party-growth-spec,11-cogwork-roster-promotion-build-framework,12-cogwork-54cards-18builds-catalog,13-party-recruitment-release-validation,15-three-builds-first-implementation-pack을 기준으로 한다.
작성 전 목록을 확인하고 새16-recruit-swap-build-guide-ux를 읽었다. 영웅별 카드/승급/충전 보존과 후반영입 무료전용카드 없음은 유지한다. 해당 화면의 “완성카드가 등장할 수 있음” 문구에 확률보완 채택 여부를 별도 표시해야 한다.

## 1. 계산 조건
조건별10,000회,각9번 선택. 기본3명 BBI/CAN/RKT. 첫선택비비단독,둘째비비+탄코,셋째부터3명 출전으로 고정한다. 실제 처치·누수·영입시간은 모델링하지 않는다. 총9회에 도달한 조건부 분석이다.
기초상한 비비2/2/1,탄코2/1/2,로코2/2/2. 공용4/4/4/2,교차사격은2명출전부터.
각영웅대표1갈래 또는전체3갈래,완성우선전용첫슬롯·나머지전용1·공용1.
목표는지정영웅의0번갈래. 선택원칙:
목표완성→목표핵심→목표기초→공용(G01,G02,G03,G04순)→다른영웅기초→다른완성→다른핵심→목표의원하지않는갈래.
같은등급은ID문자열순. 목표가안나오면공용을고르므로모든선택이주력투자는아니다.
'공용 우선 실험'은4/8/9번째에공용을다른우선순위보다앞에둔다. 나머지선택에서도목표부재시공용을고를수있어실제공용선택은3회를넘는다. 현실유저대표가아닌고정선택정책의스트레스시험이다.
시드별xorshift32,20261002+i×2654435761의하위32비트,i=1~10000. 정책마다동일시드목록을쓰되추첨호출수변경으로같은후보가보장되지않는다.

## 2. 기존안 결과
| 활성갈래/선택정책 | 목표 |3선택내|5선택내|7선택내|9선택내|평균공용선택 |
|---|---|---:|---:|---:|---:|---:|
|대표1/목표우선|비비|28.03%|56.39%|74.61%|85.48%|3.34|
|전체3/목표우선|비비|21.60%|46.88%|64.99%|77.56%|3.66|
|전체3/4·8·9공용우선|비비|21.60%|35.39%|57.01%|57.01%|4.95|
|전체3/4·8·9공용우선|탄코|0%|13.62%|39.35%|39.35%|5.90|

이는목표빌드완성률이며게임승률이아니다. 후반의높은공용우선때문에7→9완성률이늘지않는조건이있다.
“최소전용3회로성립”은“3번째레벨업에원하는빌드완성”이아니다. 카드풀확대가목표도달률을낮추는위험을확인했다.

## 3. 수정안 비교
A: 무료전체후보재추첨1회. 3번째이후,목표영웅기초를보유하고다음목표핵심/완성이안나온첫화면에사용. 공용우선회차에는쓰지않는다. 재추첨은같은풀/규칙으로3장을새로생성하고기존후보는버린다. 사용자가이보다다르게쓸수있으며결과를일반화하지않는다.
B: 목표설정영웅의다음핵심/완성카드가유효한데2화면연속안나오면다음화면전용둘째슬롯에그카드를넣는다. 자연등장해도미등장카운터0. 선택거절시카드는자동지급않음. 기초카드등장은보장하지않음.
| 조건 |기존9선택내|재추첨1회|목표기회보장 |
|---|---:|---:|---:|
|대표1/비비목표우선|85.48%|88.58%|100%|
|전체3/비비목표우선|77.56%|81.10%|100%|
|전체3/비비공용우선|57.01%|64.48%|57.01%|
|전체3/탄코공용우선|39.35%|49.22%|83.37%|

B의비비목표우선은5선택내100%였다. 첫선택에반드시비비기초를고르는모델,등장한목표를즉시고르는정책에한한결과다. 모든영웅·모든선택에서5회완성보장이라는뜻이아니다.
비비공용우선은B가개선하지못했다. 보장된기회를공용선택때거절할수있기때문이며결과를숨기지않는다.
추천은A/B동시도입이아닌B를별도시험하는것. 새유료재화·추가카드획득·확률공개없는자동지급은추가하지않는다.

## 4. 영입6회 정확 열거
6종풀,시작비비+처음2영입으로서로다른3명보유. 이후4회각6종균등,총6^4=1296가지모두열거. 첫두영입의정체는보유수/별통계에대칭이므로고정한다.
카드·교체·부활·환급추가뽑기는없다. 정확히6회영입조건이다.
| 지표 | 결과 |
|---|---:|
|최종평균보유영웅|4.5532명|
|2성이상 평균보유영웅|1.9491명|
|3성영웅이최소1명생김|5.0926%|
|3명을넘는보유(교체후보존재)|93.75%|
|최종3명/4명/5명/6명보유|81/525/582/108 경우|

마지막분포를1296으로나누면확률이다. 교체후보존재는실제교체율이아니다. 보유3명초과가항상좋은빌드선택이라는뜻도아니다.
출전3명의3성률과혼동하지않는다. 3성확률은대기영웅까지포함한다.
결론:1성도빌드완성가능규칙유지. 3성전제의보스체력을설정하지않는다. 후반교체의전용투자손실은16UX에명시하고실측으로판단한다.

## 5. 완료와 제한
완료:4정책조건각1만회×3추첨정책=12만회독립계산,영입1296경우정확열거.
미수행:적이동·피해·승률·플레이시간·사용자행동검증·실제게임코드수정·배포.
평가표본이많아도누락된전투조건을보완하지않는다. 실제9회선택에도달하지못하는런에는위완성률을적용하지않는다.
재현용JavaScript는아래첨부. 게임코드가아닌문서내계산모델이다.

### 기본 모델
```javascript

function rng(seed){let x=seed>>>0;return ()=>{x^=x<<13;x^=x>>>17;x^=x<<5;return (x>>>0)/4294967296;};}
function run(seed,branches,commonPlan,target){
 const rand=rng(seed), count={}, core=[-1,-1,-1], caps=[[2,2,1],[2,1,2],[2,2,2]], picks=[];
 let completed=0;
 function sample(a){return a[Math.floor(rand()*a.length)];}
 for(let level=1;level<=9;level++){
  const active=level===1?[0]:level===2?[0,1]:[0,1,2];
  let p=[],g=[];
  for(const h of active){
   for(let b=0;b<3;b++)if((count[h+'b'+b]||0)<caps[h][b])p.push(h+'b'+b);
   if([0,1,2].some(b=>count[h+'b'+b])){
    if(core[h]<0){for(let k=0;k<branches;k++)p.push(h+'k'+k);}
    else if(!count[h+'f'+core[h]])p.push(h+'f'+core[h]);
   }
  }
  for(let j=0;j<4;j++)if((j<3||active.length>1)&&(count['g'+j]||0)<(j===3?2:4))g.push('g'+j);
  const offered=[],finish=p.filter(x=>x[1]==='f');
  if(p.length){let x=sample(finish.length?finish:p);offered.push(x);p=p.filter(y=>y!==x);}
  if(p.length){let x=sample(p);offered.push(x);p=p.filter(y=>y!==x);}
  if(g.length){let x=sample(g);offered.push(x);g=g.filter(y=>y!==x);}
  while(offered.length<3&&p.length+g.length){let x=sample([...p,...g]);offered.push(x);p=p.filter(y=>y!==x);g=g.filter(y=>y!==x);}
  if(offered.length<3)throw Error('short pool');
  function rank(x){
   if(commonPlan&&[4,8,9].includes(level)&&x[0]==='g')return 0;
   if(x===target+'f0')return 1;
   if(x===target+'k0')return 2;
   if(x[0]===String(target)&&x[1]==='b')return 3;
   if(x[0]==='g')return 4+Number(x[1])/10;
   if(x[1]==='b')return 5;
   if(x[1]==='f')return 6;
   if(x[0]===String(target))return 99; // avoid locking unwanted target branch
   return 7;
  }
  offered.sort((a,b)=>rank(a)-rank(b)||a.localeCompare(b));
  const x=offered[0];count[x]=(count[x]||0)+1;picks.push(x);
  if(x[1]==='k')core[+x[0]]=+x[2];
  if(x===target+'f0')completed=level;
 }
 return {completed,commons:picks.filter(x=>x[0]==='g').length};
}
function experiment(branches,commonPlan,target,n=10000){
 let times=Array(10).fill(0),com=0;
 for(let i=1;i<=n;i++){const r=run(20261002+i*2654435761,branches,commonPlan,target);times[r.completed]++;com+=r.commons;}
 return {branches,commonPlan,target,n,completeBy:[3,5,7,9].map(k=>times.slice(1,k+1).reduce((a,b)=>a+b,0)/n),failure:times[0]/n,averageCommon:com/n};
}

```

### 재추첨 모델(독립 실행)
```javascript

function rng(seed){let x=seed>>>0;return ()=>{x^=x<<13;x^=x>>>17;x^=x<<5;return (x>>>0)/4294967296;};}
function run(seed,branches,commonPlan,target){
 const rand=rng(seed), count={}, core=[-1,-1,-1], caps=[[2,2,1],[2,1,2],[2,2,2]], picks=[];
 let completed=0,rerolled=false;
 function sample(a){return a[Math.floor(rand()*a.length)];}
 for(let level=1;level<=9;level++){
  const active=level===1?[0]:level===2?[0,1]:[0,1,2];
  let p=[],g=[];
  for(const h of active){
   for(let b=0;b<3;b++)if((count[h+'b'+b]||0)<caps[h][b])p.push(h+'b'+b);
   if([0,1,2].some(b=>count[h+'b'+b])){
    if(core[h]<0){for(let k=0;k<branches;k++)p.push(h+'k'+k);}
    else if(!count[h+'f'+core[h]])p.push(h+'f'+core[h]);
   }
  }
  for(let j=0;j<4;j++)if((j<3||active.length>1)&&(count['g'+j]||0)<(j===3?2:4))g.push('g'+j);
  const originalP=[...p],originalG=[...g];
 function draw(){p=[...originalP];g=[...originalG];
 const offered=[],finish=p.filter(x=>x[1]==='f');
  if(p.length){let x=sample(finish.length?finish:p);offered.push(x);p=p.filter(y=>y!==x);}
  if(p.length){let x=sample(p);offered.push(x);p=p.filter(y=>y!==x);}
  if(g.length){let x=sample(g);offered.push(x);g=g.filter(y=>y!==x);}
  while(offered.length<3&&p.length+g.length){let x=sample([...p,...g]);offered.push(x);p=p.filter(y=>y!==x);g=g.filter(y=>y!==x);}
  if(offered.length<3)throw Error('short pool');return offered;}
 let offered=draw();
 const needed=core[target]===0?target+'f0':[0,1,2].some(b=>count[target+'b'+b])?target+'k0':null;
 if(!rerolled&&level>=3&&active.includes(target)&&needed&&!count[needed]&&!offered.includes(needed)&&!(commonPlan&&[4,8,9].includes(level))){offered=draw();rerolled=true;}
  function rank(x){
   if(commonPlan&&[4,8,9].includes(level)&&x[0]==='g')return 0;
   if(x===target+'f0')return 1;
   if(x===target+'k0')return 2;
   if(x[0]===String(target)&&x[1]==='b')return 3;
   if(x[0]==='g')return 4+Number(x[1])/10;
   if(x[1]==='b')return 5;
   if(x[1]==='f')return 6;
   if(x[0]===String(target))return 99; // avoid locking unwanted target branch
   return 7;
  }
  offered.sort((a,b)=>rank(a)-rank(b)||a.localeCompare(b));
  const x=offered[0];count[x]=(count[x]||0)+1;picks.push(x);
  if(x[1]==='k')core[+x[0]]=+x[2];
  if(x===target+'f0')completed=level;
 }
 return {completed,commons:picks.filter(x=>x[0]==='g').length};
}
function experiment(branches,commonPlan,target,n=10000){
 let times=Array(10).fill(0),com=0;
 for(let i=1;i<=n;i++){const r=run(20261002+i*2654435761,branches,commonPlan,target);times[r.completed]++;com+=r.commons;}
 return {branches,commonPlan,target,n,completeBy:[3,5,7,9].map(k=>times.slice(1,k+1).reduce((a,b)=>a+b,0)/n),failure:times[0]/n,averageCommon:com/n};
}

```

### 목표기회 모델(독립 실행)
```javascript

function rng(seed){let x=seed>>>0;return ()=>{x^=x<<13;x^=x>>>17;x^=x<<5;return (x>>>0)/4294967296;};}
function run(seed,branches,commonPlan,target){
 const rand=rng(seed), count={}, core=[-1,-1,-1], caps=[[2,2,1],[2,1,2],[2,2,2]], picks=[];
 let completed=0,misses=0;
 function sample(a){return a[Math.floor(rand()*a.length)];}
 for(let level=1;level<=9;level++){
  const active=level===1?[0]:level===2?[0,1]:[0,1,2];
  let p=[],g=[];
  for(const h of active){
   for(let b=0;b<3;b++)if((count[h+'b'+b]||0)<caps[h][b])p.push(h+'b'+b);
   if([0,1,2].some(b=>count[h+'b'+b])){
    if(core[h]<0){for(let k=0;k<branches;k++)p.push(h+'k'+k);}
    else if(!count[h+'f'+core[h]])p.push(h+'f'+core[h]);
   }
  }
  for(let j=0;j<4;j++)if((j<3||active.length>1)&&(count['g'+j]||0)<(j===3?2:4))g.push('g'+j);
  const offered=[],finish=p.filter(x=>x[1]==='f');
  if(p.length){let x=sample(finish.length?finish:p);offered.push(x);p=p.filter(y=>y!==x);}
  if(p.length){let x=sample(p);offered.push(x);p=p.filter(y=>y!==x);}
  if(g.length){let x=sample(g);offered.push(x);g=g.filter(y=>y!==x);}
  while(offered.length<3&&p.length+g.length){let x=sample([...p,...g]);offered.push(x);p=p.filter(y=>y!==x);g=g.filter(y=>y!==x);}
  if(offered.length<3)throw Error('short pool');
  const desired=core[target]===0?target+'f0':[0,1,2].some(b=>count[target+'b'+b])&&core[target]<0?target+'k0':null;
 if(desired&&active.includes(target)&&!count[desired]){
  if(!offered.includes(desired)&&misses>=2){const index=offered.findIndex((x,i)=>i===1&&x[0]!=='g');if(index>=0)offered[index]=desired;}
  misses=offered.includes(desired)?0:misses+1;
 }else misses=0;
 function rank(x){
   if(commonPlan&&[4,8,9].includes(level)&&x[0]==='g')return 0;
   if(x===target+'f0')return 1;
   if(x===target+'k0')return 2;
   if(x[0]===String(target)&&x[1]==='b')return 3;
   if(x[0]==='g')return 4+Number(x[1])/10;
   if(x[1]==='b')return 5;
   if(x[1]==='f')return 6;
   if(x[0]===String(target))return 99; // avoid locking unwanted target branch
   return 7;
  }
  offered.sort((a,b)=>rank(a)-rank(b)||a.localeCompare(b));
  const x=offered[0];count[x]=(count[x]||0)+1;picks.push(x);
  if(x[1]==='k')core[+x[0]]=+x[2];
  if(x===target+'f0')completed=level;
 }
 return {completed,commons:picks.filter(x=>x[0]==='g').length};
}
function experiment(branches,commonPlan,target,n=10000){
 let times=Array(10).fill(0),com=0;
 for(let i=1;i<=n;i++){const r=run(20261002+i*2654435761,branches,commonPlan,target);times[r.completed]++;com+=r.commons;}
 return {branches,commonPlan,target,n,completeBy:[3,5,7,9].map(k=>times.slice(1,k+1).reduce((a,b)=>a+b,0)/n),failure:times[0]/n,averageCommon:com/n};
}

```

각코드끝에서 다음을실행한다:
```javascript
console.log([experiment(1,false,0),experiment(3,false,0),experiment(3,true,0),experiment(3,true,1)]);
```

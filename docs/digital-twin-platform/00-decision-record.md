# 00. AICHEMIST 디지털 트윈 플랫폼 최종 결정 기록 (Decision Record)

**문서 상태:** 최종 결정본 v1.1(범용성 보완 + 문서 간 정합 Errata 반영, §16) · 기준일 2026-10-06 · 작성: AICHEMIST 전략·기술팀 · 상위 문서: [README](README.md)
**적용 범위:** 본 마스터플랜 문서 12종(01–12), README, 부록 A·B와 이를 바탕으로 만드는 사업계획서·IR 덱·정부과제 제안서·가격표·KPI 대시보드의 단일 기준(Single Source of Truth). 문서 사이에 값이 다르면 **§16 Errata → 본문 → 부속 문서** 순으로 우선한다.
**기간 표기:** M0 = 2026년 10월(결정 월), **M1 = 2026년 11월**. P0 = M1–M4(2026.11–2027.02), P1 = M5–M12(2027.03–2027.10), P2 = M13–M24(2027.11–2028.10), P3 = M25–M36(2028.11–2029.10). 일 단위 기준일은 D0 = 2026-10-16(금, CEO 승인)이다(§16 #10).
**환율:** 1 USD = ₩1,400 [A]
**표기 규칙**
- **[A]**: 본 문서의 계획 가정. 실적 확인 전까지 목표치로만 사용한다.
- **[U]**: 리서치에서 1차 출처로 확인하지 못한 주장. 돈을 쓰거나 대외 문서에 넣기 전에 §15의 검증을 거친다.
- 태그가 없는 사실은 리서치 다이제스트에서 GitHub, PyPI, SkyPilot 가격 카탈로그로 확인된 것이다. Fact-check가 수정한 항목은 수정된 값을 쓴다.
- 금액 단위: ₩억 = 1억 원. 모든 매출 수치는 **예측이 아닌 목표**다.
- **표준 용어:** '피지컬 AI'로 쓰고 문서마다 첫 출현에만 'Physical AI'를 병기한다. 'sim-to-real(시뮬레이션-실제 전이)'을 일반 용어로 쓴다. 'sim2sim'·'sim2real'은 기술 게이트 이름에만, 'Sim2Real Gap Scorecard'는 제품 고유명사로만 쓴다. 'K-Physical AI Arena'는 고유명사이므로 그대로 둔다.
- **용어:** 허용형 라이선스, 결정론적 재현, sim2sim 게이트, 베이크오프, 릴리스 트레인, 업그레이드 세금, 측정권, 페어드 코퍼스 등은 [README §9 용어집](README.md)에서 설명한다.

**근거 문서:** 제안 A(NVIDIA-Accelerated Speed), 제안 B(Sovereign Open Core), 제안 C(Outcome-led Data & Evaluation Factory), 심사위원단 3종(CTO, 투자자, 고객·정부) 평가([research/strategy-panel](research/strategy-panel/)), 리서치 다이제스트([research/research-digest-en.md](research/research-digest-en.md), [research/research-options-en.md](research/research-options-en.md)), 출처·검증([부록 B](appendix-b-sources-verification.md))


> **v1.1 보완(CEO 요구사항 정합): '기술적 범용성'과 '상업적 집중'을 분리한다.**
> CEO 요구는 "대상은 로봇, 자동차 등 어떤 것도 가능"이다. 본 문서의 Wave 1/2/3은 **상업적 집중 순서**, 즉 어디서 먼저 돈을 버는가를 정한 것이다.
> **기술적 범용성**은 처음부터 아키텍처로 보장한다. OpenUSD 단일 장면, 엔진 중립 Sim Kernel API, Domain Pack(자산·물리 프로파일·센서 리그·표준 커넥터·학습 템플릿·평가지표·인증 기준)이 그 장치다.
> **Capability Readiness**(기술 준비 시점)는 다음과 같다.
> - 로봇 조작: P0–P1. P0 RL 템플릿 3종(팔 도달·큐브 들기, 빈 피킹(한국 SKU), 디팔레타이징)은 모두 조작 팩이다.
> - AMR·공장/물류 셀: M9–M18
> - 휴머노이드·사족·덱스터러스 템플릿: M6–M12(P1에 처음 들어간다: G1 속도 추종·모션 추적, 사족 속도 추종, 손안 재배치(상태 기반)).¹
> - **차량 Mobility Pack α: M18–M24.** 야드·저속 차량 동역학과 도로 시나리오 재생이 범위다. Chrono::Vehicle 어댑터(Zone T/S의 차량 동역학), PhysX Vehicle2(Zone F 전용, Isaac Lab 경유), OpenDRIVE/OpenSCENARIO import, 카메라·라이다 센서 리그, FMI 3.0 브리지로 구성한다.
> - 드론 PX4 SITL 기본 템플릿: M20–M24(P2 RL 템플릿 1종으로 센다. 상업화는 P3 국방 에디션)
> - 선박·해양과 오프로드 UGV: P3
>
> 도로 AV는 시뮬레이터로 정면 경쟁하지 않는다. OpenSCENARIO/OSI/FMI 브리지와 MORAI 파트너십으로 '연결'한다. 이 보완은 기존 인원·예산(부록 고정값) 범위 안의 일정 조정이다. WS1-M 1명(차량·해양 동역학 엔지니어, 서치 M16·착석 M18)과 WS3가 지원한다. 템플릿 ID의 마스터는 [06 §6.2](06-usability-and-agent.md), 팩별 배분의 마스터는 [08 §7.1](08-domain-packs.md)이다. 상세는 [08 도메인 팩](08-domain-packs.md).
>
> ¹ P2 상업화는 휴머노이드·덱스터러스 핸드에만 해당한다. 사족은 경쟁 지형 거부권(1점, §5.1)에 따라 템플릿과 Crucible 평가로만 수익화한다.

---

## 0. 결정 요약

**플랫폼 한 줄 정의**
> **CEN Athanor(아타노르)는 현실을 측정해 AI가 학습할 수 있는 디지털 트윈으로 만들고, 그 트윈에서 만든 학습 데이터·로봇 기술·평가 결과가 실제 현장에서 통한다는 것을 수치(sim-to-real 점수)로 인증해 공급하는 범용 피지컬 AI(Physical AI) 디지털 트윈 플랫폼이다.**

**CEO 질문에 대한 답(1분 요약)**

| 질문 | 답 | 증명 KPI(M12 → M24/M36) | 상세 |
|---|---|---|---|
| **어떤 엔진을 쓰나?** | 엔진 하나가 아니라 역할별 포트폴리오를 쓴다. 로봇 학습은 Newton(GPU 고속), 인증·재현은 MuJoCo(정밀 CPU), 정밀 손 조작은 NVIDIA Isaac Lab·PhysX(사내 전용), 접촉 정답 검증은 Drake, 차량·지형은 Chrono, 선박은 Chrono FSI와 자체 클린룸 Fossen 6-DOF, 드론은 PX4 SITL + Gazebo가 맡는다. 화면과 센서는 R0 웹 렌더러(고객 화면), R1 Newton Warp(고객 SDG·비전 RL), R2 3DGUT(신경 렌더), R3 NVIDIA RTX(사내)의 4티어로 그린다. | 베이크오프 결정 메모(2027-01 첫 주)로 작업 유형별 기본 백엔드 확정 | §2, [03 §7](03-engine-selection-build-vs-buy.md) |
| **직접 만드나?** | 물리 엔진과 렌더러는 만들지 않는다. 자체 개발에는 ₩400–600억과 3–5년이 들고, 이는 24개월 예산 ₩122억의 3–5배다. 대신 엔진을 갈아끼우는 표준 인터페이스(Sim Kernel API), 현실과의 오차를 재는 측정·인증 체계, 한국어 에이전트를 직접 만든다(엔지니어링의 약 60%). | 적합성 스위트 통과 4×8 → 6×15 | §3 |
| **자동차 등 무엇이든 되나?** | 된다. 장면 표준(OpenUSD) 하나와 엔진 교체 인터페이스 위에 대상별 도메인 팩을 꽂는다. 준비 시점은 로봇 조작 M12, AMR·공장 M18, 차량 M24(야드·저속 차량 동역학과 도로 시나리오 재생), 드론 M24, 선박 M36이다. 도로 자율주행 시뮬레이터 시장과는 정면으로 경쟁하지 않고 표준과 MORAI로 연결한다. | 대상별 Domain Pack과 적합성 장면 추가(C05 바퀴 차량은 P0부터) | 상단 v1.1 보완, §5.5, [08](08-domain-packs.md) |
| **물리는 강력한가?** | 작업 유형별로 최적 백엔드를 고르고, 백엔드끼리 결과를 대조하며, 실측으로 보정하고, 인증은 결정론 경로로만 낸다. | 궤적 오차 ADE ≤2 cm → ≤1 cm(M36), 인증 시험 결정론 재현 100% | §4.1 |
| **현실과 얼마나 비슷한가?** | 재질·신경 재구성·실측 센서·생성형 증강의 4계층으로 맞추고, 모든 납품물에 Sim2Real Gap Scorecard와 Bronze/Silver/Gold 인증을 붙인다. | 합성 전용 mAP 비율 ≥0.90 → ≥0.95, 정책 sim-to-real 갭 ≤15%p → ≤10%p | §4.2 |
| **쓰기 편한가?** | 한국어로 결과물을 주문하거나(Outcome Console), 설치 없이 브라우저에서 직접 만든다(Athanor Studio). 한국어 에이전트의 모든 변경은 검증 게이트와 사람 승인을 거친다. | 첫 시뮬레이션 ≤10분(베타) → ≤5분, 영상 → 피킹 스킬 24시간 → 당일(셀프서브) | §4.3 |
| **모델 학습이 되나?** | RL·모방학습·VLA·인식 학습을 하나의 라인에 내장하고, sim2sim 게이트와 Crucible 평가를 거쳐 Jetson으로 배포한다. | 템플릿(RL/IL·VLA/인식) 8/3/3 → 15/6/5, 실셀 이전 정책 누적 8 → 30, 수출 전 sim2sim 게이트(Tier 1) 100% | §4.4 |

**10대 결정 헤드라인**
1. **시뮬레이터 좌석이 아니라 '측정된 증거가 붙은 결과물'을 판다.** 인증 트윈·데이터·스킬·평가를 팔고, 자동화와 수익성이 증명된 생산 라인부터 셀프서브 제품(Athanor Studio)으로 연다. 세 제안서의 검토 경위는 §1.3에 있다.
2. **물리 엔진과 렌더러는 직접 만들지 않는다.** 자체 엔진은 150–300 engineer-year, ₩400–600억, MVP까지 30–48개월 이상이 든다. 대신 엔진 중립 **Sim Kernel API**, 적합성(conformance) 스위트, Run Manifest, 인증 체계를 소유한다(§3).
3. **엔진 스택은 Newton 1.6.x(MJWarp 솔버, Apache-2.0)와 MuJoCo 3.15 CPU(결정론적 재현·인증)가 중심이다.** Newton 버전은 Isaac Lab 3.x GA 핀으로 통일하고(§7.1, 2026-10 최신 1.6.1), 접촉 집약 조작은 사내 팩토리의 **Isaac Lab 3.x + PhysX 5.x**, 오프라인 접촉 기준은 Drake, 차량·지형·해양은 Chrono 10이 맡는다. Genesis는 관찰만 한다(§2).
4. **라이선스 원칙: NVIDIA 독점 소프트웨어는 사내에서만 쓴다.** NVIDIA의 독점 실행 소프트웨어(Isaac Sim, Omniverse Kit, RTX 렌더러 등)는 NVIDIA의 서면 허가를 받기 전까지 사내 생산 설비(Zone F)에서 데이터와 모델을 만드는 데에만 쓴다. 고객이 직접 쓰는 클라우드(Zone T)와 고객 사이트 설치본(Zone S)은 상업적 재배포가 자유로운 오픈소스(허용형과 의무 이행이 가능한 약한 카피레프트)로만 구성한다. 허가 전에 NVIDIA 소프트웨어를 고객에게 호스팅하는 방식은 하지 않는다. 대상 패키지 목록과 구성 규칙은 §6.2에 있다.
5. **비치헤드는 18개월간 "물체가 많은 조작(object-rich manipulation)" 하나다.** 물류 피킹·디팔레타이징, 공장 셀 조립·검사, 조선소 작업장 핸들링이 여기에 들어간다. 휴머노이드·양팔 VLA 데이터와 Crucible 평가 아레나는 M12부터 연다. 조선·해양 인식(M25 트리거 판정 개시)과 국방 에어갭(M27부터)은 트리거 조건부다. 기준안의 2028년 말 ARR 목표는 ₩20억이므로 M25에 ARR ₩30억 트리거는 충족되지 않는 것이 기본 경로이며, M25 착수는 확정 ₩5억 이상의 앵커 계약에 달려 있다(§5.4). AV 시뮬레이터 시장에는 정면으로 들어가지 않고 MORAI·표준(OpenSCENARIO·OSI·FMI 3.0)으로 연결하며, 차량 트윈 기술(Mobility Pack α: 야드·저속 차량 동역학과 도로 시나리오 재생)은 M18–M24에 준비한다.
6. **첫 매출은 산출물만으로 만든다.** 기존 CEN SDG 고객과 데이터셋 계약(mAP 인수 조건 포함)을 M4까지 맺고, 바우처 매출은 M5–M8부터 잡는다. 12주 고정가 **Cell-to-Policy PoC**(₩1.5–2.5억, 선금 30%, 인수 기준과 책임 상한 명시)는 M5부터 판다.
7. **24개월 예산은 기준안 ₩122억**(보수안 ₩99억, 공격안 ₩159억)이고, 이번 분기에 CEO가 실제로 결정할 금액은 P0 ₩11.2억이다. 인력은 16(M4) → 26(M12) → 36(M24) → 48(M36)명이며, 한국 시니어 채용 지연 3–6개월을 인건비(564 head-month)에 반영했다.
8. **세 개의 하드 게이트로 자본을 단계 투입한다.** G1(M11, 심의 2027-09-24)을 통과해야 26명을 넘겨 채용한다. 핵심 조건은 유료 결과물 고객 3곳 이상(양산 계약 1곳 이상), NVIDIA 서면 조건 또는 허용형 전용 경로 확정, 라인 총마진(완전원가 기준) 50% 이상, 측정권 고객 2곳 이상, Arena 공동서명 기관 MOU다(7개 조건 전체는 §7.2). G2(M18)는 첫 온프렘 설치와 반복매출 30%, G3(M24)는 Series B와 P3 확장을 판정한다. G1을 통과하지 못하면 보수안(₩99억)으로 자동 전환한다.
9. **자금 조달:** Series A ₩80억은 M5 전환 조건부 브리지 ₩20억 + M10 1차 클로징 ₩30억 + M12 2차 클로징 ₩30억(G1 연동)으로 받는다. 증빙 KPI는 코퍼스·인증서·총마진이고, Series B ₩250억은 M25–M28에 목표한다(§9.4). 정부 보조금은 업사이드로만 잡고 바우처는 '정부재원 매출'로 따로 보고한다. 매출 목표는 2027년 ₩15억, 2028년 ₩45억, 2029년 ₩110억이다.
10. **해자는 감사 가능한 지표로 관리한다.** 페어드 실측/시뮬 코퍼스, Silver/Gold 인증 자산, 제3자 공동서명 K-Physical AI Arena, 엔지니어 시간당 결과물 학습곡선을 분기 KPI로 공개한다. USD 100M ARR 경로는 한국 상한(약 USD 20–30M [U])을 넘어 **글로벌 로봇 파운데이션모델·휴머노이드 기업 대상 데이터·평가 공급**(M12–M15 착수)에서 나온다.

**이번 달 CEO 승인 요청 7건:** ① P0 ₩11.2억 집행, ② Sim Architect(CTO 트랙)와 Head of Fidelity & Evaluation 동시 서치 개시, ③ NVIDIA Korea에 서면 조건 요청서 발송(D5 = 2026-10-23, §14.2 체크리스트), ④ Wave-1 앵커 3곳(로봇 OEM·조선 로보틱스·물류/AI팩토리)과 첫 데이터셋 고객 지정, ⑤ 6–8주 엔진 베이크오프 착수(W1 = 2026-11-02, §14.3), ⑥ Series A 전환 조건부 브리지(₩20억, M5) 구조 협의 개시와 기존 가용 현금 ₩15억 확인(CFO, M1 첫 주. 미달 시 브리지를 M3로 앞당김), ⑦ G1 미통과 시 보수안 자동 전환 규칙과 중단·축소 기준([09 §3.7a](09-roadmap-organization-budget.md))의 이사회 사전 결의.

---

## 1. 플랫폼 정의와 포지셔닝

### 1.1 무엇인가
- **학습 가능한 트윈 플랫폼**이다. 로봇·차량·드론·선박·공장을 OpenUSD 장면 하나로 표현하고, 그 장면에서 RL·IL·VLA·인식 모델을 학습·평가한다. 엔진 중립 Sim Kernel 위에서 여러 물리·렌더 백엔드를 작업 유형별로 고른다.
- **결과물 팩토리이자 셀프서브 스튜디오**다. 고객은 Outcome Console에서 한국어로 결과물을 주문할 수 있고(Done-for-you), Athanor Studio에서 직접 만들 수도 있다(Self-serve). 두 경로는 같은 생산 라인과 같은 인증 체계를 쓴다.
- **인증 발행자**다. 모든 자산·데이터셋·정책에 Sim2Real Gap Scorecard와 Bronze/Silver/Gold 인증서(`aic:TwinCertificate` USD 스키마 + JSON 사이드카)를 붙인다. 연금술의 은유대로 '미검증 자산(납)'을 '실측 검증 자산(금)'으로 변환하는 과정 자체가 상품이다.
- **시뮬레이션 트윈이 기본, 라이브 트윈은 측정 도구**다. 라이브 트윈은 인수 모니터링, 현장 실패 마이닝, 트윈 충실도 드리프트 측정에 쓴다.
- **CEN의 확장**이다. 기존 구독·토큰·마켓플레이스, GPU 클라우드 워크스페이스, NeRF 기반 2D→3D, LLM 텍스트 명령 인터페이스를 그대로 수익 모델과 UX의 뼈대로 쓴다.

### 1.2 무엇이 아닌가
- **새 물리 엔진이나 렌더러가 아니다.** Newton·MuJoCo·PhysX·Chrono·Drake·RTX·3DGUT를 통합한다(§3).
- **IIoT·PLM 운영 트윈의 대체재가 아니다.** Siemens·AVEVA·Dassault 트윈과는 OPC UA·USD로 연결한다. 마케팅 메시지는 "기존 PLM 트윈을 위한 AI 학습 레이어"다.
- **도로 자율주행용 HIL·인증 도구 시장에서는 정면으로 경쟁하지 않는다. 차량 트윈 자체는 만든다.** 차량 Mobility Pack α(M18–M24)는 야드·저속 차량의 동역학(Chrono::Vehicle), 도로 시나리오 재생(OpenDRIVE·OpenSCENARIO), 카메라·라이다 리그, 고객이 보유한 CarSim·CarMaker 모델 연결(FMI 3.0)을 제공한다. 승용차 ADAS·자율주행 시뮬레이터는 dSPACE·IPG·Applied Intuition·MORAI의 영역이므로 표준으로 연결하고, 우리는 한국 도로 인식 데이터와 시뮬레이션 신뢰성 증거를 판다(선택지 비교는 §5.5).
- **NVIDIA 리셀러나 SI가 아니다.** NVIDIA와는 공동 판매(co-sell)하되, 가치는 측정·인증·데이터·한국 현장 콘텐츠에 둔다.
- **좌석 단위 시뮬레이터 라이선스 사업이 아니다.** 뷰어·리뷰어 좌석은 무료다. 컴퓨트는 원가 근처로 팔고, 가치는 결과물과 인증서에서 받는다.
- **범용 월드모델 회사가 아니다.** Cosmos 같은 월드모델은 외형 증강과 정책 사전 선별에만 쓰고, 물리·라벨·센서는 시뮬레이터가 책임진다.

### 1.3 포지셔닝 문장
- **투자자용:** *"NVIDIA는 시뮬레이터를 무료로 준다. AICHEMIST는 그 시뮬레이터에서 나오는 '현실에서 작동한다는 증거'(측정된 sim-to-real 점수가 붙은 트윈·데이터·스킬)를 팔고, 한국 로봇이 채점받는 아레나를 운영한다."*
- **고객용:** *"휴대폰 영상 한 편에서 인증된 트윈과 검증된 피킹 스킬까지. 인수 기준은 계약서에 숫자로 쓴다."*
- **정부 평가위원용:** *"TRL 4→7, 제3자 시험성적서로 검증 가능한 sim-to-real 지표, 국산 피지컬 AI 데이터·평가 인프라."*

**검토 경위(세 제안서 비교)**
- 이 결정은 세 제안서를 CTO·투자자·고객·정부 심사단이 각각 평가한 결과다. 세 심사단 모두 C안을 1위로 꼽았다.

| 제안 | 포지셔닝 | 심사 점수(CTO / 투자자 / 고객·정부) | 최종안에 남긴 것 |
|---|---|---|---|
| A. NVIDIA-Accelerated Speed | NVIDIA 스택의 한국 라스트마일 딜리버리 파트너 | 6.22 / 5.76 / 5.88 | **시장 진입 속도:** 12주 고정가 PoC, 하드 게이트, NVIDIA co-sell. '약관 전 호스팅 베타'는 폐기 |
| B. Sovereign Open Core | 라이선스가 깨끗한 소버린 피지컬 AI 코어 | 6.04 / 5.60 / 5.95 | **라이선스 섀시:** 3구역 원칙, 서명 SBOM, Sovereign·Air-gap 에디션 |
| **C. Outcome-led Data & Evaluation Factory** | 측정된 sim-to-real 점수가 붙은 결과물과 중립 평가 | **6.74 / 6.62 / 7.28** | **전략 골격 전체.** 약점(서비스화, 결과물 책임, 아레나 이해상충)은 생산화 게이트·책임 상한·공동서명 헌장으로 통제 |

- 엔진 선택은 세 안이 거의 같았다. 승부는 사업모델에서 갈렸다. 상세 비교는 [01 §3.4](01-vision-positioning.md)에 있다.

### 1.4 경쟁 구도 요약

| 경쟁자 | 그들의 수 | 우리의 대응 |
|---|---|---|
| NVIDIA | 엔진·Cosmos·GR00T·usd-content-agents 무료 배포, GPU·NVAIE로 수익 | 무료 공개 하나하나가 우리 원가를 낮춘다(P1 45일·P2 이후 30일 안에 사이드 브랜치 검증 완료 후보로 만들고, 프로덕션 반영은 다음 릴리스 트레인). 측정된 한국 콘텐츠와 중립 인증은 NVIDIA가 팔지 않는다. Inception·co-sell로 협력한다. 관리형 Isaac 클라우드가 한국에 출시되면 전략을 재검토한다(§12). |
| 재벌 내재화 | 그룹 IT 계열사가 Omniverse 트윈을 구축 | 재벌은 자사나 경쟁사를 스스로 인증할 수 없다. 공급망 1·2차 협력사는 내재화 역량이 없다. SI 계열사를 리셀러로 쓰고, Forge·Kernel·인증 IP는 PoC 이후에도 라이선스로 유지한다(계약 조항). |
| MORAI | AV·UAM·해양 시나리오, 정부 네트워크 | AV는 파트너로 협력한다. 해양에서는 도구가 아니라 데이터·평가를 판다. |
| Lightwheel | SimReady 자산(비상업 무료), LW-BenchHub 268개 과제(sim 전용) | 상업 라이선스, 실측 물리, 한국 SKU, 실셀 평가로 차별화한다. 해외 리셀러 후보이기도 하다. 지역 거점은 [U]다. |
| Applied Intuition | AV·국방 툴체인(가치 USD 15B, ARR 약 USD 830M 추정 [U]) | 정면 경쟁하지 않는다. 한국 조작·휴머노이드 영역에서는 존재감이 없다. |
| Genesis AI | 오픈 엔진 + 자체 모델(GENE-26.5) | 데이터·평가의 잠재 고객으로 본다. Genesis World는 비CUDA 헤지로 관찰만 한다. |
| CyLab·E8·중국 데이터 팩토리 | 인식 데이터, 도시 트윈, 저가 자산 | 물리·정책·측정된 전이를 더한다. 국방·재벌 고객에게는 신뢰를 앞세운다. |

### 1.5 명칭 후보와 추천

| 후보 | 연금술 의미 | CEN 브랜드 적합성 | 충돌·리스크 |
|---|---|---|---|
| **Athanor (아타노르)** ★추천 | 연금술사의 자급식 화로. 장기 연성 작업 동안 일정한 열을 유지한다 | '항상 켜진 팩토리'와 '통제된 변환'이라는 CEN 철학에 정확히 맞는다. Forge, Crucible, Gold 등급과 한 계열로 묶인다 | 로보틱스·시뮬레이션 분야의 주요 충돌은 확인되지 않았다. 상표 검색은 [U] |
| Crucible (크루서블) | 금속을 시험·정련하는 도가니 | 평가·인증 라인 이름으로 탁월하다 | 일반명사라 등록상표로서 식별력이 약하다. 기존 SW 제품명과 겹칠 가능성이 있다 [U] |
| Aludel (알루델) | 승화(昇華)용 용기 | 데이터 정제 이미지 | 인지도가 낮아 발음·의미 설명이 필요하다 |
| Azoth (아조트) | 만물의 용매, 변환의 매개 | '무엇이든 트윈으로'라는 범용성 | 게임 아이템명 등과 겹칠 가능성 [U] |
| Lapis (라피스) | 현자의 돌(Lapis philosophorum) | 최종 결과물(금) 은유 | 오픈소스 프레임워크명과 겹칠 가능성 [U] |

- **제외한 명칭:** Genesis(Genesis 엔진과 충돌), Alembic(VFX 표준 파일 포맷 Alembic과 충돌. 3D 파이프라인에서 혼동이 불가피하다), Opus(Opus 오디오 코덱 등 기존 소프트웨어 제품명과 충돌), Elixir(프로그래밍 언어와 충돌).
- **추천:** 플랫폼명은 **CEN Athanor**로 한다. 하위 브랜드 체계는 아래와 같다(후속 문서 전체에 동일하게 사용).
  - **Athanor Forge**: Real2Sim 자산 변환(CEN NeRF 파이프라인의 후속)
  - **Athanor Data / Athanor Skill**: 데이터셋 라인, 정책 학습 라인
  - **Athanor Crucible**: 평가·인증 라인. K-Physical AI Arena를 운영한다.
  - **Athanor Studio**: 셀프서브 작업 환경(CEN 워크스페이스 내부)
  - **Athanor Live**: 라이브 트윈과 fork-from-live
  - **에디션**: Athanor Cloud(SaaS), Athanor Sovereign(온프렘·국내 CSP), Athanor Air-gap(국방)
  - **인증 등급**: Bronze(VLM 추정), Silver(영상 기반 식별), Gold(랩 실측)
- 상표 출원(KIPRIS·USPTO·EUIPO 검색 후)은 M2까지 끝낸다.

---

## 2. 엔진 최종 선정표

**선정 원칙**
- 팩토리를 빠르고, 측정 가능하고, 재현 가능하게 만드는 것을 고른다.
- 테넌트에게 노출되는 경로는 처음부터 라이선스가 깨끗해야 한다.
- 버전은 릴리스 트레인 단위로 고정한다(§7.1). 벤더 처리량 수치(MJWarp 나이틀리, Genesis 43M FPS, 252배/475배 등)는 의사결정에 쓰지 않고, 사내 베이크오프 수치(steps/s/$, 보상 도달 시간)로 바꾼다.
- **사본 관리:** 이 표는 역할·라이선스·구역 판정의 정본이다. 버전 문자열, 구역 열, 재결정 트리거는 [03 §7](03-engine-selection-build-vs-buy.md)과 [03 §12.3](03-engine-selection-build-vs-buy.md)(Train 1 호환성 매트릭스)이 운영 정본이다. 버전이 바뀌면 03을 먼저 갱신하고, 이 표는 분기 Errata(§16)로 맞춘다. 요약본은 [README §2](README.md), 판정 등급만 [부록 A](appendix-a-technology-catalog.md)에 싣는다.

**SaaS 호스팅 상태 범례**
- **OK**: 허용형 라이선스(또는 의무 이행이 가능한 약한 카피레프트)로, 멀티테넌트 SaaS·온프렘에 탑재할 수 있다.
- **조건부(V7 등)**: 커스텀 사용 제한 라이선스다. 표시된 검증(§15)을 통과한 범위에서만 쓴다.
- **BYOL**: 벤더·고객 라이선스다. 고객이 자기 라이선스로 운영하는 환경에서만 연동하며 'OK' 대상이 아니다.
- **NVIDIA 서면확인 필요**: 독점 런타임이다. 내부 팩토리에서 산출물을 만드는 데에만 쓴다. 산출물 면제 자체도 [U]다.
- **NO**: 사용·탑재 금지, 또는 현 단계 보류.

| # | 레이어 | 1차(Primary) | 2차·폴백 | 버전 (2026-10) | 라이선스 | SaaS 호스팅 | 선정 근거 |
|---|---|---|---|---|---|---|---|
| 1 | 로봇 물리: 보행·전신·학습 처리량 | **Newton 1.6.x**, MJWarp 솔버 기본 | MuJoCo 3.15 CPU(레퍼런스), mjlab 1.6.0(MJWarp 3.11 고정 별도 이미지) | 버전은 Isaac Lab 3.x GA 핀으로 통일(§7.1). 2026-10 최신 Newton 1.6.1(2026-10-05. 1.0.0은 2026-03-10). MJWarp 3.15(PyPI상 Alpha). 최신 Warp 1.18 휠은 Turing(sm_75) 이상 GPU와 R580 이상 드라이버(CUDA 13) 필요 | Apache-2.0 | **OK** | Linux Foundation 거버넌스, 처리량 최상위, Isaac Lab 3.x Kit-less 백엔드. 단점: float32, GPU에서 비결정적, 미분 불가, 단일 메커니즘 약 60 DoF 이상에서 약함 |
| 2 | 접촉 집약 조작: 삽입, SDF, 촉각(팩토리) | **Isaac Lab 3.x + PhysX 5.x**(Isaac Sim 6.1 번들 버전 [U], 공개 SDK 최신 5.11. Isaac Sim 6.1·Kit) | 테넌트용: Newton SDF + hydroelastic. 조건부(P2): PhysX SDK 소스 빌드 어댑터 | Isaac Lab 3.0.0-EA(2026-09-16, GA는 2026년 10월 말 목표). Isaac Sim 6.1.0(2026-09-10). 공개 PhysX SDK 5.11(Isaac Sim 6.1 번들 PhysX 빌드는 [U]) | Isaac Lab 소스 BSD-3(mimic은 Apache-2.0). **Isaac Sim·Kit 런타임과 isaacsim/isaaclab PyPI 휠은 NVIDIA 독점.** PhysX SDK 코어는 Apache-2.0(저장소 루트는 BSD-3) | **NVIDIA 서면확인 필요**(팩토리 산출물 전용) | 가장 성숙한 조작 스택(TacSL, Mimic, Teleop, Arena). Isaac Lab의 Kit-less Newton 백엔드는 아직 beta이고 검증된 환경이 제한적이다 |
| 3 | 폐루프 메커니즘 | Newton Kamino | MuJoCo equality 제약 | Kamino는 Newton에서 experimental(Isaac Lab은 beta로 표기) | Apache-2.0 | OK | 링크 기구 그리퍼·클로즈드 체인 |
| 4 | 변형체·케이블·입상체 | Newton VBD / Style3D / ImplicitMPM | MuJoCo 3.15 flex(Stable Neo-Hookean 3.15·IPC 접촉 3.14 모두 실험적). Genesis IPC(관찰) | MuJoCo 3.15.0(2026-10-05) | Apache-2.0 | OK | 물류 폴리백·케이블·호스. 어떤 엔진도 결정론을 보장하지 않으므로 측정 전에는 성능을 보증하지 않는다 |
| 5 | 오프라인 접촉 골드 스탠다드 | **Drake** | — | v1.57.0(2026-09-10) | 소스 BSD-3. PyPI 휠 분류는 'BSD and Other/Proprietary'(번들된 서드파티 솔버에 별도 약관) | Zone F 내부 검증 OK. Zone S 번들은 독점 솔버를 제외한 소스 빌드만(V2 법률 의견 후) | Hydroelastic·SAP 접촉 정밀도 최고. CPU 전용이라 RL 규모로는 쓰지 않는다 |
| 6 | 차량·지형·해양 | **Chrono 10.0**(Vehicle, SCM/CRM, FSI-SPH) + PhysX Vehicle2(야드 차량, Zone F 전용) + 자체 클린룸 Fossen 6-DOF | BeamNG.tech(견적 기반), 고객 CarSim/CarMaker FMU(FMI 3.0) | Chrono 10.0.0(AMD ROCm은 dev 브랜치에만 있음) | BSD-3 / Apache-2.0 / 자체 | Chrono 10.0·Fossen: **OK** / PhysX Vehicle2: **Zone F 전용**(현재 Isaac Lab·Isaac Sim 경유), 테넌트·온프렘 개방은 P2 조건부 PhysX SDK 소스 어댑터(§3.4) 또는 Mobility α 설계 메모(M17)의 C++ 바인딩 결정 이후 / BeamNG.tech·고객 FMU: **BYOL**(벤더·고객 라이선스) | 차량 Mobility Pack α는 M18–M24(Chrono::Vehicle 어댑터 + OpenDRIVE/OpenSCENARIO, Zone F에서는 Vehicle2 병행), 해양·오프로드는 P3. 테넌트 AMR은 Newton 관절형 휠 모델을 쓴다. Stonefish(GPL-3.0)는 쓰지 않는다 |
| 7 | 드론 | PX4 SITL + Gazebo Jetty | Pegasus(Isaac Sim 5.1에 묶여 있음)를 포팅하거나 자체 브리지 개발 | Pegasus v5.1.0 | BSD-3 / Apache-2.0(Pegasus 코드 BSD-3, 실행은 Isaac Sim 약관 적용) | PX4·Gazebo·자체 PX4 브리지: **OK** / Pegasus 포팅: Isaac Sim 런타임 의존이므로 **Zone F·BYOL 전용** | ArduPilot(GPL)은 온프렘 번들에서 제외. 기본 PX4 SITL 템플릿은 M20–M24(기술 준비, P2 RL 1종), 상업화는 P3 국방 에디션 |
| 8 | 렌더·센서(팩토리 SDG) | **Isaac Sim 6.1 RTX 실시간**(Kit 110.x [U: Isaac Sim 6.1 번들 버전]) + Replicator. RTX 카메라(PPISP)·라이다·레이더·초음파 | ovrtx(GA와 약관 확보 후). Blender Cycles(별도 프로세스, 내부 전용) | Kit 110.3.0(2026-08-28, kit-app-template 기준. Isaac Sim 6.1 번들 Kit 버전은 [U]). ovrtx 0.5.1 alpha(2026-10-06) | NVIDIA 독점(Kit: NVIDIA SLA + Omniverse PST. ovrtx: AI Products PST) | **NVIDIA 서면확인 필요** | RT 코어 GPU 필수(데이터센터 기준 최소 A40, 권장 L40S, 최적 RTX PRO 6000 Blackwell). H100/H200/B200에는 RT 코어가 없다 |
| 9 | 렌더(테넌트·웹) | **R0 브라우저 렌더:** three.js r186(WebGPU/WebGL2) + Spark 2.x(WebGL2), PlayCanvas 2.23(WebGPU), Babylon.js 9.29(OpenUSD WASM). WebGPU가 없는 브라우저는 WebGL2로 동작 | Newton Warp 렌더러(RL 디버그·타일드 카메라) | — | MIT / Apache-2.0 | OK | 서버 GPU 비용 없음이 기본. 고충실도 보기는 별도 세션 |
| 10 | 센서 모델(테넌트·소버린) | **자체 Warp Sensor Library** + 실측 센서 프로파일(카메라 차트, 라이다 거리·강도, 노이즈 PSD) | RTX 센서(고객 자체 라이선스 환경) | — | 자체(Apache 의존성) | OK | 레이더·EO/IR은 오차 막대가 공개된 검증 계획을 통과하기 전에는 해양·국방에 판매하지 않는다(§4.2) |
| 11 | 신경 재구성 | **gsplat 1.6.0 + 3DGRUT 2.0**(3DGUT) | fVDB Reality Capture. NuRec(성숙도·약관 [U]) | 3DGRUT 2.0(2026-06) | Apache-2.0(NuRec은 미확인) | OK(NuRec은 확인 필요) | Instant-NGP(비상업)와 Inria 3DGS 계열을 대체 |
| 12 | 피드포워드 기하·생성형 3D | VGGT-1B-Commercial, MapAnything-apache 가중치(기본 가중치는 NEVER #22), DA3 Small/Base/Metric. TRELLIS.2(nvdiffrast 교체 후), SAM 3D Objects(민수 전용) | Articulate-Anything(MIT), CoACD/CuACD | TRELLIS.2-4B | 다양함. SAM License(SAM 3D Objects·SAM 3)와 VGGT-1B-Commercial은 **커스텀 사용 제한 라이선스**(신청서, 군사·ITAR 제외) | SAM·VGGT-Commercial: **조건부(V7)**. Zone T 호스팅 추론은 V7 통과 후, Zone S 온프렘 번들(가중치 재배포)은 재배포 조항 서면 확인 전 제외 / 국방 **NO** / 나머지 허용형 항목 OK | Hunyuan3D 2.1은 한국을 지역에서 제외(출력물 사용 포함)하므로 금지 |
| 13 | 생성형 증강·월드모델 | Cosmos Transfer 2.5(현재) → **Cosmos 3 Nano 16B** 파인튜닝(M9부터) | Cosmos 3 Super 64B(정책 평가, P3), Edge 4B | Cosmos 3(2026년 5–6월, Super 64B / Nano 16B / Edge 4B). Predict·Transfer 2.5는 유지보수 축소 | OpenMDW-1.1(전문 미확인). Transfer 2.5 가중치는 NVIDIA Open Model License | OK(법률 검토 V7 조건) | 라벨 일관성 QA를 통과한 프레임만 납품한다 |
| 14 | 학습 프레임워크 | **Isaac Lab 3.x(GitHub 소스 빌드)** + rsl_rl 5.5 / skrl 2.1. **mjlab 1.6.0** | RLinf 0.3(P2, VLA RL), SB3 2.9(교육) | mjlab 1.6.0(2026-08-09) | BSD-3 / Apache-2.0 / MIT | Kit-less Newton 경로는 OK. PhysX·RTX 경로는 #2와 같다 | PyPI 휠(독점) 대신 소스 빌드. 테넌트 기본은 mjlab과 Isaac Lab-Newton |
| 15 | 모방학습·VLA | **LeRobot 0.6.1** + LeRobotDataset v3. SmolVLA 450M(기본·국방). GR00T N1.7(휴머노이드·양팔) | ACT, Diffusion Policy. pi0.5는 가중치 약관 확인 전까지 차단 | LeRobot 0.6.1(2026-08-03). GR00T N1.7 GA(3B) | Apache-2.0. GR00T 가중치는 NVIDIA Open Model License. openpi 가중치 약관은 명시되지 않음 | LeRobot·SmolVLA: OK / GR00T: 학습·내부 사용 OK. 파인튜닝 가중치의 고객 납품은 재배포에 해당하므로 **조건부(V7, M3)**. 부정적이면 SmolVLA 또는 ACT로 증류해 납품 | 파인튜닝 비용: SmolVLA 약 4 A100-시간, GR00T·pi0.5 단일 과제 약 2–40 H100-시간 |
| 16 | 시연 증강·텔레옵 | Isaac Lab Mimic(팩토리). 테넌트용: GELLO + SpaceMouse + LeRobot 기록 | SkillGen은 Apache 태그로 고정한 cuRobo와 NVIDIA 확인이 있을 때만. Isaac Teleop(CloudXR)은 팩토리 전용 | isaaclab_mimic | Mimic은 Apache-2.0. **MimicGen·DexMimicGen 코드는 사용 금지** | Kit-less 동작이 검증되기 전까지 팩토리 전용 | 데모 10개 → 1,000개 생성 시간: 상태 기반 18–40분, **시각운동(visuomotor) 약 10시간**. 생성 성공률은 Franka 약 50% |
| 17 | 인식 모델·SDG | (a) 팩토리 SDG: Omniverse Replicator. (b) 테넌트 SDG: Newton Warp 타일드 카메라 래스터 + Warp Sensor Library. (c) 검출기: RF-DETR N–L | — | — | (a) NVIDIA 독점(Kit·Omniverse 약관) / (b) Apache-2.0·자체 / (c) Apache-2.0(XL/2XL은 PML 1.0) | (a) **NVIDIA 서면확인 필요**(Zone F 산출물 전용) / (b) OK(Zone T·S) / (c) N–L OK, XL/2XL 제외 | Ultralytics(AGPL)는 SaaS 사용 금지 |
| 18 | 장면·데이터 포맷 | **OpenUSD**(툴링은 26.08, 런타임은 Isaac Sim 6.1 번들 USD). UsdPhysics + newton/mjc/physx 스키마. 자체 `aic:TwinCertificate` | glTF + KHR_gaussian_splatting(비준 완료). URDF/MJCF(Apache 변환기). MCAP. LeRobot v3. FMI 3.0/SSP. ASAM OpenX | UsdPhysics 중첩과 Hydra 2 기본값은 25.11부터 | AOUSD Core 1.0.1(CC-BY-ND 사양). 변환기 Apache-2.0 | OK | AOUSD Core는 UsdPhysics를 포함하지 않으므로 백엔드 간 적합성 스위트로 보완 |
| 19 | 오케스트레이션 | K8s 1.32+, GPU Operator v26.7.x, **KAI Scheduler v0.18.x**, Ray 2.59, SkyPilot, MLflow 3 | OSMO(Apache), Kueue/KubeRay | — | Apache-2.0 | OK | MinIO(AGPL-3.0 [U], SPDX 확인 M2)와 lakeFS 1.87 이상(BSL 1.1)은 제외. SeaweedFS 또는 Ceph RGW(LGPL, 의무 이행) 사용 |
| 20 | 스트리밍 | **자체 WebRTC 게이트웨이**(인증·TLS·NVENC·세션 관리) | Kit App Streaming은 게이트웨이 뒤에서 팩토리·고객 라이선스 환경에만. Selkies(MPL-2.0)는 CEN 데스크톱용 | — | 자체 / MPL-2.0 | OK | Isaac Sim 스트리밍에는 인증·암호화가 없고 host 네트워크가 필요하다 |
| 21 | 라이브 트윈 연결 | 자체 ROS 2 브리지(신규 배포 기본 **Jazzy·Lyrical**, Humble은 best-effort, Zenoh), open62541(OPC UA), MQTT, Kafka, TSDB(TimescaleDB Apache-2.0 에디션 또는 InfluxDB 3 Core) | Eclipse Ditto 방식의 트윈 상태 서비스(EPL-2.0) | ROS 2 Lyrical(2026-05-22 출시, 2031-05 EOL). Jazzy 2029-05 EOL. **Humble 2027-05 EOL**(이후 보안 패치 없음) | MPL-2.0 / EPL-2.0 / Apache-2.0 | OK(약한 카피레프트는 수정 파일 공개·고지 의무 이행) | Isaac Sim ROS 워크스페이스는 Humble·Jazzy만 지원. Humble 고객 브리지는 M7 이후 best-effort. TimescaleDB 고급 기능(TSL)은 제외 |
| 22 | 에이전트 | **자체 MCP 서버**(사양 2026-07-28) + 샌드박스 USD 코드 에이전트 | kit-usd-agents(개발 단계 API 그라운딩용) | — | 자체 / Apache-2.0 | OK | 임의 코드를 실행하는 커뮤니티 MCP는 테넌트에 노출하지 않는다 |
| 23 | 관찰 전용 | Genesis World 1.4.3(Apache. Nyx 렌더러는 폐쇄 바이너리라 제외). Isaac Sim 7.0 alpha(사이드 브랜치). ovphysx 0.6.3 alpha(소스는 Apache, pip 휠과 ovstage는 독점) | — | — | — | **NO**(현 단계) | Genesis 43M FPS 주장은 비현실적 설정으로 비판받았다(약 150배 차이) |

**버전 정합성 결정**
- Isaac Lab 3.0-EA는 Newton 1.5.2와 Warp 1.16을 대상으로 한다. Newton 1.6.1의 최소 Warp 버전은 pyproject로 확인한다 [U]. 최신 Warp 1.18 휠을 쓰면 Turing(sm_75) 이상 GPU와 R580 이상 드라이버(CUDA 13)가 필요하다. 1.6.1이 Warp 1.16을 받아들이면 이중 핀 문제는 없어진다.
- **원칙:** 릴리스 트레인마다 Newton은 **Isaac Lab 3.x GA가 실제로 지원하는 버전 하나로 통일**한다. 테넌트 Kernel 경로가 1.6.x 신기능(솔버 등)을 반드시 써야 할 때에만 이중 핀을 허용하고, 그 차이는 적합성 스위트로 관리한다.
- 모든 트레인의 호환성 매트릭스(Isaac Sim, Kit, Isaac Lab, Newton, Warp, MuJoCo, mjlab, PyTorch, CUDA, 드라이버)는 **실제 국내 CSP GPU 이미지에서 검증한 뒤** 발행한다.

---

## 3. "직접 구축 vs 도입" 결정

### 3.1 명시적 답변
- **물리 엔진: 직접 구축하지 않는다(NO).** 도입·통합하고, 작은 Warp 커널(촉각, 센서 노이즈, 해양 Fossen 동역학)만 만든다. 범용성이 있는 커널은 Newton에 업스트림 기여해 로드맵 영향력을 얻는다.
- **렌더러: 직접 구축하지 않는다(NO).**
  - 팩토리: Isaac Sim RTX가 카메라·라이다·레이더를 하나의 USD 스테이지에서 렌더링한다.
  - 테넌트: 브라우저 렌더 라이브러리(WebGPU/WebGL2)와 Newton Warp 렌더러를 쓴다.
  - 신경 렌더링: 3DGUT(Apache-2.0)를 쓴다.
  - 자체 패스 트레이서는 고객이 돈을 낼 가치를 더하지 못한다.
- **대신 소유하는 것:** 엔진 사이의 이음새(Sim Kernel API, 적합성 스위트, Run Manifest), 현실과의 이음새(Forge, Fidelity Lab, 인증서), 사용자와의 이음새(Outcome Console, Studio, 한국어 MCP 에이전트).

### 3.2 근거: 엔진 개발 이력과 비용

| 근거 | 내용 | 시사점 |
|---|---|---|
| MuJoCo | Roboti LLC에서 약 10년 개발. DeepMind가 2021년 10월 인수, 2022년 5월 오픈소스화. 2026년 7–10월에 마이너 릴리스 5회(3.11–3.15) | 한 회사가 10년 들인 결과물이 무료로, 2–3주마다 업데이트된다 |
| Newton | 2025년 3월 발표. NVIDIA·Google DeepMind·Disney Research가 기존 Warp·MuJoCo 코드를 바탕으로 2026-03-10에 1.0 출시. 이후 7개월 동안 마이너 6회(현재 1.6.1) | 대형 3개 조직의 합작 속도를 스타트업이 따라잡을 수 없다 |
| Chrono / Drake | 각각 약 20k, 35k 커밋의 수십 년 프로젝트 | 차량·접촉 정밀도는 축적의 산물이다 |
| Genesis | 20개 이상 연구실이 약 24개월 협업 [U] → 회사 주도로 2026년 5월 1.0 | 1.0에 이르기까지도 대규모 협업이 필요했다 |
| 자체 구축 비용 추정 | 40–80명 전문가, 3–5년(추정 150–300 engineer-year), 약 ₩400–600억, MVP까지 30–48개월 이상 | 우리 24개월 전체 예산(₩122억)의 3–5배 |
| 리서치 의사결정 매트릭스 | 자체 엔진(A) 2.40 / NVIDIA 중심(B) 3.70 / 오픈 멀티엔진(C) 3.20 / 하이브리드(D) 4.23 | 하이브리드 D가 1위다. D의 핵심은 Newton·MuJoCo·Isaac Lab Kit-less 오픈 코어이고, RTX는 프리미엄 계층이며, Phase 0만 Isaac Sim에 기댄다. B안이 D를 'Isaac 우선 하이브리드'라고 부른 것은 잘못된 표기이므로 정정한다 |
| 충실도 | GAUGE·GPUSimBench(수치 미확인 [U])는 어떤 엔진도 현실에 균일하게 충실하지 않다고 보고했다 | 충실도는 엔진 소유가 아니라 보정·측정의 문제이고, 측정은 우리가 소유한다 |

### 3.3 컴포넌트별 OWN / INTEGRATE / LICENSE / PARTNER 맵

| 구분 | 컴포넌트 |
|---|---|
| **OWN** (엔지니어링의 약 60%) | ① **Sim Kernel API**: load/step/get_state/set_state/apply_actions/render/contacts/snapshot/restore/set_seed/capabilities. Isaac Lab 3.0의 팩토리 패턴을 미러링한다. ② **적합성 스위트**: P0 장면은 C01 낙하 박스, C02 진자, C03 Franka 픽, C04 폴리백, C05 바퀴 차량이다(C01–C15 정본은 [04 §4.6](04-system-architecture.md)). 모든 업그레이드 때 CI에서 돌린다. ③ **Run Manifest**와 장면 커밋 서비스(콘텐츠 해시 USD 레이어, 브랜치) ④ **Athanor Forge**: 오케스트레이션, 관절·물성 추정 자체 모델, 물리 QA, 인증서 생성기 ⑤ **Fidelity Lab**: 측정 프로토콜, 테스트 셀, 페어드 코퍼스, Sim2Real Gap Scorecard, 충실도 예측기 ⑥ **Athanor Crucible**와 K-Physical AI Arena: 과제 스위트, 거버넌스 헌장 ⑦ **Outcome Orchestrator**: 주문 명세, 작업 DAG, QA 게이트, 토큰 미터링 ⑧ 라이선스·출처(Provenance) 레지스트리(SPDX 게이트) ⑨ 한국어 MCP 에이전트와 검증 게이트 ⑩ 자체 WebRTC 게이트웨이와 컨트롤 플레인(테넌시, RBAC, 데이터 거주 태그) ⑪ 자체 Warp Sensor Library와 클린룸 Fossen 해양 모듈 ⑫ 소버린 패키징(서명 SBOM, 에어갭 설치기, 오프라인 업데이트) ⑬ 한국 콘텐츠(SKU, 셀·현장 트윈, 센서 프로파일) |
| **INTEGRATE** (오픈소스, 버전 고정) | Newton, MuJoCo/MJWarp, mjlab, Isaac Lab(소스), PhysX SDK 5.11, Drake(Zone S는 독점 솔버 제외 소스 빌드), Chrono 10, PX4, Gazebo, gsplat, 3DGRUT, fVDB, VGGT-1B-Commercial(V7 조건부), MapAnything-apache, DA3 S/B/Metric, TRELLIS.2(nvdiffrast 교체), SAM 3D(민수, V7 조건부), Articulate-Anything, CoACD/CuACD, LeRobot, rsl_rl, skrl, RLinf, RF-DETR N–L, Cosmos 3, OpenUSD, KAI, Ray, Kafka, open62541, MCAP, three.js, PlayCanvas, Babylon.js, Spark |
| **LICENSE** (상용) | Isaac Sim/Kit RTX(팩토리 내부. NVIDIA가 요구할 때만 NVAIE), ovrtx·NuRec(GA와 약관 확보 후), 고객 보유 CarSim/CarMaker/FTire(FMI 연결), Ultralytics Enterprise(고객이 요구할 때만) |
| **PARTNER** | NVIDIA(Inception → NPN, co-sell, 서면 약관), Linux Foundation Newton(업스트림), 로봇 OEM(Doosan Robotics, Rainbow Robotics, HD Hyundai Robotics), 시험기관(KTL·KIRIA·TTA 중 Arena 공동서명 1곳), MORAI(AV), 그룹 SI(Samsung SDS, LG CNS, SK AX, Hyundai AutoEver, HD Hyundai 계열 IT), 국내 CSP(NHN·Naver·KT, RT GPU), KAIST·SNU·ETRI(IITP 컨소시엄) |
| **NEVER** (CI와 마켓플레이스에서 자동 차단) | Hunyuan3D 2.x(한국 제외, 출력물 포함), Inria 3DGS와 파생(2DGS, MILo), PGSR, SuGaR 계열 코드, Instant-NGP, nvdiffrast, Neuralangelo, MimicGen·DexMimicGen 코드, PhysX-Anything(S-Lab), ManiSkill 자산(CC BY-NC), AgiBot World·GO-1, RLDX-1 가중치, DA3 Large/Giant, 원본 VGGT-1B, Waymax·WOD, SaaS 내 Ultralytics(AGPL), 온프렘 번들 내 GPL(BlenderProc, Stonefish, ArduPilot), lakeFS 1.87 이상(BSL), 국방 에디션 내 SAM 계열·VGGT-Commercial, Isaac Lab 번들 cuRobo(Apache 태그로 고정한 업스트림만 허용), **#22 후보: MapAnything 기본(비 apache) 가중치**(허용 대상은 MapAnything-apache 가중치로 한정. [부록 A §0.3](appendix-a-technology-catalog.md), [05](05-physics-and-realism.md) Forge 라인과 정합) |

### 3.4 접촉 집약 조작 경로: 명시적 결정
- **결정:** 접촉 집약 조작(삽입, SDF 접촉, TacSL 촉각, Mimic 데이터 증강, Teleop)은 **내부 팩토리의 Isaac Lab 3.x + PhysX(Isaac Sim 6.1) 경로를 받아들인다.** 결과는 산출물(데이터셋, 정책, 리포트)로만 판매한다.
- **테넌트 경로:** Newton SDF + hydroelastic과 mjlab 조작 과제만 제공한다. Kit-less 모드에서 TacSL·Mimic·Teleop가 동작한다고 **검증하기 전에는 약속하지 않는다.**
- **PhysX SDK 소스 어댑터:** P2에 조건부로 착수한다. 조건은 셋 모두다.
  - (a) G1 통과
  - (b) 베이크오프에서 PhysX가 Newton보다 접촉 과제에서 우위로 측정됨
  - (c) 온프렘 수요 2건 이상
  공수는 B안의 24 HM이 아니라 **36–48 HM**으로 현실화한다(articulation, tensor API, SDF, drive 패리티). 대안으로 ovphysx를 Apache 소스에서 ovstage 없이 빌드하는 방법을 P0의 V2 검증에서 법률·기술 양면으로 확인한다.
  어댑터에 착수하면 적합성 스위트의 백엔드 수에 하나를 더하고, Zone T/S의 sim2sim 게이트를 3개 백엔드로 넓히며, PhysX Vehicle2의 테넌트 개방 여부를 함께 판정한다.
- **60 DoF 초과 메커니즘:** 휴머노이드 + 양손처럼 MJWarp의 약점이 드러나는 구성은 PhysX 경로로 보내거나 관절 트리를 분할한다. 휴머노이드 + 덱스터러스 핸드 템플릿 출시 전에 베이크오프 T11로 확인한다.

### 3.5 AICHEMIST 고유 IP 자산 목록
1. **Sim Kernel API 사양 + 적합성 스위트 + Run Manifest 스키마.** 엔진 교체가 가능함을 증명하는 자산이다.
2. **Athanor Forge 파이프라인**과 자체 학습 모델. 관절 추정, VLM 물성 사전분포, 영상 기반 sysid 보정이 포함된다.
3. **페어드 실측/시뮬 측정 코퍼스.** 궤적, 접촉력, 센서 통계, 실셀 성공률로 구성되며 해자의 중심이다.
4. **인증 체계.** Bronze/Silver/Gold 기준, `aic:TwinCertificate` 스키마, Sim2Real Gap Scorecard, 충실도 예측기로 이뤄진다.
5. **Crucible 과제 스위트와 Arena 거버넌스 헌장**(제3자 공동서명, 이해상충 회피 규정)
6. **한국어 MCP 에이전트.** 타입이 지정된 도구 세트와 USD 검증 게이트 로직을 포함한다.
7. **Outcome Orchestrator와 토큰 미터링 로직**(GPU 풀별 원가 기반)
8. **라이선스·출처 레지스트리**(코드 SPDX, 자산·데이터·가중치 권리)
9. **한국 콘텐츠 라이브러리.** 한국 SKU, 공장·물류·조선 셀 트윈, 센서 디바이스 프로파일로 구성된다.
10. **자체 Warp Sensor Library와 클린룸 Fossen 해양 모듈**
11. **소버린 패키징.** 서명 SBOM, 에어갭 설치기, 드라이버 사전 점검기다.
12. **특허 포트폴리오**(M24까지 출원 8건 목표 [A]): 인증서 산출 방법, 충실도 예측, 월드모델 증강 라벨 일관성 검증, LLM→USD 변경 검증 게이팅, 페어드 측정 프로토콜.

---

## 4. 4대 요구사항 충족 설계

### 4.1 요구사항 (1) 강력한 물리 엔진
**메커니즘**
- **작업 유형별 기본 백엔드**는 베이크오프(§14.3)로 확정한다.
  - 보행·전신: Newton/MJWarp
  - 접촉 집약 조작: Isaac Lab + PhysX(팩토리), Newton SDF·hydroelastic(테넌트)
  - 폐루프: Kamino
  - 변형체: VBD·MPM
  - 재현·인증: MuJoCo CPU
  - 차량·지형: Chrono(Zone T/S), PhysX Vehicle2(Zone F 전용). 테넌트 AMR은 Newton 관절형 휠 모델
- **적합성 스위트:** 장면 정본은 [04 §4.6](04-system-architecture.md)의 C01–C15다. 백엔드는 P0 Newton/MJWarp·MuJoCo CPU·Isaac Lab PhysX(3) → P1 + Drake(4) → P2 + Chrono(5) → P3 + 클린룸 Fossen 6-DOF(6, 해양 장면 C13)로 늘린다. FMU는 공동 시뮬레이션 브리지라 백엔드 수에 넣지 않는다. 허용치 최종값은 베이크오프 결정 메모(2027-01 첫 주)에서 고정한다.
- **sim2sim 게이트(구역별, 2단):** 교차 백엔드는 **Zone F 정책이면 Newton → PhysX → MuJoCo CPU 3개**, **Zone T/S 정책이면 Newton ↔ MuJoCo CPU 2개**다(조건부 PhysX SDK 소스 어댑터 편입 시 3개).
  - **Tier 1(모든 수출 정책, 실패 시 수출 차단):** 1,000 에피소드, 성공률 차 ≤10%p, 평균 반환 비율 ≥0.85, 지연·노이즈 주입 후 하락 ≤15%p, ONNX 행동 최대 오차 ≤1e-3.
  - **Tier 2(인증서·Crucible 공식 캠페인 대상):** 초기조건 200개, 백엔드 쌍별 ≤5%p, 관절 RMSE ≤0.05 rad [A].
  - 정본은 [07 §7.3](07-training-module.md)이다.
- **보정:** MuJoCo sysid 툴박스, 액추에이터 네트워크, 영상 기반 마찰·질량 식별을 쓰고, 오프라인 기준으로 Drake hydroelastic을 쓴다.
- **결정론 정책:** 인증서와 '재현 가능' 주장은 **MuJoCo CPU 또는 Newton 결정론 모드에서, 고정된 하드웨어·드라이버로만** 발행한다. Newton 결정론 모드는 N1–N5 시험(베이크오프 W7)을 통과한 뒤에만 인증 경로에 넣는다. GPU 배치 산출물에는 '통계적 재현(statistically reproducible)' 라벨을 붙이고 시드, GPU SKU, 드라이버를 Run Manifest에 저장한다. Newton의 '하드웨어 간 이식 가능 결정론' 주장은 사내에서 직접 시험한다.
  - **결정론 등급:** Run Manifest 필드 `D0_bitwise` / `D1_statistical` / `D2_generative` / `none`으로 정본화한다. 인증서는 D0 경로에서만 발행한다.
  - **D0 경로 확장 규칙:** Chrono CPU(차량), 클린룸 Fossen(Warp CPU, 선박), PX4 SITL lockstep(드론)은 반복 비트 일치 시험(N1–N4와 동등)을 통과하고 CTO가 D0 목록에 등록한 뒤에만 인증 경로로 쓴다(목표 등재 Chrono M22, Fossen M28 [A]). 등록 전 해당 동역학 산출물은 D1 '통계적 재현'으로 표기하고 Scorecard 리포트만 납품하며, 인증서는 자산·센서 항목에만 발행한다.
  - **변형체·입상체·유체:** 변형체(VBD·flex·cable) 산출물은 D1이다. 변형체 인증서는 정적 보정 시험(처짐·정지 형상)을 MuJoCo CPU로 D0 재현한 항목에만 붙이고 'experimental'로 표기한다. 입상체·유체는 인증 대상에서 제외한다.
- **업그레이드 세금:** 엔진에 닿는 워크스트림(Kernel, Sensors, Platform) 용량의 **25%**를 예약한다(리서치 경고 20–30% 범위). 반기 릴리스 트레인을 운영하고, 분기 중간점검에서는 보안 패치만 반영한다(§7.1).

**측정 목표**

| 지표 | P0(M4) | P1(M12) | P2(M24) | P3(M36) |
|---|---|---|---|---|
| 적합성 스위트 통과(백엔드 수 × 장면)¹ | 3 × 5 | 4 × 8 | 5 × 12 | 6 × 15 |
| 사내 벤치마크 공개(steps/s/$, 보상 도달 시간) | 10개 과제 | 분기 갱신 | 월간 갱신 | 월간 갱신 |
| 자동 Forge 추정값의 Gold 랩 실측 대비 질량 / 마찰 오차² | ≤15% / ≤25% | ≤10% / ≤20% | ≤8% / ≤15% | ≤5% / ≤10% |
| 궤적 오차 ADE(표준 밀기·낙하 시험) | 기준선 측정 | ≤2 cm | ≤1.5 cm | ≤1 cm |
| 인증 시험 결정론적 재현율(D0 경로) | 100% | 100% | 100% | 100% |
| 신규 엔진 릴리스 채택 지연(고정 버전 기준)³ | — | ≤45일 | ≤30일 | ≤30일 |

¹ 장면 정의의 정본은 [04 §4.6](04-system-architecture.md)의 C01–C15다(05의 S 번호는 쓰지 않는다). P0 '3 × 5'의 백엔드 3개는 베이크오프 구성 B1–B5 가운데 Newton/MJWarp 계열·PhysX·MuJoCo CPU의 통과 백엔드 수로 센다.

² 자동 Forge 추정값(VLM 사전분포 + 영상 sysid) θ_auto를 Gold 랩 실측값 θ_lab과 비교한 상대오차 |θ_auto − θ_lab| / θ_lab이다([05 §16.1](05-physics-and-realism.md) D4). Gold 값 자체는 랩 실측이므로, 이 지표는 자동화 체인의 정확도를 뜻한다. Gold 인증서에는 랩 실측값과 측정 불확도를 기록하며, 이 KPI 수치를 Gold 자산의 인증 임계나 고객 보증 문구로 쓰지 않는다. 시험기관 비교 지표는 'Gold 랩 실측 재현성'으로 따로 부른다.

³ 검증된 사이드 브랜치 후보로 채택하기까지의 일수다. 프로덕션 반영은 다음 릴리스 트레인에서 한다.

### 4.2 요구사항 (2) 높은 현실 유사도(시각·물리·센서)
**메커니즘: 하나의 OpenUSD 스테이지 안의 4계층 현실감 구조**
- **L1 물리 기반 메시·재질:** MDL, MaterialX, OpenPBR와 물리 스키마.
- **L2 신경 재구성 배경:** UsdVolParticleField 3DGS·3DGUT를 쓰고, 충돌용 프록시 메시는 숨겨 둔다.
- **L3 보정된 센서:** 팩토리에서는 RTX 카메라(PPISP), 라이다, 레이더를 쓰고, 테넌트에서는 Warp Sensor Library를 쓴다. 둘 다 디바이스별 실측 프로파일을 적용한다.
- **L4 생성형 증강:** M5–M8은 Cosmos Transfer 2.5, M9부터는 Cosmos 3 Nano 16B 파인튜닝을 깊이·세그멘테이션·엣지 조건으로 쓰고, 라벨 일관성 검사를 자동으로 돌린다(§2 #13).
- 위 L1–L4는 '현실감 계층'이다. 시스템 계층 L0–L8(§6.1)과는 번호 체계가 다르다.

**Real2Sim**
- 대상 현장의 갭은 스플랫으로 제거한다.
- 롱테일은 구조화된 도메인 랜덤화로 덮는다.
- 소량의 실제 데이터 파인튜닝을 기본으로 포함한다.

**Sim2Real Gap Scorecard 항목**
- 렌더링: PSNR, SSIM, LPIPS
- 인식: 합성으로 학습한 모델의 실데이터 mAP ÷ 실데이터로 학습한 모델의 mAP, 소량 실데이터 곡선
- 정책: 정책 5개 이상의 sim/real 성공률 Pearson r(Fisher 95% CI 병기. 인증·G3 판정은 정책 패밀리 8개 이상, 권장 12개 [A])과 순위 일치
- 물리: 궤적 ADE/FDE, 정지 자세 오차, 접촉력 오차
- 센서: 라이다 거리·강도 오차, Chamfer 거리, 노이즈 PSD
- FID·KID는 보조 지표로만 쓴다.

**센서 현실감 검증 계획(해양·국방 판매의 전제)**
- 레이더(해양 레이더 포함)와 EO/IR은 실측 캠페인(KRISO·KR·시험기관과 협력 [U])으로 **오차 막대를 공개**한 프로파일을 통과해야만 판매한다.
- '단순화된 FMCW 레이더'는 국방 증거물로 팔지 않는다.
- 고정밀 레이더 모델링은 IITP 공동연구 예산으로 수행한다(§11).

**측정 목표**

| 지표 | P0(M4) | P1(M12) | P2(M24) | P3(M36) |
|---|---|---|---|---|
| 합성 전용 mAP ÷ 실데이터 학습 mAP(보류된 실데이터 기준) | ≥0.85 | ≥0.90 | ≥0.95 | 3개 버티컬에서 ≥0.95 |
| 합성 + 실데이터 10% vs 실데이터 100% | — | ≥1.0 | ≥1.0 | ≥1.05 |
| 정책 sim-to-real 성공률 갭(%p) | ≤25(1개 과제) | ≤15(3개 과제) | ≤10(5개 과제) | ≤8(10개 과제) |
| sim/real 성공률 상관(Pearson r, 정책 ≥5개, Fisher 95% CI 병기. 인증·G3 판정은 정책 패밀리 ≥8개, 권장 12 [A]) | — | ≥0.7 | ≥0.8 | ≥0.85 |
| 라이다 거리 오차(보정 타깃) | — | ≤3 cm | ≤2 cm | ≤2 cm + 레이더 프로파일 공개 |
| 증강 프레임 라벨 일관성 검사 통과율 | — | ≥98% | ≥99% | ≥99% |
| 제3자 시험성적서(KTL·KOLAS·TTA) 지표 수 | — | 1 | 3 | 5 |

### 4.3 요구사항 (3) 편의성·사용 용이성
**메커니즘**
- **두 개의 문:** Outcome Console(한국어로 주문, 검토, 인수)과 Athanor Studio(CEN 워크스페이스 안, 설치 없이 브라우저(WebGPU/WebGL2)로 동작). Studio 베타(M9)는 Zone T 전용이고, 공개 가입과 GA는 M15다.
- **한국어 MCP 에이전트:** "이 박스를 세 가지 조명에서 5만 장 생성해", "이 셀에서 피킹 정책을 학습시켜"처럼 말로 지시한다. 타입이 지정된 도구, 샌드박스, 검증 게이트, 사람의 승인을 거친다. **먼저 사내 딜리버리 엔지니어용으로 만들어** 결과물당 엔지니어 시간을 절반으로 줄인 뒤 고객에게 공개한다.
- **템플릿 카탈로그:** 피킹, 디팔레타이징, 조립, 보행, 모션 트래킹, Mimic 증강, VLA 파인튜닝, 검출기. 보상·관측·도메인 랜덤화는 GUI와 YAML로 편집한다.
- **원클릭 경로:** 휴대폰 영상 → 인증 자산(Forge) → 장면 → 데이터·정책 → Crucible 평가 → Jetson 수출(ONNX → TensorRT).
- **결과물 크레딧:** 결과물 계약 금액의 20–30%를 CEN 토큰 크레딧(12개월 유효)으로 구성한다. 이 크레딧은 계약 금액에 포함되며, 셀프서브 전환을 유도하는 장치다.
- **생산화 게이트:** 아래 세 조건을 모두 충족한 라인만 셀프서브로 연다.
  - ① 내부 작업의 80% 이상이 엔지니어 개입 없이 완료된다.
  - ② 라인 총마진이 60% 이상이다(완전원가 기준, §7.2 G1 각주).
  - ③ 모든 구성요소에 테넌트 사용에 대한 서면 라이선스 근거가 있다.

**측정 목표**

| 지표 | P0(M4) | P1(M12) | P2(M24) | P3(M36) |
|---|---|---|---|---|
| 신규 사용자 첫 시뮬레이션까지 시간(Studio) | — | ≤10분(베타) | ≤5분 | ≤5분 |
| 한국어 명령 스크립트 성공률(에이전트) | 20개 중 ≥80% | 50개 중 ≥85% | 100개 중 ≥90% | ≥92% |
| 영상 → Bronze 강체 자산 | ≤2시간(내부) | ≤30분 | ≤15분(셀프서브) | ≤10분 |
| 영상 → 학습된 피킹 스킬 | 48시간(내부) | 24시간 | 당일(셀프서브) | 4시간 |
| Forge 무개입(zero-touch) 비율 | 30% | 60% | 80% | 90% |
| 결과물당 엔지니어 시간 지수 | 100 | 50 | 25 | 15 |

- 엔지니어 시간 지수는 P0 기준선(100) 대비로 잰다. P3 말 지수 15는 연율 약 −51%로, §10.9의 '연 50% 감소' 조건과 같은 정의다.

### 4.4 요구사항 (4) 모델 학습 내장(RL·IL·VLA·인식)
**메커니즘(Athanor Skill 라인)**
- **RL:** Isaac Lab 3.x(rsl_rl 5.5 기본, skrl 2.1은 멀티에이전트·오프폴리시)와 mjlab. 1–8 GPU 원클릭 학습과 실시간 롤아웃 영상을 제공한다. PBT·ADR 스윕은 P2에 넣는다.
- **IL·VLA:** 텔레옵(팩토리는 Isaac Teleop, 테넌트는 GELLO·SpaceMouse)으로 시연을 모으고 Mimic으로 증강한 뒤, LeRobot으로 ACT, Diffusion, SmolVLA, GR00T N1.7을 학습한다. P2에는 RLinf로 VLA RL 후처리를 붙인다.
- **인식:** 팩토리(Zone F)는 Replicator SDG(+ Cosmos 증강), 테넌트(Zone T·S)는 Newton Warp 래스터 + Warp Sensor Library로 데이터를 만들고 RF-DETR N–L로 학습한다. 실데이터 소량 파인튜닝 곡선을 자동으로 그린다.
- **Sim2Real 키트:** 도메인 랜덤화 프리셋, 액추에이터 넷, teacher→student 증류, 지연·노이즈 주입, sim2sim 게이트.
- **평가:** Crucible을 Isaac Lab Arena 기반으로 만들고 고객 시나리오 스위트를 얹는다. 신뢰구간과 회귀 게이트를 포함한다.
- **배포:** ONNX(opset 고정) → TensorRT → Jetson AGX Thor 패키지를 만든다. 현장 MCAP 로그는 실패 마이닝 → 재시뮬레이션 → 재학습 → 게이트 재배포 순으로 흐른다(P2).

**컴퓨트 기준(리서치 수치)**
- 사족보행 정책 0.3–1 GPU-시간, 휴머노이드 속도 추종 1–2 GPU-시간.
- 시각 기반 덱스터러스 200–600 GPU-시간.
- SmolVLA 약 4 A100-시간, GR00T·pi0.5 단일 과제 약 2–40 H100-시간.
- 카메라 기반 RL은 상태 기반보다 약 16배 느리다.

**측정 목표**

| 지표 | P0(M4) | P1(M12) | P2(M24) | P3(M36) |
|---|---|---|---|---|
| 템플릿 과제 GPU당 병렬 환경 수 | ≥4,096 | ≥4,096 | ≥8,192 | ≥8,192 |
| 템플릿 수(RL / IL·VLA / 인식)¹ | 3 / 1 / 1 | 8 / 3 / 3 | 15 / 6 / 5 | 25 / 10 / 8 |
| Mimic 1,000개 생성(상태 / 시각운동) | 측정 | ≤1시간 / ≤12시간 | ≤40분 / ≤8시간 | ≤30분 / ≤6시간 |
| 수출 전 sim2sim 게이트 적용률(Tier 1)² | 100% | 100% | 100% | 100% |
| 실셀 이전 정책 수(누적) | 1 | 8 | 30 | 80 |
| 1B 환경 스텝당 RL 비용(카메라 없음) | 측정 | ≤$10 | ≤$6 | ≤$4 |

¹ 템플릿 ID의 마스터는 [06 §6.2](06-usability-and-agent.md)(RL-/IL-/PE- 번호), 팩별 배분의 마스터는 [08 §7.1](08-domain-packs.md)이다. P0 RL 3종은 팔 도달·큐브 들기, 빈 피킹(한국 SKU), 디팔레타이징으로 모두 조작 팩이다. 휴머노이드(G1 속도 추종·모션 추적)·사족(속도 추종)·덱스터러스(손안 재배치, 상태 기반) 템플릿은 P1(M6–M12)에 처음 들어간다. 드론 PX4 SITL 기본 템플릿은 P2(M20–M24) RL 1종으로 센다.

² Tier 1 기준(§4.1)이다. Tier 2는 인증서·Crucible 공식 캠페인 대상에만 적용한다.

---

## 5. 타깃 도메인 우선순위

### 5.1 평가표
점수는 1–5점이다[A]. '열린 경쟁 지형'이 1점이면 해당 도메인은 독자 매출 라인이 될 수 없다(거부권). 파트너 전용이거나 템플릿만 제공한다. '결과 측정성'은 납품물을 현실 대비 얼마나 빨리 채점할 수 있는지를 본다.

| 도메인 | 국내 수요 | 열린 경쟁 지형 | 앵커 접근성 | Forge·CEN 적합 | 매출화 속도 | 결과 측정성 | 라이선스·조달 마찰(역) | 합계 /35 | 결정 |
|---|---|---|---|---|---|---|---|---|---|
| **물체가 많은 조작**(물류 피킹·디팔레타이징·키팅, 공장 셀 조립·검사, 조선 작업장 핸들링) | 4 | 4 | 4 | 5 | 5 | 5 | 4 | **31** | **Wave 1 (M1–M18)** |
| **휴머노이드·양팔 VLA 데이터 + Crucible 평가** | 4 | 4 | 4 | 4 | 3 | 5 | 4 | **28** | **Wave 2 (M12–M24)** |
| AMR 플릿(공장 트윈의 맥락으로) | 3 | 2 | 3 | 4 | 4 | 4 | 4 | 24 | 부가 기능(P2 라이브 트윈) |
| **조선·항만·해양 인식**(EO/IR, 해양 레이더, COLREG) | 5 | 4 | 3 | 3 | 2 | 3 | 2 | **22** | **Wave 3 (M25–)**, 트리거 조건부 |
| AV·ADAS | 4 | 1 | 3 | 3 | 2 | 3 | 3 | 19 | **도로 AV 시뮬레이터 시장은 정면 경쟁 없이 MORAI·표준으로 연결.** 인식 데이터는 MORAI·마켓플레이스 경유. 차량 트윈 기술(Mobility Pack α)은 M18–M24에 준비(§5.5) |
| 민수 드론 | 2 | 2 | 2 | 3 | 3 | 3 | 3 | 18 | 기술 템플릿 M20–M24, 상업화는 국방 에디션 안에서 |
| 국방 UGV·드론(에어갭) | 4 | 3 | 2 | 3 | 1 | 3 | 1 | 17 | **Wave 3b (M27–)**, 트리거 조건부 |
| 사족보행 | 2 | 1 | 2 | 2 | 3 | 3 | 4 | 17 | 템플릿만 제공(매출 라인 아님) |

### 5.2 Wave 1 (M1–M18): "Pick Anything, Korea"
- **왜 먼저인가**
  - Forge의 작업 단위는 '물체'다. 한 고객을 위해 스캔한 SKU(예: 한국 라면 박스)를 다음 고객(로봇 OEM)에게 다시 팔 수 있으므로 자산이 복리로 쌓인다.
  - 결과를 몇 시간 안에 채점할 수 있다. 실데이터 mAP, 1,000회당 피킹 성공 수가 그 지표다.
  - NVIDIA 스택이 가장 깊은 영역(Mimic, GR00T, TacSL, Replicator)이고, CEN의 실내 SDG 강점이 그대로 전이된다.
  - 조선소 작업장의 용접·핸들링 셀도 '조작'이므로, 해양 인식 없이 조선 고객 접점을 일찍 만들 수 있다.
- **앵커 LOI 3곳(TIPS 제출 전, M3까지 서명):**
  - ① 로봇 OEM: Doosan Robotics(이미 Isaac·cuRobo와 통합된 것으로 GitHub에서 확인) 또는 Rainbow Robotics(Samsung 지분 약 35%, 중간 신뢰도 [U])
  - ② 조선 로보틱스: HD Hyundai Robotics, Samsung Heavy, Hanwha Ocean 중 1곳
  - ③ 물류·AI팩토리: CJ Logistics, Hyundai Glovis, Coupang, 또는 M.AX AI팩토리 주관 제조사 중 1곳. 물류 수요 자체가 아직 검증되지 않았다 [A].
- **첫 유료 레퍼런스(M4, 2027-02):** 기존 CEN SDG 고객 1곳(CEO가 M1에 지정)과 산출물 전용 데이터셋 계약을 맺는다. mAP 인수 조건을 넣고, 고객의 2027 회계연도 예산(국내 기업 예산은 12–1월 확정, 신규 발주는 1–2분기)을 쓴다.
  - 첫 데이터셋 계약(M3–M4)의 인수 하한은 합성 전용 mAP 비율 0.85(P0 KPI), 목표는 0.90이다. 데이터셋 팩 정가 계약(P1 이후)의 기준은 0.90이다(§10.4).
- **경쟁:** Lightwheel 자산은 비상업 용도만 무료다. CyLab은 물리·정책 없이 데이터만 판다. 한국 SKU 라이브러리는 아직 없다.

### 5.3 Wave 2 (M12–M24): 휴머노이드·양팔 VLA 데이터 + Athanor Crucible
- **수요:** K-Humanoid Alliance(2025-04-10 출범 [U]) 회원사, HMG/Boston Dynamics, Samsung/Rainbow, LG, RLWRLD. 중립적인 평가와 롱테일 시연 데이터가 필요하다.
- **차별점:** 제3자 공동서명이 붙은 실셀 + 시뮬 평가다. Lightwheel LW-BenchHub는 시뮬 전용이고, RoboArena는 학술용·DROID 전용이다.
- **이해상충 통제:** 공동서명 기관과 거버넌스 헌장에 서명하기 **전에는 외부 채점을 하지 않는다.** 우리가 학습시킨 정책은 공동서명 기관의 검토를 거쳐야만 인증한다(회피 규정).
- **헌장 일정:** 헌장 초안 M8 → 공동서명 MOU M10(2027-08-27) → 헌장 서명 M12 초(K-Pick Challenge 2027-10-22 이전). 서명이 늦어지면 K-Pick Challenge는 공동서명 기관 입회 아래 순위를 매기지 않는 공개 시연으로 연다.
- **글로벌 연결:** 같은 데이터·평가 상품을 M12–M15부터 미국 로봇 파운데이션모델·휴머노이드 기업에도 판다(§11.4).

### 5.4 Wave 3 (M25–M36, 트리거 조건부): 조선·해양 인식과 국방 에어갭
- **트리거:** 연환산 반복매출(ARR) ₩30억 이상, **또는** 자금이 확보된 앵커 계약(조선사 공동개발이나 국방 과제, 확정 금액 ₩5억 이상). 여기에 소버린 에디션 GA와 센서 검증 프로파일(§4.2)이 있어야 한다.
- **트리거의 현실성:** 기준안의 2028년 말 ARR 목표는 ₩20억이므로 M25에 ARR ₩30억 트리거는 충족되지 않는 것이 기본 경로다. ARR 경로는 2029년 중에야 충족된다. 따라서 M25 착수는 확정 ₩5억 이상의 앵커 계약에 달려 있다. M25는 트리거 판정을 시작하는 시점이고, 국방 Air-gap 에디션은 M27부터다. §10.6의 2029년 Sovereign·Air-gap ₩15억 가운데 Air-gap 약 ₩4.5억은 이 앵커 계약을 전제로 한다 [A]. 조선 앵커와의 관계는 Wave 1의 작업장 셀 조작 계약으로 미리 만든다.
- **해양:** 자율운항선박법(2025-01-03 시행)이 성능 검증을 요구하고, Avikus는 약 350척에서 운용 중이다[U]. SHI SAS, Hanwha Ocean도 수요처다. 해양 시뮬레이션에는 상업적 선두가 없다. Fossen 6-DOF, 파랑 스펙트럼, Chrono FSI, 검증된 레이더·EO/IR 프로파일로 EO/IR·해양 레이더·COLREG 데이터셋과 항만 크레인 트윈을 만든다.
- **국방(Wave 3b, M27–):** Athanor Air-gap 에디션이다. 텔레메트리가 없고, 오프라인 서명 업데이트를 쓰며, SAM 계열·VGGT-Commercial·미확인 모델을 제외하고, 온프렘 LLM의 출처를 확인한다(V8). Chrono CRM 지형 UGV와 PX4 드론 인식을 포함한다. 판매 주기가 12–24개월이므로 2027년 하반기 DAPA 프로그램은 '준비'로만 잡는다.
- **AV:** 도로 자율주행용 HIL·인증 도구 시장에서는 정면으로 경쟁하지 않는다. 차량 트윈 자체는 Mobility Pack α(M18–M24)로 만들고, 승용차 ADAS·자율주행 시뮬레이터와는 OpenSCENARIO·OSI·FMI 3.0과 MORAI 파트너십으로 연결한다. 한국 도로 인식 데이터 팩은 MORAI와 마켓플레이스를 통해 판다.

### 5.5 자동차 선택지(CEO 요구 "자동차 등" 대응)

| 선택지 | 범위 | 공수·비용 [A] | 착수 조건 | 결정 |
|---|---|---|---|---|
| ① 현안: Mobility Pack α + 표준 연결 | 야드·저속 차량 동역학(Chrono::Vehicle, Zone F는 PhysX Vehicle2 병행), 도로 시나리오 재생(OpenDRIVE·OpenSCENARIO), 카메라·라이다 리그, 고객 CarSim·CarMaker FMU 연결(FMI 3.0) | WS1-M 1명 × 7개월(M18–M24) ≈ 7 HM + WS3 지원. 기존 인원·예산 안이라 추가 비용 없음 | 계획대로 M18 착수 | **채택** |
| ② 확장: 승용 ADAS 센서·동역학 트윈(Tier-1 협력사 대상) | 승용차 센서 리그·차량 동역학 트윈, ADAS 인식 데이터 | [08 §6.1](08-domain-packs.md) Type B 기준 18–37 HM(인건비 약 ₩2.5–5.2억) | 재결정 트리거 X14(확정 ₩5억 이상 앵커 또는 ARR ₩30억) 또는 고객 NRE | **조건부 옵션** |
| ③ 도로 AV 시뮬레이터 자체 구축 | dSPACE·IPG·Applied Intuition·MORAI와 정면 경쟁 | — | — | **기각**(열린 경쟁 지형 1점, §5.1 거부권) |

- 08의 'Mobility Pack β'는 오프로드 UGV(P3)를 뜻한다. 위 ②는 별도 확장 옵션이며 β와 혼동하지 않는다.

---

## 6. 아키텍처 요약

### 6.1 계층 구조

플랫폼은 아래 아홉 계층으로 이뤄진다. 위로 갈수록 사용자에 가깝고, 아래로 갈수록 인프라에 가깝다. 계층별 상세 설계는 [04 §2–§3](04-system-architecture.md)에 있다.

| 계층 | 이름 | 한 줄 설명 | 주요 구성요소 |
|---|---|---|---|
| L8 | 사용자 화면 | 고객과 엔지니어가 만나는 모든 입구 | Outcome Console, Athanor Studio(CEN 워크스페이스: 브라우저 렌더, Jupyter·VS Code, Selkies 데스크톱), 마켓플레이스, Crucible 리더보드, REST·gRPC·Python SDK·MCP |
| L7 | 에이전트 | 한국어 지시를 검증된 장면 변경과 작업으로 바꾼다 | 한국어 LLM → 자체 MCP 서버(타입 지정 도구) → 샌드박스 USD 코드 에이전트(gVisor·Kata) → 검증 게이트(UsdValidation·물리 정합성·2개 백엔드 스모크 테스트) → 사람 승인 병합 |
| L6 | 오케스트레이션 | 주문을 작업 DAG로 쪼개고 품질·원가를 관리한다 | Outcome Orchestrator(주문 명세 → 작업 DAG → QA 게이트 → 납품 + 인증서), 토큰 미터링(DCGM + KAI → CEN 토큰), Run Manifest, 라이선스 매니페스트 |
| L5 | 생산 라인 | 결과물을 만드는 네 개의 라인 | **Forge**(촬영 → SimReady 자산 + 인증서), **Data**(SDG + 증강 + 라벨 일관성 QA), **Skill**(RL·IL·VLA + sim2sim 게이트), **Crucible**(결정론 재생 + 실셀 + Scorecard + Arena) |
| L4 | 트윈 런타임 | 같은 장면을 세 가지 모드로 돌린다 | 라이브(미러, 10–60 Hz), 시뮬레이션(배치, 실시간보다 빠름), 섀도·HIL(lockstep). fork-from-live → 보정 → what-if·RL → 이후 라이브 데이터와 비교 |
| L3 | Sim Kernel | 엔진을 갈아끼우는 공통 인터페이스 | 물리 어댑터: Newton/MJWarp, MuJoCo CPU, PhysX(Isaac Lab, Zone F), Chrono, FMU 브리지, Genesis(관찰). 렌더러 API: R0 브라우저, R1 Newton Warp, R2 3DGUT, R3 Isaac RTX(Zone F·BYOL). 센서 모델 라이브러리 + 실측 프로파일, 적합성 스위트 |
| L2 | 장면 | 모든 대상을 하나의 OpenUSD 장면으로 관리한다 | OpenUSD 스테이지 서비스, 콘텐츠 해시 장면 커밋·브랜치, `aic:TwinCertificate` |
| L1 | 데이터 | 데이터와 권리를 함께 저장한다 | 객체 저장소(SeaweedFS·Ceph RGW), Postgres, Kafka, TSDB, MCAP, LeRobot v3, MLflow 레지스트리, 라이선스·출처 레지스트리, **페어드 실측/시뮬 코퍼스(해자)** |
| L0 | 인프라 | GPU 풀을 용도별로 나눠 운영한다 | K8s + GPU Operator + KAI, RT 풀, TRAIN 풀, LIGHT 풀, LAB EDGE, 서울 리전 + 온프렘 |

### 6.2 세 개의 라이선스 구역(Zone): 모든 문서가 지켜야 하는 경계

| 구역 | 누가 쓰나 | 허용 구성요소 | 금지 | 매출 연결 |
|---|---|---|---|---|
| **Zone F: 내부 팩토리** | AICHEMIST 엔지니어만 | 허용형 전체 + Isaac Sim 6.1/Kit, RTX 센서, Replicator, Isaac Lab PhysX 경로, TacSL, Mimic, Isaac Teleop, (약관 확인 후) NuRec·ovrtx | 테넌트 접근, 고객 화면 스트리밍 | 산출물(데이터셋, 정책, 인증 자산, 리포트)만 판매. **산출물 면제 자체가 [U]이므로 NVIDIA 서면 확인(§14.2)을 받는다.** 필요하면 NVAIE를 내부 RT GPU에 적용(예산 ₩2.9억 예비) |
| **Zone T: 테넌트 대면** | Studio·Cloud 고객 | Newton(관절형 휠 모델 포함), MuJoCo, mjlab, Isaac Lab(소스, Kit-less Newton), PhysX SDK(소스, P2 조건부 어댑터 편입 후), Chrono(차량), 브라우저 렌더(WebGPU/WebGL2), Warp 센서, Newton Warp 래스터 SDG, gsplat/3DGRUT, LeRobot, 자체 게이트웨이. SAM·VGGT-Commercial 호스팅 추론은 V7 통과 후 | Kit, Isaac Sim, Replicator, PhysX Vehicle2(어댑터 전), ovrtx, ovphysx 휠, isaacsim/isaaclab PyPI 휠(NVIDIA 서면 조건 전) | 구독, 토큰, 마켓플레이스 |
| **Zone S: 소버린·온프렘·에어갭** | 고객 사이트, 국내 CSP | Zone T 구성 + 서명 SBOM, 텔레메트리 없음, 오프라인 업데이트. Drake는 독점 솔버를 제외한 소스 빌드만(V2 후) | Zone T 금지 항목 + GPL 번들(Blender는 V2 의견 전까지 제외) + SAM·VGGT-Commercial 가중치 번들(재배포 조항 서면 확인 전) + 국방 에디션에서는 SAM·VGGT-Commercial 전면 금지 | Sovereign Edition 라이선스. RTX는 **고객이 자기 라이선스로 직접 운영하는 환경(BYOL)**에서만 연동한다. AICHEMIST가 고객 라이선스로 대신 호스팅하는 것은 NVIDIA 확인 전까지 금지 |

- **Zone T/S 라이선스 구성 규칙:** 허용형(Apache-2.0/BSD/MIT)과 의무 이행이 가능한 약한 카피레프트(MPL-2.0: open62541·Selkies·OpenBao·Lichtblick, EPL-2.0: Eclipse Ditto, LGPL: Ceph RGW)로만 구성한다. 약한 카피레프트는 수정 파일 공개·고지 의무를 SPDX 레지스트리로 추적한다. TSL(TimescaleDB 고급 기능)·BSL·AGPL·GPL·비상업 라이선스는 제외한다. TimescaleDB는 Apache-2.0 에디션만 쓰거나 InfluxDB 3 Core로 대체한다.
- **NVIDIA 독점 패키지 목록(Zone F 전용):** Kit, Isaac Sim, RTX 렌더러·센서, Replicator, ovrtx, ovphysx 휠·ovstage, isaacsim/isaaclab PyPI 휠, Isaac Teleop(CloudXR). 서면 조건을 받기 전까지 Zone T/S에 넣지 않는다.

### 6.3 라이브 트윈 vs 시뮬레이션 트윈
- **시뮬레이션 트윈(기본 제품):**
  - 장면 커밋에서 분기해 헤드리스로 배치 실행하며, 실시간보다 빠르다. 스팟 GPU를 쓰고 체크포인트를 자주 남긴다.
  - 인증용 재현은 D0 경로(MuJoCo CPU, N1–N5 통과 후 Newton 결정론 모드)로 돌린다(§4.1).
- **라이브 트윈(Athanor Live, P2부터):**
  - 고객 셀의 PLC·로봇·AMR 데이터를 엣지 게이트웨이로 받는다. OPC UA(open62541), MQTT, ROS 2(신규 배포는 Jazzy·Lyrical, 자체 브리지 + Zenoh)를 쓴다. Humble은 2027-05 EOL로 이후 보안 패치가 없으므로, Humble 고객 브리지는 M7 이후 best-effort로만 지원한다.
  - 데이터는 Kafka → 트윈 상태 서비스(W3C WoT 기술을 USD prim 경로에 매핑) → USD 라이브 세션 레이어(변환·관절 상태·신호만 덮어씀, 10–60 Hz)로 흐르고, 브라우저에는 WebSocket으로, 이력은 TSDB로 보낸다.
  - **용도는 셋이다.** ① 배포된 스킬의 인수 모니터링 ② 현장 실패 마이닝(실패 → 새 시나리오 → 재학습 → 게이트 재배포) ③ 트윈 충실도 드리프트 측정(fork-from-live → 예측 → 이후 라이브 데이터와 비교 → twin-fidelity score).
- **섀도·HIL 모드:** 실제 컨트롤러를 시뮬레이터에 lockstep 클록으로 물려 돌린다.
- **범위 제한:** 범용 IIoT 플랫폼을 만들지 않는다. Siemens·AVEVA·Dassault PLM 트윈과는 OPC UA·USD로 연결한다.

### 6.4 에이전트·MCP 레이어
- **자체 MCP 서버**(사양 2026-07-28)의 타입 지정·권한 관리 도구: `scene.search/query/diff/apply_ops`, `asset.search/certify`, `sim.run/sweep`, `sdg.generate`, `skill.train`, `eval.run`, `cert.issue`, `twin.query/forecast`, `dataset.export`, `order.quote`, `job.submit/status`.
- **인증서 발행 권한:** `cert.issue`는 에이전트가 단독으로 호출할 수 없다. 사람 승인 또는 Forge 서비스 계정 서명(Bronze 셀프서브 인증서)을 거쳐야 한다.
- **코드 생성:** USD Python은 gVisor·Kata 샌드박스 안에서만 생성한다. 커밋 전에 UsdValidation, 물리 정합성 검사(질량·관성, 상호 관통, 관절 한계), 2개 백엔드 스모크 테스트를 통과해야 하고, 병합은 사람이 승인한다.
- **모델 선택:** SaaS에서는 프런티어 API를 쓴다. 소버린 에디션에서는 온프렘 오픈 가중치 모델을 쓰며, 공공·국방 고객에게는 출처를 확인한 국산 모델을 우선한다(V8).
- **시나리오 출력:** OpenSCENARIO DSL로 제한해 재현성과 수출 가능성을 확보한다.
- **보안:** 임의 실행을 허용하는 커뮤니티 MCP(isaac-sim-mcp, blender-mcp 등)는 테넌트에 노출하지 않는다. ros-mcp-server는 테넌트 ACL 뒤에서만 쓴다. 개발 단계 API 그라운딩에는 kit-usd-agents를 쓴다.

### 6.5 GPU 풀 분리

| 풀 | GPU | 용도 | 규칙 |
|---|---|---|---|
| **RT 풀** | L40S, RTX PRO 6000 Blackwell(드라이버 R580 이상) | Isaac Sim RTX SDG, 고충실도 세션, 3DGUT 렌더, Kernel 경량 RL | 자체 서버 8 GPU(M5) + 8 GPU(M13, G1 통과 조건) = 16 GPU. 클라우드 버스트는 평균 3(P0) → 5(P1) → 8(P2) GPU, P2 최대 약 32 GPU. RTX PRO 6000 MIG는 [U]이므로 **세션당 GPU 1장 단위로 과금**한다 |
| **TRAIN 풀** | H100 / H200 / B200 | VLA·Cosmos 파인튜닝, 렌더링 없는 물리 RL | 네오클라우드 약 65k GPU-시간(24개월). **정부 B200/H200 배정분은 학습 전용이고 업사이드로만 잡는다.** RTX 센서 렌더링에는 절대 배정하지 않는다(RT 코어 없음) |
| **LIGHT 풀** | L4, CPU, 개발용 워크스테이션 | CI, 적합성 스위트, 웹 베이킹, MuJoCo CPU 재현 | — |
| **LAB EDGE** | Jetson AGX Thor, 테스트 셀 PC | 실셀 시험, 배포 검증 | 실측 데이터를 코퍼스로 직접 수집 |

- **스케줄링:** KAI 계층형 큐(테넌트 → 등급: 대화형·배치·학습). 유료 등급에는 보장 쿼터, 초과분은 선점형으로 운영한다.
- **격리:** 테넌트 간 시분할을 금지한다(같은 테넌트 작업끼리만 허용). 무료 프리뷰는 '비신뢰' 전용 노드 풀에서 돌린다. 데이터 거주 태그(KR/US/EU)를 스케줄러가 강제한다.
- **조달:** 국내 CSP(NHN, Naver, KT)의 RT GPU 공급, MIG 지원, R580 이상 이미지를 M2까지 확인한다(V4). 서울 하이퍼스케일러 리전은 미국 대비 23–38% 비싸다(AWS 서울 L40S $2.288/시간, RTX PRO 6000 $4.135/시간, 8×H100 $75.96/시간). 서울 리전은 지연이 중요한 대화형 세션에만 쓰고, 배치 작업은 자체 서버와 네오클라우드로 보낸다.

---

## 7. 로드맵 (36개월)

### 7.1 릴리스 트레인과 버전 규율
- **Train 1 (2026-12 ~ 2027-06):**
  - Zone F: Isaac Sim 6.1.x, Kit 110.x(번들 버전 [U]), Isaac Lab 3.x GA(GA 릴리스 노트에 명시된 Newton·Warp 핀)
  - Zone T: 같은 Newton 핀을 원칙으로 하되, 필요하면 Newton 1.6.x + Warp 1.18을 예외 승인한다. MuJoCo 3.15.x. mjlab 1.6.x는 MJWarp 3.11에 고정한 별도 이미지로 운영하고, 인증 재생은 MuJoCo 3.15 CPU에서 한다
  - 공통: 드라이버 R580 이상, OpenUSD 툴링 26.08
- **Train 2 (2027-07 ~ 2027-12), Train 3 (2028-01 ~ 2028-06), 이후 반기마다:** 분기 중간점검에서 보안 패치만 반영한다.
- **Isaac Sim 7.x 채택 조건:** GA와 패치 1회가 나온 뒤에 다음 트레인에서 채택한다. 그 전에는 사이드 브랜치에서만 쓴다.
- **ovrtx·ovphysx·NuRec 채택 조건:** 프로덕션 릴리스 + 서면 약관 + 적합성 스위트 통과.

### 7.2 단계별 계획

| 단계 | 산출물 | 종료 기준(게이트) | 데모 |
|---|---|---|---|
| **P0 Factory Zero** M1–M4 (2026.11–2027.02) | NVIDIA 서면 조건 요청(D0 이후 첫 주, 발송 D5 = 2026-10-23. 1차 회신 기한 M3, 최종 조건 M10). V1–V8 검증. CEN NeRF 파이프라인 라이선스 감사(1개월 차) 후 gsplat/3DGRUT로 이전 착수. SPDX 거부 목록 CI. **6–8주 베이크오프**(§14.3) → 작업 유형별 기본 백엔드 결정 메모와 Train 1 호환성 매트릭스. Sim Kernel API v0 + 적합성 스위트 v0(장면 C01–C05). Run Manifest v0(2026-11-06, W1)·장면 커밋 서비스·라이선스 레지스트리 v0(WS1 담당, P1부터 운영은 WS6·레지스트리 UI는 WS7). Forge v0(강체). Test Cell 1(코봇, 빈, 카메라 3대, F/T 센서: D1–30 BOM·견적 3건, 발주 2026-11-30, 시운전 D61–90) + 측정 프로토콜 v1. 앵커 LOI 3건. TIPS 운영사 확보. 바우처 공급기업 등록(2026.12–2027.01) | **G0 (M4, 심의 2027-02-26):** ① 베이크오프 결정 메모 완료 ② Silver/Gold 한국 SKU 150개 ③ 합성 전용 검출기 mAP 실데이터 대비 ≥0.85 ④ 인증 시험 결정론적 재현 100% ⑤ 첫 데이터셋 계약 체결(≥₩0.5억) ⑥ LOI 3건 ⑦ Sim Architect 채용 확정(미확정 시 §8.4의 대체 경로) | **M4: "휴대폰 영상에서 로봇 피킹까지 48시간"**(내부 팩토리 기준). 한국어 명령으로 셀 장면을 구성·랜덤화 |
| **P1 Outcome MVP + Studio Beta** M5–M12 (2027.03–2027.10) | Forge v1(관절 물체, VBD 폴리백, 온프렘 촬영·재구성 키트: 카메라 반입 제한 사이트용). DATA 라인(M5–M8 Cosmos Transfer 2.5, M9부터 Cosmos 3 Nano 16B 파인튜닝 + 라벨 일관성 QA). SKILL 라인(그래스프 RL, Mimic + SmolVLA/GR00T 파인튜닝, Jetson 수출). **12주 Cell-to-Policy PoC** 판매 개시(M5). Outcome Orchestrator v1. 사내용 MCP 에이전트. **Athanor Studio 베타**(M9, 디자인 파트너 대상, Zone T 전용: 브라우저 뷰어, Newton·MuJoCo 템플릿, Bronze Forge 셀프서브. Explorer는 대기자 명단 초대제·주간 상한, 공개 가입은 M15 GA). Test Cell 2. Crucible v0(시뮬 과제 25개, 실셀 2개, 내부 전용). 마켓플레이스 'Certified' 등급. Arena 헌장 초안(M8) → 공동서명 MOU(M10, 2027-08-27) → 헌장 서명(M12 초). Product Lead 착석(M8, 서치 M4). ISMS-P·ISO 27001 착수(M6). Series A ₩80억(M5 전환 브리지 ₩20억 → M10 ₩30억 → M12 ₩30억) | **G1 (M11, 심의 2027-09-24):** ① 유료 결과물 고객 ≥3(그중 양산·연간 계약 ≥1) ② NVIDIA 서면 조건 확보, **또는** 테넌트·온프렘을 허용형 전용으로 운영한다는 결정 확정 ③ 결과물 라인 총마진 ≥50%(완전원가 기준¹) ④ 측정권 부여 고객 ≥2 ⑤ Arena 공동서명 기관 MOU ⑥ 3개 피킹 과제에서 sim-to-real 갭 ≤15%p ⑦ 결과물당 엔지니어 시간 P0 대비 −50%. **불충족 시 보수안(§9.3)으로 전환: 인원 24–26명 동결, Wave 2 축소** | **M12: 공개 "K-Pick Challenge"(2027-10-22)**: 로봇 OEM 3곳의 정책을 시뮬과 실셀에서 동시에 채점(외부 채점은 공동서명 기관 입회. 헌장 서명 전이면 순위 없는 공개 시연) |
| **P2 Productize, Live & Sovereign** M13–M24 (2027.11–2028.10) | Studio GA(M15, 생산화 게이트를 통과한 FORGE·DATA 라인부터). 셀프서브 학습 템플릿. **Athanor Live**(커넥터, fork-from-live, 첫 라이브 트윈은 M18 앵커 셀). **Crucible v1 + 외부 Arena**(M18, 공동서명·헌장 서명 완료 후): 휴머노이드·양팔 트랙과 휴머노이드 셀. VLA 데이터 팩(Mimic + 텔레옵). **Athanor Sovereign**: 온프렘 베타 설치(M14) → GA(M18, 허용형 코어, RTX는 BYOL). MIG 테넌시(검증 시). GS 인증(동결 릴리스, M18). ISMS-P 취득(M18). 조건부 PhysX SDK 어댑터(§3.4). **미국 데이터·평가 GTM**(M15, 원격 우선). 일본 PoC 준비 | **G2 (M18, 심의 2028-04-28):** 첫 온프렘 유료 설치, 반복매출 비중 ≥30%, 정부재원 매출 비중 ≤40%. **G3 (M24, 심의 2028-10-27):** ① 계약 ARR ≥₩20억² ② 직전 분기(2028 Q3) 혼합 총마진 ≥55%² ③ 해외 데이터·평가 계약 ≥3 ④ 5개 과제에서 갭 ≤10%p ⑤ sim/real r ≥0.8(정책 패밀리 ≥8개, Fisher 95% CI 병기 [A]) ⑥ Silver/Gold 자산 4,000개 ⑦ Series B 착수 | **M18:** 휴머노이드 제조사 3곳이 참여하는 Arena v1 출범. 라이브 셀 트윈에서 한국어로 재배치 what-if를 실행해 예측 처리량과 실측을 비교. **M24:** 셀프서브 "영상 투입 → 인증 트윈과 피킹 스킬, 당일 산출" |
| **P3 Scale, Maritime·Defense, Global** M25–M36 (2028.11–2029.10) | (트리거 충족 시. M25는 트리거 판정 개시 시점이며 기본 경로는 확정 ₩5억 이상 앵커 계약, §5.4) 해양·조선 인식 팩: Fossen, Chrono FSI, 검증된 레이더·EO/IR 프로파일, COLREG 시나리오 500개. Athanor Air-gap 국방 에디션(M27–). Chrono 오프로드 UGV, PX4 드론(국방 에디션 내부). Chrono·Fossen·PX4 SITL 경로는 D0 목록 등록 후에만 인증(§4.1). Cosmos 3 Super 기반 정책 사전 선별. 셀프서브 SKILL 라인. 미국 법인(M24–M27). 일본 고객. 국내 OEM의 미국 공장(HMGMA, Hanwha Philly) 추종 | **M36:** ① 2029 매출 ₩110억 ② ARR ₩70억 ③ 반복매출 ≥50% ④ 해외 매출 ≥27% ⑤ 총마진 ≥60% ⑥ NRR ≥120% ⑦ Arena 인증서를 인용한 조달·PO 누적 ≥3건 ⑧ Silver/Gold 자산 12,000개 | **M30:** 실제 선박 로그로 해양 인식 팩 검증(합성 90% 이상으로 학습한 검출기의 해상 벤치마크). **M36:** 에어갭 랙에서 촬영 → 학습 → 평가 전 과정을 네트워크를 물리적으로 끊은 채 실행 |

¹ **라인 총마진(G1·생산화 게이트):** [10 §6.4](10-business-model-gtm.md)의 완전원가 정의를 쓴다. 라인 매출에서 컴퓨트·토큰 원가, 인건비(개입·FDE·Skill·Forge 시간, head-month ₩1,400만 환산), 랩·현장 원가, 크레딧 이행 원가, 인수 리스크 충당금을 빼고 라인 매출로 나눈다. 직접원가 마진은 이 지표로 쓰지 않는다.

² **G3 판정 기준:** 'ARR ≥₩20억'은 M24 시점 서명된 반복 계약의 연환산 금액(계약 ARR, 정부재원 제외)이다. '총마진 ≥55%'는 직전 분기(2028 Q3) 혼합 총마진이다. 둘 다 2028년 연간 목표(혼합 총마진 약 52%, 연말 인식 ARR ₩20억, §10.6)와 구분한다.

- 게이트 심의일은 모두 금요일이다(G0 2027-02-26, G1 2027-09-24, G2 2028-04-28, G3 2028-10-27). 단계 막대는 월 단위(M1 = 2026.11) 그대로 둔다.

---

## 8. 조직·공수

### 8.1 역할 × FTE (각 단계 말 인원, CEO 제외)
기존 CEN 인력 6명(NeRF 2, SDG·렌더링 1, 웹 워크스페이스 1, 마켓플레이스·플랫폼 1, ML 1)을 M1에 재배치한다고 가정한다[A]. 예산에는 재배치 인력의 인건비를 모두 포함했다.

| 역할(워크스트림) | 소유 범위 | P0 (M4) | P1 (M12) | P2 (M24) | P3 (M36) | 책임자 |
|---|---|---|---|---|---|---|
| 리더십: Sim Architect(CTO 트랙), Head of Fidelity & Evaluation, Product Lead(P1, 서치 M4·착석 M8), US GM(P3) | 아키텍처, 인증 체계, 제품 | 2 | 3 | 3 | 4 | CEO |
| WS1 Sim Kernel & Physics | Kernel API, 어댑터, 적합성 스위트, Warp 커널, sysid 도구, Newton 업스트림 | 3 | 4 | 4 | 5 | CTO |
| WS1-M 차량·해양 동역학 | Chrono, FMI, Fossen. Mobility Pack α(M18–M24) | 0 | 0 | 1 | 2 | CTO |
| WS2 Athanor Forge | 신경 재구성, 기하·SimReady, 생성형 3D·관절 ML | 2 | 4 | 5 | 6 | Forge Lead |
| WS3 센서·렌더링·SDG | RTX 센서, Warp Sensor Library, 센서 프로파일, 렌더 티어 | 1 | 2 | 3 | 4 | CTO |
| WS4 Fidelity Science & Crucible | sim-to-real 과학자, 지표, sysid, Arena 프로그램 | 1 | 2 | 3 | 4 | Head of Fidelity |
| WS4-L 촬영·랩 운영 | 촬영 기술자, 로봇 테크니션 | 1 | 2 | 2 | 3 | Head of Fidelity |
| WS5 Athanor Skill | RL, IL·VLA, 인식, Jetson 배포 | 2 | 3 | 4 | 5 | Skill Lead |
| WS6 Platform, MLOps & Sovereign | K8s/KAI, 컨트롤 플레인, 미터링, 게이트웨이, 보안, 에어갭 패키징, SBOM | 1 | 2 | 4 | 5 | Platform Lead |
| WS7 Studio UX, Agent & Marketplace | 브라우저(WebGPU/WebGL2) 클라이언트, MCP 에이전트, 마켓플레이스, 라이선스 레지스트리 UI | 1 | 2 | 3 | 4 | Product Lead(M8 착석 전 CTO 대행) |
| WS8 Solutions/FDE & 콘텐츠 | 현장 배치 엔지니어, 테크니컬 아티스트, 버티컬 팩 | 1 | 1 | 2 | 3 | CEO |
| WS9 BD, 얼라이언스, 정부과제, 라이선스·법무, 글로벌 GTM | NVIDIA 협상, 과제, 계약, 미국 BD(M15부터) | 1 | 1 | 2 | 3 | CEO |
| **합계** | | **16** | **26** | **36** | **48** | |

- **P0 배치(각주):** 기존 CEN 마켓플레이스·플랫폼 인력 1명은 WS1에 배치해 Run Manifest(v0 2026-11-06)·장면 커밋 서비스·라이선스 레지스트리 백엔드를 맡긴다(Kernel 리드 대행). WS6의 P0 1명은 신규 K8s 엔지니어(M3)다. P1부터 이 서비스들의 운영은 WS6가, 레지스트리 UI는 WS7이 맡는다. WS4의 P0 1명은 sim-to-real 과학자(M4 착석)다.
- **WS1-M 공백 대응:** WS1-M 1명은 '차량·해양 동역학 엔지니어(Chrono, FMI, Fossen)'로 M16에 서치를 시작해 M18에 착석한다(늦어도 M20). 공백 기간에는 CTO 설계 메모(M17)와 WS1·WS3가 어댑터 골격을 맡는다. 단계 말 인원과 564 HM은 변하지 않는다.
- **가격표 v1.0(M1) 책임:** CEO와 CFO(기존 경영지원)가 맡는다.
- **예산용 평균 인원(채용 지연 3–6개월 반영):** P0 11명(44 HM), P1 20명(160 HM), P2 30명(360 HM). **24개월 합계 564 head-month**(§9와 일치).
- **인원 상한:** G1 통과 전까지 26명, G2 전까지 32명. 공격안은 G1을 강하게 통과하고 Series A가 ₩100억 이상일 때만 적용한다.

### 8.2 공수 배분(P1–P2 엔지니어링 시간)
- **해자 35%:** Forge, Fidelity Lab, Crucible, 인증서
- **생산 라인 20%:** DATA, SKILL
- **Studio·에이전트·오케스트레이션·플랫폼 20%**
- **엔진 통합과 업그레이드 세금 15%:** 엔진에 닿는 워크스트림(WS1, WS3, WS6) 용량의 25%를 고정 예약한다.
- **고객 딜리버리(FDE) 10% 이하:** FDE는 결과물 매출 ₩8억당 1명으로 상한을 둔다.
- **P0 배분:** 웹·멀티테넌트 엔지니어링은 거의 하지 않는다. 내부 팩토리에는 필요 없기 때문이다. Kernel, 베이크오프, Forge, 랩에 집중한다.

### 8.3 채용 순서
1. **Sim Architect(CTO 트랙)**: Isaac Lab, Newton, OpenUSD 경험자. M1에 서치를 시작해 M3까지 확정한다. **게이팅 조건**이다.
2. **Head of Fidelity & Evaluation**: 실제 로봇 랩을 운영해 본 sim-to-real 과학자. M4까지 확정한다. **게이팅 조건**이다.
3. Warp/CUDA 물리 엔지니어 2명(M2–M4)
4. BD·정부과제·라이선스 매니저(M1)
5. 촬영·랩 테크니션(M2)
6. RL/IL 엔지니어(M3)
7. K8s GPU 플랫폼 엔지니어(M3)
8. 제조 배경의 FDE(M4)
9. WS4 sim-to-real 과학자(M4 착석)
10. 이후: Product Lead(서치 M4, 착석 M8), 센서·렌더링 엔지니어(M6, 게임사 출신), VLA 엔지니어(M6), 생성형 3D·관절 ML 엔지니어(M6), 웹·에이전트 엔지니어(M8), Arena 프로그램 매니저(M10), 보안·소버린 패키징 엔지니어(M12), OPC UA·라이브 트윈 엔지니어(M13), 미국 BD 리드(M15), 차량·해양 동역학 엔지니어(서치 M16, 착석 M18, Mobility Pack α 담당), 국방 보안 책임자(M26)

### 8.4 한국 시니어 인재 확보 전략
- **현실 가정:** 시뮬레이션 아키텍트, Warp/CUDA 접촉 물리, RTX 센서 엔지니어는 채용이 3–6개월 늦어진다고 보고 인건비를 산정했다.
- **게이팅 대체 경로**
  - Sim Architect가 M3까지 확정되지 않으면 원격 재미 한인 아키텍트를 분할 근무(fractional)로 투입하고 G0를 최대 2개월 늦춘다.
  - Head of Fidelity가 M4까지 확정되지 않으면 KAIST·SNU 교수를 겸직 Chief Scientist로 두고 시니어 sim-to-real 엔지니어를 붙인다. 이 경우 Crucible 외부 출범도 늦춘다.
- **인재 풀**
  - 재미 한인·원격 인력: NVIDIA, Google DeepMind, Meta, Tesla, Boston Dynamics 출신. 분기마다 서울에 체류한다.
  - 국내 게임사(Nexon, NCSoft, Krafton, Pearl Abyss): 실시간 그래픽·센서 렌더링.
  - Samsung Research, NAVER LABS, Hyundai 로보틱스 출신.
  - KAIST, SNU, POSTECH, UNIST 로봇 연구실의 박사후연구원과 겸직 교수.
  - ADD 출신: 센서·레이더.
- **보상:** 시니어 기본급 ₩1.2–1.8억 이상[U]. 핵심 10명을 위한 스톡옵션 풀(발행주식의 약 8–10% [A]). 원격 근무 프리미엄은 인당 단가에 반영했다.
- **흡인 요인:** Newton 업스트림 커밋 권한, 공개 벤치마크, CoRL·ICRA 논문, 오픈소스 적합성 스위트. 지원자에게 '정상급 엔진 생태계의 기여자'라는 경력 가치를 준다.
- **제도:** KOITA 인정 기업부설연구소를 활용한 전문연구요원, 해외 우수인력 유치 프로그램[U].
- **완충:** 비핵심 작업(웹 프런트엔드, 테크니컬 아트)은 외주로 채용 지연을 흡수한다.

---

## 9. 예산 (24개월, M1–M24, KRW)

### 9.1 가정 [A]
- **인건비 단가:** 완전부담 기준 head-month당 ₩1,400만(혼합). 리서치 중간값은 전원 엔지니어 기준 ₩1,495만이다. 우리 팀은 약 15%가 테크니션·운영·BD여서 단가가 낮고, 시니어 원격 프리미엄을 반영했다. 법정부담(4대보험 + 퇴직금) 1.18배와 인당 연 ₩2,500만 간접비를 포함한다. 급여 밴드는 낮은 신뢰도[U]다.
- **Head-month:** 44(P0) + 160(P1) + 360(P2) = **564**. 채용 지연 3–6개월을 반영했다.
- **GPU 단가:**
  - RT 클라우드 혼합 $2.3/시간: RunPod RTX PRO 6000 $2.09, L40S $1.09, 국내 CSP, AWS 서울 $4.135(지연 민감 세션만)의 가중평균.
  - TRAIN $3.5/시간: 네오클라우드 H100 $2.89–3.99.
  - 자체 RTX PRO 6000 8-GPU 서버는 대당 약 ₩1.6억[A]. 1호기는 베이크오프 결과를 본 뒤 M5에, 2호기는 G1을 통과하면 M13에 산다.
- **정부 GPU:** B200/H200 배정분은 학습 전용이고 **예산에 넣지 않는다**(업사이드).
- **NVAIE 예비비:** 산출물 면제가 거부되는 최악의 경우를 RT 풀 실제 규모로 산정했다. P0–P1은 14 GPU, P2는 최대 32 GPU로 잡아 약 46 GPU-year × $4,500(리스트 가격 [U]) ≈ ₩2.9억이다. Inception 75% 할인[U]이 적용되면 약 ₩0.7억이 된다.
- **API 변동 대응:** 엔진에 닿는 워크스트림 용량의 25%를 인건비 안에서 예약한다(약 ₩6억 상당).

### 9.2 기준안: 항목 × 단계 (₩억)

| 항목 | 산정 근거 | P0 (M1–M4) | P1 (M5–M12) | P2 (M13–M24) | **24개월 합계** |
|---|---|---|---|---|---|
| **인건비** | 564 HM × ₩1,400만 | 6.2 | 22.4 | 50.4 | **79.0** |
| 컴퓨트: 자체 RT 서버 | 8-GPU RTX PRO 6000 × 2대 | 0.0 | 1.6 | 1.6 | 3.2 |
| 컴퓨트: 코로케이션·전력 | | 0.0 | 0.2 | 0.4 | 0.6 |
| 컴퓨트: RT 클라우드 버스트 | 약 112k GPU-시간 × $2.3 | 0.3 | 1.0 | 2.3 | 3.6 |
| 컴퓨트: TRAIN 풀 | 약 65k GPU-시간 × $3.5 | 0.1 | 0.9 | 2.2 | 3.2 |
| 컴퓨트: 개발 워크스테이션·CI | RTX 5090급 등 | 0.5 | 0.6 | 0.3 | 1.4 |
| 컴퓨트: 스토리지·이그레스 | 멀티모달 프레임 100만 장당 약 5.5 TB | 0.1 | 0.3 | 0.8 | 1.2 |
| 컴퓨트: 서울 파일럿·스트리밍 세션 | AWS 서울·국내 CSP | 0.0 | 0.2 | 0.6 | 0.8 |
| **컴퓨트 소계** | | **1.0** | **4.8** | **8.2** | **14.0** |
| 라이선스: NVAIE 예비비 | 46 GPU-year × $4,500 [U] | 0.0 | 0.9 | 2.0 | 2.9 |
| 라이선스: 개발 도구·보안·LLM API | | 0.2 | 0.6 | 0.5 | 1.3 |
| **라이선스 소계** | | **0.2** | **1.5** | **2.5** | **4.2** |
| **법무·IP·인증** | 라이선스 자문·NVIDIA 협상·데이터권 1.0, 특허 0.6, ISMS-P/ISO 27001 0.8, GS 0.4, KTL/TTA 시험성적서 0.4, 침투 테스트 0.3 | 0.6 | 1.2 | 1.7 | **3.5** |
| **Fidelity Lab** | 코봇 테스트 셀 2개 2.4, 휴머노이드·양팔 셀(파트너 리스) 1.2, 촬영·측정 키트(온프렘 키트 포함) 1.0, 랩 공간 1.6, 소모품·Jetson Thor 0.6 | 1.6 | 2.6 | 2.6 | **6.8** |
| **GTM·관리** | 행사·Arena 출범 1.5, 출장·일본 PoC·미국 GTM 1.3, 헤드헌팅 수수료 1.4, 일반관리 1.3 | 0.8 | 1.8 | 2.9 | **5.5** |
| **소계** | | **10.4** | **34.3** | **68.3** | **113.0** |
| 예비비(8%) | | 0.8 | 2.7 | 5.5 | 9.0 |
| **총계** | ≈ USD 8.7M | **11.2** | **37.0** | **73.8** | **122.0** |

### 9.3 변형안 비교 (₩억, 24개월)

| 항목 | **보수안(Lean)** | **기준안(Base)** | **공격안(Aggressive)** |
|---|---|---|---|
| 발동 조건 | G1 미충족, 또는 Series A 총액(브리지 ₩20억 포함) < ₩60억 | 기본 계획 | G1을 강하게 통과(양산 계약 ≥2, ARR 경로 확인) + Series A ≥ ₩100억 |
| 인원(M24 말) | 24–26명 동결 | 36명 | 46명 |
| Head-month | 492 | 564 | 692 |
| 인건비 | 68.9 | 79.0 | 96.9 |
| 컴퓨트 | 9.5(서버 1대) | 14.0 | 22.0(서버 3대, 미국 리전) |
| 라이선스 | 2.5 | 4.2 | 5.5 |
| 법무·IP·인증 | 2.5(GS는 P3로 연기) | 3.5 | 4.5 |
| Fidelity Lab | 4.6(휴머노이드 셀은 파트너 전용) | 6.8 | 9.0(해양 센서 리그, 셀 3개) |
| GTM·관리 | 3.5(미국 GTM은 M24 이후) | 5.5 | 9.0(미국 법인 M15) |
| 소계 | 91.5 | 113.0 | 146.9 |
| 예비비 8% | 7.3 | 9.0 | 11.8 |
| **총계** | **98.8 (≈99)** | **122.0** | **158.7 (≈159)** |
| 범위 변화 | Wave 2를 축소(Arena v1은 M24로), Sovereign GA는 M24로, 미국 GTM 연기 | §7 그대로 | 해양 트랙을 M18에 병행 착수, 미국 법인 M15, Studio GA를 M12로 앞당김 |

### 9.4 자금 조달 논리(정정된 수학)
- **24개월 창(M1–M24) 매출 목표:** 약 ₩48억(2027년 ₩15억 + 2028년 1–10월 약 ₩33억). 이 중 정부재원(바우처, 정부 데이터 구축 용역)은 약 ₩13억, 상업 매출은 약 ₩35억이다.
- **현금 회수:** 회수 지연 60–90일과 선금 구조를 반영하면 창 내 회수액은 약 ₩41억이다.
- **24개월 순현금 소요:** ₩122억 − ₩41억 ≈ **₩81억**.
- **조달 구성**
  - ① 기존 가용 현금 ₩15억 이상으로 P0를 충당한다[A]. CFO가 M1 첫 주에 확인하고, 미달 시 브리지를 M3로 앞당긴다. 월 단위로 보면 ₩15억은 M4에 약 ₩4억까지 내려가므로 M5–M8 운영 자금은 ②의 브리지로 보강한다.
  - ② **Series A ₩80억을 브리지 ₩20억(M5, Series A 전환 조건부, 할인 15–20%) + 1차 클로징 ₩30억(M10) + 2차 클로징 ₩30억(M12, G1 통과 연동)으로 받는다.** 증빙 KPI는 코퍼스 10k trial, Silver/Gold 자산 1,000개, 유료 결과물 고객 3곳 이상, 총마진 45% 이상, 측정권 고객 2곳, NVIDIA 조건이다. 월말 현금 저점은 M4 약 ₩4억, M9 약 ₩5억이다([09 §9.2](09-roadmap-organization-budget.md)).
  - ③ 합계 ₩95억으로 순소요 ₩81억을 덮고, M24 말 잔여 약 ₩14억(P2 말 월 소진 약 ₩6억 기준 약 2.3개월)이 남는다. 총액·순소요·M24 잔액은 납입 구조와 무관하게 같다.
  - ④ **Series B ₩250억(M25–M28)** 착수 조건은 G3다. Series B가 늦어지면 G2(M18) 시점에 보수안으로 전환한다.
- **정부 보조금(업사이드, 차감 금지):** Deep-tech TIPS(3년 최대 ₩15억 [U], 운영사 투자 ₩3억 이상), 초격차 1000+(최대 ₩6억 [U]), 컨소시엄 과제가 있다. 선정되면 런웨이가 늘어나며, 창 내 약 ₩13–16억으로 추정한다[A]. **선정 전에는 소요 자금에서 빼지 않는다.**
- **매칭 현금:** 중소기업 정부 R&D는 정부 부담이 최대 75%이므로 민간 부담 25% 이상(현금 일부 포함)이 필요하다. 이 부담은 기준안 인건비와 GTM 예산 안에서 충당한다.
- **바우처 처리:** 바우처는 '정부재원 매출'로만 잡고, 비희석 자금 추정치(리서치 ₩30–60억 [U])에는 넣지 않는다. 이중 계상을 막기 위해서다.

---

## 10. 사업모델·가격

### 10.1 원칙
- **컴퓨트는 원가 근처, 가치는 결과물과 인증서에서 받는다.** 뷰어·리뷰어 좌석은 무료·무제한이다.
- 모든 가격은 [A]이며 분기마다 실제 풀 원가로 재산정한다. 총마진 하한은 30%다. 하한에 못 미치는 스토리지·이그레스는 '원가 회수 품목'으로 따로 표시하고 자체 저장소 이전으로 하한을 맞춘다(§10.2).
- **NVIDIA 런타임에 닿는 모든 매출 라인**(호스팅 RTX 세션, 온프렘 RTX 번들, NuRec 기반 상품)은 **NVIDIA 서면 조건 마일스톤과 연동**한다. 서면 조건 전에는 해당 라인 매출을 계획에 넣지 않는다. 2027–2029 목표에는 이 라인을 넣지 않았다.

### 10.2 CEN 토큰(1 토큰 = ₩100 [A])

| 토큰 항목 | 가격 | 원가 근거 | 총마진 |
|---|---|---|---|
| RT GPU-시간(배치: 자체 서버·네오클라우드) | 60 토큰(₩6,000) | 자체 RTX PRO 6000 상각 + 전력, 가동률 60%에서 약 ₩1,600[A]. RunPod $2.09(₩2,926) | 51–73% |
| RT GPU-시간(서울 거주 대화형·데이터 거주) | 95 토큰(₩9,500) | AWS 서울 RTX PRO 6000 $4.135(₩5,789) | 약 39%(국내 CSP 단가는 [U]) |
| TRAIN GPU-시간(H100급) | 80 토큰(₩8,000) | 네오클라우드 $2.89–3.99(₩4,046–5,586) | 30–49%. 서울 하이퍼스케일러 H100($9.49/GPU-시간)은 쓰지 않는다 |
| LIGHT 시간(L4·CPU) | 20 토큰(₩2,000) | RunPod L4 $0.49(₩686), AWS 서울 L4 $0.99(₩1,386) | 31–66%. 무료 등급에는 월 5시간 포함 |
| 합성 이미지 | 래스터 ₩0.3, RTX 실시간 ₩1.5, 패스트레이싱 ₩15 | 리서치 하한(래스터 ≥$0.0001, RTX ≥$0.0005, 패스 ≥$0.005)의 약 2배 | — |
| 스토리지·이그레스 | ₩40,000/TB-월, ₩150/GB | 프레임 100만 장당 약 $126/월, 이그레스 약 $495 | 별도 미터링. 리서치 원가 기준 총마진 16–20%로 하한 30%보다 낮아 **원가 회수 품목**으로 분류한다. 자체 SeaweedFS·Ceph RGW 저장소로 옮긴 뒤 30%를 맞추고, 2027 Q1 재산정에서 실측 원가로 다시 판정한다 |

### 10.3 구독·에디션 SKU

| SKU | 가격 [A] | 포함 내용 | 시작 시점 |
|---|---|---|---|
| **Explorer** | 무료 | 브라우저 뷰어, MuJoCo CPU 샌드박스, Bronze Forge 변환 월 3회, LIGHT 5시간 | M9 대기자 명단 초대제(주간 승인 상한), 공개 가입은 M15 GA |
| **Builder** | 월 ₩99,000 / 워크스페이스 | 1,000 토큰, 템플릿 | M9(베타, Zone T 전용), M15 GA |
| **Team** | 월 ₩190만 | 편집 좌석 5석(리뷰어·뷰어 좌석은 무료·무제한), 25,000 토큰, 프라이빗 마켓플레이스 | M15 |
| **Enterprise VPC** | 연 ₩2억부터 | 국내 CSP 또는 고객 VPC, SSO, SLA, 예약 RT GPU 4장(Zone T 허용형 경로). RTX는 고객이 자기 계정·VPC에서 자기 라이선스로 직접 운영할 때만 BYOL로 연동한다. AICHEMIST가 운영하는 국내 CSP 테넌시에서는 NVIDIA 서면 확인(§14.2 #5) 전까지 RTX를 제공하지 않는다 | M15 |
| **Athanor Sovereign**(온프렘·국내 소버린 클라우드) | 플랫폼 연 ₩2.5억(16 GPU·20석 이하) + 초과 GPU당 연 ₩1,200만. 일반 거래 연 ₩4–8억 | 허용형 코어, 서명 SBOM, 텔레메트리 없음, 지원 SLA | 베타 M14, GA M18 |
| **Athanor Air-gap**(국방) | 연 ₩8–15억 | 오프라인 업데이트, 인증 지원, 상주 엔지니어 | M27 이후(트리거 조건부) |

- **셀프서브 인증서:** Bronze 셀프서브 인증서는 Forge 서비스 계정이 자동 서명한다. `cert.issue`는 에이전트가 단독으로 호출할 수 없다(§6.4).

### 10.4 결과물(Outcome) SKU와 구매자 ROI

| 결과물 | 가격 [A] | 인수 기준(계약서 명시) | 구매자 ROI 논리 [A] |
|---|---|---|---|
| **인증 트윈:** 물체 | ₩30만–150만(Bronze→Gold) | 인증 등급, 궤적·정지 자세 오차 임계 | 고객이 직접 모델링·물성 측정을 하면 물체당 엔지니어 1–3일이 든다 |
| **인증 트윈:** 셀·현장 | ₩3,000만–1.5억 | 지정 지표의 Scorecard 값 | 현장 측량과 CAD 정리에 드는 수 주의 작업을 대체한다 |
| **합성 멀티모달 데이터셋 팩** | ₩5,000만–2억 | 합성 전용이 실데이터 학습 mAP의 ≥90%, 또는 합성 + 실데이터 10%가 실데이터 100% 이상(첫 데이터셋 계약(M3–M4)은 하한 0.85·목표 0.90, §5.2) | 실데이터 수집·라벨링에 드는 장당 수백–수천 원과 수개월의 일정을 줄인다 |
| **Cell-to-Policy PoC**(12주, 고정가) | ₩1.5–2.5억, 선금 30%, 산출물 전용 | 지정 실셀에서 성공률, sim-to-real 갭 ≤15%p, 정책 5개 이상 r 보고. **책임 상한 = 계약 금액**. 운영 범위(조명·물체군) 명시 | 사내 RL·sim 팀 구성(시니어 3–4명 × 6–12개월)을 대체한다 |
| **양산 스킬 프로그램** | 연 ₩4–10억 + 런타임 로봇당 연 ₩300만 | 현장 KPI(피킹 성공률, 사이클 타임)와 재학습 SLA | 라인 정지·수작업 대체 효과로 산정(고객별) |
| **Crucible 평가 캠페인** | 정책 버전당 ₩2,000만–6,000만 | 신뢰구간이 붙은 성공률, sim/real r, 서명 리포트 | 실셀 시험 시간과 실패 리스크를 줄인다 |
| **Arena 회원** | 연 ₩3,000만(스타트업), ₩1억(대기업) | 공동서명 인증서, 리더보드 | 조달·투자 유치용 제3자 증빙 |
| **인증서 발급** | 자산 클래스당 ₩500만. 로봇-과제 인증서 ₩3,000만–1억 | Gold는 랩 실측 | 고객 내부 검증 절차를 대체한다 |

- **결과물 크레딧:** 결과물 계약 금액의 20–30%를 12개월 유효 CEN 토큰으로 구성한다(계약 금액 안). 토큰을 쓸 때 매출로 인식한다.
- **측정권 할인:** 측정권(페어드 데이터의 익명화 재사용)을 허락하는 고객은 10–20% 할인받는다. 첫 계약 3건에서 데이터권 조항을 시험한다.
- **재벌 내재화 대응 계약 조항:** PoC가 끝나도 Forge·Kernel·인증서 IP와 도구는 AICHEMIST 라이선스로 남는다. 고객이 받는 것은 산출물 사용권이다. 도구 이전은 별도 라이선스 SKU로 판다.

### 10.5 마켓플레이스
- **제3자 인증 자산:** 75/25 배분(수수료 25%). 모든 리스팅에 라이선스 매니페스트, 출처(촬영원, 동의, 익명화), 인증 등급, Run Manifest(데이터셋)를 붙인다.
- **기여자 로열티:** 중소 공장 등 촬영 기여자는 익명화된 촬영물이 재사용될 때 로열티를 받는다(데이터권 약관 기반).
- **비상업 품목:** 상업 워크스페이스에서 자동으로 차단한다.

### 10.6 매출 목표(연도별, ₩억, 목표치이며 예측 아님)

| 라인 | 2027 | 2028 | 2029 |
|---|---|---|---|
| Athanor Data(데이터셋 팩) | 5.0 | 11.0 | 22.0 |
| Athanor Skill(PoC, 양산 프로그램, 런타임) | 5.5 | 13.0 | 25.0 |
| Athanor Forge(인증 트윈·자산) | 1.5 | 5.0 | 10.0 |
| Athanor Crucible(평가, 인증, Arena) | 0.5 | 4.0 | 12.0 |
| Studio·Cloud(구독, 토큰, 마켓플레이스 수수료) | 0.5 | 5.0 | 16.0 |
| Athanor Sovereign·Air-gap 에디션 | 0.0 | 3.0 | 15.0 |
| 정부 데이터 구축·NRE 용역 | 2.0 | 4.0 | 10.0 |
| **합계** | **15.0** | **45.0** | **110.0** |
| 이 중 정부재원 매출(바우처, 정부 용역) | 6.0 (40%) | 9.0 (20%) | 12.0 (11%) |
| 이 중 해외 매출 | 0.0 (0%) | 4.0 (9%) | 30.0 (27%) |
| 반복매출 비중 | ~10% | ~30% | ~50% |
| 혼합 총마진 | ~45% | ~52% | ~60% |
| 연말 ARR | 3 | 20 | 70 |

- **하방·상방 시나리오(2029):** 하방 ₩60억(해외 지연, Wave 3 미발동), 상방 ₩150억(공격안 + 해양 앵커).
- **정부재원 상한:** 2028년부터 매출의 40% 이하로 관리한다. 바우처 매출은 별도 보고하고 상업 ARR에 넣지 않는다.
- **손익분기:** 기준안에서 2030년 중반(M44 전후)을 목표로 한다[A].

### 10.7 시장 규모: 바텀업 TAM/SAM/SOM (전부 낮은 신뢰도, 검증 필요)
- **쓰지 않는 수치:** 디지털 트윈 전체 시장(USD 21–25B → 2030년 약 USD 150B)은 기관마다 범위가 3–10배 다르므로 사업 규모 근거로 쓰지 않는다. 합성데이터 '도구' 시장은 약 USD 0.3–0.6B로 작다[U].
- **한국 SAM(바텀업):** 도달 가능한 기업 계정 약 50–100곳 × 평균 ACV ₩3–8억 ≈ **연 ₩150–800억(USD 11–57M)**.
  - 계정 구성[A]: 로봇 OEM·통합사 약 15, 재벌 계열 공장·AI팩토리 과제 약 20, 1·2차 제조 협력사 약 30, 물류·3PL 약 8, 조선·중공업 약 6, 방산·국방연구 약 5, 연구기관 약 10.
  - 중소기업·바우처 세그먼트 연 ₩20–40억 별도.
  - **단일 벤더의 한국 매출 상한은 ARR USD 20–30M 수준**(리서치 추정 [U]).
- **글로벌 SAM(바텀업):**
  - ① 로봇 파운데이션모델·휴머노이드 기업 약 40–60곳(Figure, Physical Intelligence, Skild, 1X, Agility, Apptronik, Field AI, Dyna, Genesis AI 등. 자금 규모는 [U]) × 외부 데이터·평가 지출 연 USD 1–3M ≈ USD 40–180M
  - ② 글로벌 로봇 OEM·통합사·AI팩토리 약 300곳 × USD 0.1–0.3M ≈ USD 30–90M
  - ③ 셀프서브 Forge·인증 자산·데이터셋(합성데이터 도구 시장의 일부) ≈ USD 30–60M
  - **합계 현재 약 USD 0.1–0.3B.** 휴머노이드 설비투자와 합성데이터 연 35–46% 성장[U]을 가정하면 2033년 USD 0.6–1.5B[A].
- **목표 매출과 요구 점유율(SOM 대신):** 2029년 매출 ₩110억(약 USD 7.9M), 연말 ARR ₩70억(약 USD 5M)은 한국 SAM 중간값의 약 14%와 글로벌 SAM의 0.6–2.1%를 점유해야 달성된다([02 §1.4](02-market-competition.md)). 목표에서 거꾸로 정의한 SOM은 순환 논리이므로 IR에서는 '요구 점유율'로 쓴다.

### 10.8 USD 100M ARR 경로와 라운드별 마일스톤 [A]

| 시점 | ARR | 해외 비중 | 성장 동력 | 라운드·증빙 KPI |
|---|---|---|---|---|
| 2027년 말 | ₩3억(~USD 0.2M) | 0% | 국내 결과물(데이터, PoC) | **Series A ₩80억(M5 브리지 ₩20억 + 본 클로징 M10·M12):** 유료 고객 ≥3, 코퍼스 10k, Silver/Gold 1,000, 총마진 ≥45%, 측정권 고객 2 |
| 2028년 말 | ₩20억(~USD 1.4M) | ~10% | 국내 양산 프로그램, Sovereign, 미국 데이터·평가 파일럿 | **Series B ₩250억(M25–M28):** 계약 ARR ≥₩20억*, 반복매출 ≥30%, 직전 분기 혼합 총마진 ≥55%*, 해외 계약 ≥3, NRR ≥110% |
| 2029년 말 | ₩70억(~USD 5M) | ~30% | 미국 FM·휴머노이드 데이터·평가, Arena 인증서 | — |
| 2030년 말 | ~USD 15M | ~50% | 글로벌 FM 계정 10곳 이상, Forge 셀프서브 글로벌 | Series C(USD 60–100M) |
| 2031년 말 | ~USD 40M | ~65% | 글로벌 계정 25곳 × 약 USD 1M, 마켓플레이스 | — |
| 2033년 | **~USD 100M** | **≥70%** | 한국 ~USD 25–30M(상한), 글로벌 데이터·평가 ~USD 45M, 셀프서브·마켓 ~USD 20M, 동맹국 소버린·국방(국내 프라임 경유) ~USD 10M | 후기 단계 또는 IPO |

- \* Series B 증빙 KPI의 ARR은 M24 시점 서명된 반복 계약의 연환산(계약 ARR, 정부재원 제외), 총마진은 직전 분기(2028 Q3) 혼합 총마진이다. 2028년 연간 목표(혼합 총마진 약 52%, 연말 인식 ARR ₩20억)와 구분한다(G3와 같은 정의, §7.2).
- **글로벌 구매자 세그먼트(명시):** 미국의 로봇 파운데이션모델·휴머노이드 기업이다. 상품은 VLA 시연 데이터 팩, 인증 자산, 제3자 평가(Crucible)이고, 다계정 연 USD 1–3M 계약을 노린다.
- **착수일:** M12–M15(2027.10–2028.01)에 원격 우선으로 시작한다. 미국 법인은 M24–M27에 세운다(공격안에서는 M15).

### 10.9 밸류에이션 논리
- **소프트웨어·데이터 인프라 멀티플을 받는 조건(2029년, Y3):**
  - 총마진 60% 이상
  - 반복매출 50% 이상
  - NRR 120% 이상
  - 결과물당 엔지니어 시간 연 50% 감소(P0 기준선 지수 100 대비 연율. P3 말 지수 15는 연 약 −51%)
  - 정부재원 매출 15% 이하
- 이 조건에 못 미치면 **서비스 멀티플(매출의 한 자릿수 초반 배수)**로 평가받는다. 그래서 위 다섯 지표를 이사회 KPI로 둔다(§13).
- **비교 기업**(Applied Intuition USD 15B 가치·ARR 약 USD 830M 추정, Scale AI 지분 49%를 약 USD 14.3B에 매각 등)은 모두 검증되지 않은 사전 지식이다[U]. IR 자료에는 '검증 필요' 표기와 함께만 쓴다.

---

## 11. GTM·정부과제·해외

### 11.1 앵커 고객과 구매자 유형별 조달 경로

| 구매자 유형 | 대상 예시 | 기본 배포 형태 | 벤더 등록·보안 심사 | 현장 촬영 제약 | 진입 상품 | 인증 요구 |
|---|---|---|---|---|---|---|
| 로봇 OEM | Doosan Robotics, Rainbow Robotics, HD Hyundai Robotics | 산출물 납품 → Enterprise VPC | 1–2개월 | 낮음(자사 랩) | Cell-to-Policy PoC, 데이터셋 | 계약서 인수 기준 |
| 재벌 계열 공장·AI팩토리 | Samsung, HMG, SK, LG 계열(SI 경유) | 산출물 → 온프렘(Sovereign) | 2–3개월(SI 벤더 등록) | **높음:** 카메라 반입 금지가 흔하다. **온프렘 촬영·재구성 키트(P1)** 필수 | 데이터셋, 셀 트윈, PoC | ISMS-P, ISO 27001, 보안 서약 |
| 1·2차 제조 협력사 | 자동차·전자·배터리 협력사 | 산출물, Studio | 1개월 | 중간 | 바우처 연계 결과물 SKU | — |
| 물류·3PL | CJ Logistics, Hyundai Glovis, Coupang [수요 미검증] | 산출물 → VPC | 1–2개월 | 중간 | 피킹 데이터셋, 스킬 | — |
| 조선·중공업 | HD Hyundai, Samsung Heavy, Hanwha Ocean | 온프렘 | 2–3개월 | 높음 | 작업장 셀 조작(Wave 1), 해양 인식(Wave 3) | 보안 심사, 온프렘 |
| 국방 | ADD, Hanwha Aerospace, LIG Nex1, KAI | 에어갭 | 6–12개월 이상 | 매우 높음 | Air-gap 에디션(P3) | 국방 보안, 수출통제 심사 |
| 공공 SaaS | 지자체, 공공기관 | CSAP 인증을 받은 국내 CSP 경유 | CSAP 요건 [U] | — | 공공 데이터 구축 | CSAP(국내 CSP 경유) |
| 글로벌 FM·휴머노이드 | 미국 로봇 FM·휴머노이드 기업 | 산출물(데이터, 평가) | 2–4주 | 해당 없음 | VLA 데이터 팩, Crucible 평가 | SOC 2 준비(P2–P3) [A] |

- **인증 일정:** ISMS-P·ISO 27001은 M6 착수, M18 취득. GS 인증은 동결 릴리스로 M18. CSAP는 공공 SaaS를 하게 되면 국내 CSAP 인증 CSP를 통해서만 대응한다.
- **채널**
  - NVIDIA Inception(즉시 가입) → NPN 파트너 등재(M10 목표) → HMG·Samsung·SK·Naver 피지컬 AI 프로그램에 공동 판매.
  - 그룹 SI(Samsung SDS, LG CNS, SK AX, Hyundai AutoEver, HD Hyundai 계열 IT)를 리셀러로 둔다. 판매 초점은 **재벌 본사가 아니라 공급망 협력사와 로봇 OEM**이다.
- **수요 검증:** TIPS 제출 전(M3)에 실명 LOI 3건(로봇 OEM, 조선 로보틱스, 물류 또는 AI팩토리)을 받는다. 첫 계약 3건에서 측정권 조항을 시험한다.

### 11.2 정부과제 맵과 일정
일반 원칙
- 우리 역할은 **대형 국가과제의 주관기관이 아니라 재벌·연구기관 주도 컨소시엄 안의 '시뮬레이션·합성데이터·로봇학습 인프라 공급자'**다.
- 공통 제안 키트(TRL 4→7, 제3자 검증 KPI)를 모든 과제에 재사용한다.
- 모듈별 중복 지원 방지 맵과 3책5공(연구자 1인당 동시 과제 제한)에 맞춘 인력 배치표를 함께 운영한다.

| 프로그램 | 일정(달력) | 우리 역할 | 지원받는 모듈 | 규모 [U] | TRL·KPI 주장 | IP·데이터 조건, 비고 |
|---|---|---|---|---|---|---|
| 자격·서류 정비 | 2026 Q4(M1–M2) | — | KOITA 기업부설연구소, 벤처 인증, IRIS·SMTECH 계정 | — | — | 대부분 부처 R&D의 전제 조건 |
| **Deep-tech TIPS** | 운영사 확보 2026 Q4, 제출 2027 Q1(M3–M5), 선정 예상 M6–M8 [A] | 단독 | **Forge + Sim Kernel + Fidelity Scorecard** | 3년 최대 ₩15억, 운영사 투자 ₩3억 이상 | TRL 4→7. 합성 mAP 비율, sim-to-real 갭 | 성과물은 수행기관 귀속. 매칭과 기술료 확인 |
| **AI 바우처**(NIPA, 공급기업) | 공급기업 등록 2026.12–2027.01, 공모 2027.01–03, **납품 M5–M8** | 공급기업 | 결과물 SKU(데이터셋, 셀 트윈) | 바우처당 약 ₩2–3억 | 실명 레퍼런스와 측정된 합성→실 결과 | 정부재원 매출로 별도 보고 |
| **데이터 바우처**(K-DATA, 공급기업) | 공급기업 등록 2026.12–2027.01, 수요 공모 2027.01–02 | 공급기업 | 합성데이터 가공 | 과제당 최대 약 ₩7,000만 | — | 마켓플레이스 콘텐츠와 연계 |
| **초격차 스타트업 1000+** | 공모 2027.02–03 예상 | 단독 | 사업화와 글로벌 트랙(미국·일본) | 3년 최대 ₩6억 | — | 빅데이터·AI 또는 로봇 분야로 신청 |
| **IITP** 피지컬 AI·디지털 트윈 R&D | 신규 과제 2027.01–04(IRIS) | ETRI·KAIST·SNU와 공동수행 | **센서 물리 라이브러리**(라이다·레이더·EO/IR 프로파일), 월드모델 증강 | 연 ₩2–10억 몫 | 레이더·EO/IR 오차 막대 공개 | 자체 해양·국방 센서 R&D를 지분 희석 없이 충당 |
| **K-Humanoid Alliance / KEIT 로봇 R&D** | 회원 가입 2026 Q4, 공모 2027 Q1–Q2 | 컨소시엄 참여 | **시연 데이터 팩토리 + 중립 평가(Crucible)** | 연 ₩3–10억 몫(추정) | 정책 sim/real r, 갭 %p | 컨소시엄 IP 약정 사전 협상 |
| **NIA AI 학습데이터 구축** | 2027 Q1–Q2 | 컨소시엄 주관 또는 참여 | 휴머노이드·조작 합성데이터셋 구축 | 컨소시엄당 연 ₩10–50억 | 데이터 품질 지표 | **데이터셋은 개방 조건을 수용하되 생성기·페어드 코퍼스는 독점으로 유지**(계약에 명시) |
| **MOTIE M.AX / AI팩토리 라이트하우스** | 2026–2027 상시 | 공급기업(SI가 주관) | 셀 트윈·합성 비전 | 과제당 ₩3–30억(추정) | 라인 KPI | SI와 경쟁하지 않고 협업 |
| **정부 GPU 배정**(B200/H200) | 2027 Q1 신청 | — | **학습 전용**(VLA, 인식, 물리 RL) | 현물 | — | RT 코어가 없어 RTX 렌더링 불가. 스타트업 접근성은 [U] |
| **DAPA 혁신 중소기업·국방 AI 데이터** | 2027 H2 준비, 실제 착수는 P3 | 공급기업 | Air-gap 에디션 | 프로그램 단위 수십억 원 | — | 에어갭 에디션, 수출통제, 국방 라이선스 프로파일이 전제 |
| **KIAT 국제공동 R&D, 수출바우처, NIPA KIC 실리콘밸리** | 2027–2028 | 단독·공동 | 일본·미국 파트너 PoC, 전시회 | 수출바우처 연 최대 약 ₩1억 | — | 미국 GTM 보조 |

- **매칭·현금 흐름:** 중소기업 정부 부담은 최대 75%이므로 민간 부담 25% 이상이 필요하다. 정산·지급 지연과 사후 기술료를 자금 계획에 반영한다. 보조금은 선정 후에만 런웨이에 더한다(§9.4).
- **중복성:** 같은 모듈을 두 과제에서 지원받지 않는다. 예를 들어 TIPS는 Forge·Kernel, IITP는 센서, KEIT는 Crucible로 나누고, 중복 매트릭스를 제안서마다 첨부한다.
- **AI 기본법 관련 정정:** AI 기본법(2026-01-22 시행)은 고영향 AI, 투명성, 생성물 표시 의무를 다룬다. **시뮬레이션 신뢰성(credibility)을 의무화하지 않는다.** 시뮬레이션 신뢰성 수요의 근거는 UN ADS 규정(WP.29, 2026년 6월 승인 [U])과 ISO 34505:2025다.

### 11.3 해외 진출 순서
1. **국내 레퍼런스 확보(2027):** 로봇 OEM 1, AI팩토리·물류 1, 조선 1의 실명 사례와 정량 사례 연구를 만든다.
2. **인증과 생태계 진입(2027 H2–2028 H1):** GS 인증, TTA·KTL 시험성적서, NVIDIA NPN 등재, 공개 벤치마크(K-Pick Challenge).
3. **미국 데이터·평가 GTM(M12–M15 착수, 원격 우선):** 로봇 FM·휴머노이드 기업에 VLA 데이터 팩과 Crucible 평가를 판다. 이것이 USD 100M 경로의 핵심이다(§10.8).
4. **일본(2028 H1 PoC):** 국내 협력사의 일본 공장, 노동력 부족에 따른 자동화 수요, AIRoA 로봇 데이터 컨소시엄[U]. KIAT·KOTRA를 활용한다.
5. **미국 산업 고객(2028–2029):** 국내 OEM의 미국 공장(HMGMA 조지아, Samsung Taylor, MASGA 관련 Hanwha Philly Shipyard [U])을 따라간다. 미국 법인은 M24–M27에 세운다.
6. **중동(2029 이후):** 국내 프라임 경유 G2G 스마트시티·국방 패키지. 건별로 수출통제(US EAR) 심사를 한다.

---

## 12. 리스크 레지스터 (Top 12)

| # | 리스크 | 가능성 / 영향 | 완화책 | 책임자 | 조기경보 지표 |
|---|---|---|---|---|---|
| 1 | **NVIDIA 약관:** 멀티테넌트 호스팅, 온프렘 재배포, 산출물 면제, NVIDIA 자산 번들, 텔레메트리 모두 미확인 | 높음 / 높음 | Zone F/T/S 경계(§6.2). D5(2026-10-23)에 서면 요청(§14.2). NVAIE 예비비 ₩2.9억. 테넌트·온프렘은 허용형 전용. RTX는 BYOL. 관련 매출 라인은 약관 마일스톤에 연동 | CEO + 얼라이언스·라이선스 매니저 | M3까지 서면 회신이 없으면 G1에서 '허용형 전용' 경로 확정 |
| 2 | **서비스화 함정:** 결과물 계약이 SI 업무로 변질되어 총마진이 희석됨 | 높음 / 높음 | 생산화 게이트(무개입 80%, 총마진 60%, 서면 라이선스). FDE 상한(매출 ₩8억당 1명). 결과물 크레딧. 결과물당 엔지니어 시간을 이사회 KPI로 | CEO | 분기 엔지니어 시간 지수가 목표 대비 20% 이상 초과 |
| 3 | **한국 시니어 채용 지연:** Sim Architect, Head of Fidelity, Warp/CUDA, RTX 센서 인력 | 높음 / 높음 | 지연 3–6개월을 예산에 반영. 게이팅 대체 경로(§8.4). 원격·재미 한인 채용. 게임사·연구실 풀. 스톡옵션 | CEO + CTO | M3에 Architect 미확정, M4에 Head of Fidelity 미확정 |
| 4 | **API 변동·버전 불일치:** Isaac Lab 3.x(쿼터니언 순서, ProxyArray), Newton 월간 릴리스, Warp R580, Kit 연간 약 3개 메이저, Isaac Sim 7.0 alpha | 높음 / 중간 | 반기 릴리스 트레인, 호환성 매트릭스, 적합성 스위트 CI, 엔진 접촉 워크스트림 용량 25% 예약, 7.x는 GA + 패치 1회 이후 채택 | CTO | 업그레이드에 계획 대비 1.5배 이상 공수 투입 |
| 5 | **라이선스 오염:** CEN NeRF 내 Instant-NGP 가능성, Hunyuan3D, Inria 계열, nvdiffrast, MimicGen, cuRobo, AGPL·GPL, SAM 군사 조항 | 중간(발견 시 높음) / 높음 | M1 감사, SPDX·거부 목록 CI, 마켓플레이스 출처 게이트, 국방용 화이트리스트, Apache 태그 cuRobo 고정 | CTO + 라이선스 자문 | 감사에서 차단 항목 발견. CI 차단 건수 > 0 |
| 6 | **충실도 미달·결과물 책임:** 접촉 집약·변형체 갭, 고객 하드웨어·조명 변수 | 중간 / 높음 | 인증 셀 또는 서면 프로토콜로 인수 정의, 책임 상한 = 계약 금액, 운영 범위 명시, M12 측정 전 변형체 보증 금지, 소량 실데이터 파인튜닝 포함 | Head of Fidelity | 갭 KPI 미달, PoC 인수 실패 |
| 7 | **GPU 등급·공급·서울 원가:** RT 공급 부족, RTX PRO 6000 MIG 미확인, 정부 GPU는 학습 전용 | 중간 / 높음 | 풀 분리, 국내 CSP RT 계약을 조기 확보(V4), 자체 서버 2대, 세션당 GPU 1장 과금, 서울 리전은 대화형 전용 | Platform Lead | RT 가동률 80% 초과 지속, 서울 단가 상승 |
| 8 | **NVIDIA 범용화·재벌 내재화·경쟁 진입:** usd-content-agents, 관리형 Isaac 클라우드, Lightwheel 한국 진출 | 높음 / 중간 | 측정·인증·한국 콘텐츠로 가치 이전, 협력사 집중, IP 라이선스 유지 조항, 재검토 트리거(관리형 Isaac 클라우드 한국 출시, Lightwheel 한국 영업 개시) | CEO | 트리거 이벤트 발생 |
| 9 | **데이터·측정권 거부로 코퍼스 해자 정체** | 중간 / 높음 | 측정권 할인 10–20%, 기여자 로열티, 자체 테스트 셀 trial, NIA 계약에서 생성기·코퍼스 독점 조항 확보 | BD + Head of Fidelity | 분기 측정권 고객 목표 미달 |
| 10 | **Arena 중립성·이해상충** | 중간 / 중간 | 공동서명 기관과 헌장 서명 전 외부 채점 금지(헌장 초안 M8 → MOU M10 → 서명 M12 초. 지연 시 K-Pick은 비순위 시연), 회피 규정, 프로토콜 공개, Arena 프로그램 분리 | Arena PM + 외부 공동서명 기관 | 회원사 이의 제기, 공동서명 MOU 지연(M10 초과) |
| 11 | **자금·정책 주기:** Series A 지연, 보조금 지급 지연, 매칭 현금, 바우처 의존 | 중간 / 높음 | 단계 게이트, 보조금은 업사이드, 정부재원 매출 2028년부터 40% 이하, 보수안 사전 설계 | CEO / CFO | M9까지 Series A 텀시트 없음 |
| 12 | **보안·센서·수출통제:** 스트리밍 무인증, 에이전트 RCE, 멀티테넌트 격리, 해양·국방 레이더 충실도, EAR·ITAR | 중간 / 높음 | 자체 인증·TLS 게이트웨이, host 네트워크 미노출, 테넌트 간 GPU 공유 금지, gVisor·Kata, GA 전 침투 테스트, 센서 검증 계획(§4.2), 국방 라이선스 프로파일, 건별 수출 심사 | Platform Lead + 센서 리드 + 자문 | 침투 테스트 고위험 발견, 센서 오차 목표 미달 |

---

## 13. KPI 트리 (단계별)

### 13.1 북극성 지표와 트리
- **북극성:** 인증된 결과물 매출(Certified Outcome Revenue). sim-to-real 점수가 붙어 인수된 결과물의 매출이다.
  - **기술 축:** 충실도(갭, r, mAP 비율, 센서 오차), 재현성, 처리량·원가(steps/s/$)
  - **제품 축:** 무개입 비율, 결과물당 엔지니어 시간, 셀프서브 전환, 에이전트 성공률
  - **사업 축:** 매출, 반복매출 비중, 총마진, NRR, 해외 비중, 정부재원 비중
  - **해자 축(감사 가능):** 코퍼스 규모, Silver/Gold 자산, 재사용률, 측정권 고객, 조달 인용, Arena 공동서명

### 13.2 단계별 KPI

| 축 | KPI | P0 (M4) | P1 (M12) | P2 (M24) | P3 (M36) |
|---|---|---|---|---|---|
| 기술 | 정책 sim-to-real 갭(%p) | ≤25(1개 과제) | ≤15(3개) | ≤10(5개) | ≤8(10개) |
| 기술 | 합성 전용 mAP 비율 | ≥0.85 | ≥0.90 | ≥0.95 | ≥0.95(3개 버티컬) |
| 기술 | sim/real Pearson r(정책 ≥5개, Fisher 95% CI 병기. G3 판정은 정책 패밀리 ≥8개 [A]) | — | ≥0.7 | ≥0.8 | ≥0.85 |
| 기술 | 라이다 거리 오차 | — | ≤3 cm | ≤2 cm | ≤2 cm + 레이더 프로파일 |
| 기술 | 인증 시험 결정론적 재현(D0 경로) | 100% | 100% | 100% | 100% |
| 기술 | 적합성 스위트(백엔드 × 장면, C01–C15 정본은 04 §4.6) | 3×5 | 4×8 | 5×12 | 6×15 |
| 제품 | Forge 무개입 비율 | 30% | 60% | 80% | 90% |
| 제품 | 영상 → 피킹 스킬 | 48시간(내부) | 24시간 | 당일(셀프서브) | 4시간 |
| 제품 | 에이전트 한국어 명령 성공률 | ≥80%(20개) | ≥85%(50개) | ≥90%(100개) | ≥92% |
| 제품 | 결과물당 엔지니어 시간 지수 | 100 | 50 | 25 | 15 |
| 제품 | 결과물 → 셀프서브 전환율¹ | — | 25% | 50% | 60% |
| 제품 | Studio 월간 활성 워크스페이스 | — | 30(베타) | 300 | 1,500 |
| 사업 | 계약·매출 | 첫 계약 ≥₩0.5억 | 2027년 ₩15억 | 2028년 ₩45억 | 2029년 ₩110억 |
| 사업 | 유료 결과물 고객(누적) | 1 | 6 | 18 | 40 |
| 사업 | 반복매출 비중 | — | ~10% | ~30% | ~50% |
| 사업 | 혼합 총마진 | — | ≥45% | ≥52% | ≥60% |
| 사업 | 정부재원 매출 비중 | — | ≤40% | ≤20% | ≤15% |
| 사업 | 해외 매출 비중 | — | 0% | ~9% | ~27% |
| 사업 | NRR | — | — | ≥110% | ≥120% |
| 해자 | 페어드 실측/시뮬 trial(누적) | 1k | 10k | 50k | 150k |
| 해자 | **Silver/Gold 자산(누적, Bronze 제외)** | 150 | 1,000 | 4,000 | 12,000 |
| 해자 | 그중 Gold(랩 실측) | 30 | 200 | 800 | 2,000 |
| 해자 | Bronze 자산(참고, KPI 아님) | — | 5,000 | 30,000 | 100,000 |
| 해자 | 2개 이상 주문에서 재사용된 자산 비율 | — | 20% | 35% | 45% |
| 해자 | 측정권 부여 고객(누적) | 0 | 4 | 12 | 25 |
| 해자 | Arena 회원 | — | 3(파일럿) | 8 | 20(해외 2 포함) |
| 해자 | 인증서 인용 조달·PO | — | 고객 PO 1건 | 공공·재벌 조달 1건 | 3건 |

¹ 2단 정의([06 §11.1](06-usability-and-agent.md)): P1에는 결과물 고객 가운데 Studio 베타 워크스페이스를 활성화한 비율로 재고, P2부터는 12개월 안에 크레딧 외 유료 토큰·구독을 쓴 비율로 잰다.

### 13.3 분기별 해자 KPI (투자자 보고용, 2027 Q1–2028 Q4)

| 분기 | 페어드 trial 누적 | Silver/Gold 누적 | 재사용률 | 측정권 고객 누적 | 엔지니어 시간 지수 | 거버넌스 마일스톤 |
|---|---|---|---|---|---|---|
| 2027 Q1 (M3–M5) | 1.5k | 200 | — | 0 | 100 | Arena 공동서명 기관 접촉. G0(M4) 통과 |
| 2027 Q2 (M6–M8) | 3k | 400 | 10% | 1 | 85 | 데이터권 계약 템플릿 확정. Arena 헌장 초안(M8) |
| 2027 Q3 (M9–M11) | 6k | 700 | 15% | 2 | 65 | 공동서명 MOU(M10, 2027-08-27). G1(M11, 2027-09-24) |
| 2027 Q4 (M12–M14) | 10k | 1,000 | 20% | 4 | 50 | 거버넌스 헌장 서명(M12 초, K-Pick Challenge 2027-10-22 이전. 지연 시 K-Pick은 순위 없는 공개 시연). 첫 KTL·TTA 시험성적서(지표 1개). 고객 PO가 인증서를 인수 기준으로 인용 |
| 2028 Q1 (M15–M17) | 18k | 1,600 | 25% | 6 | 42 | Studio GA(M15) |
| 2028 Q2 (M18–M20) | 28k | 2,300 | 30% | 8 | 36 | 외부 Arena v1 출범. G2(M18) |
| 2028 Q3 (M21–M23) | 38k | 3,100 | 33% | 10 | 30 | 시험성적서 지표 3개 확보 |
| 2028 Q4 (M24–M26) | 50k | 4,000 | 35% | 12 | 25 | 공공·재벌 조달 문서에 인증서 인용. G3(M24) |

### 13.4 제3자 검증 KPI(시험기관 명시)
- **시험기관:** KTL, KOLAS 인정 시험기관, TTA 중에서 지표별로 지정한다.
- **인증 대상 지표(P2 말까지 3개 이상):**
  - ① 합성 전용 mAP ÷ 실데이터 mAP
  - ② 정책 sim-to-real 갭(%p)
  - ③ 라이다 거리 오차(cm)
  - ④ 결정론적 재현율(%)
- 정부과제 제안서와 IR 자료에는 이 지표들만 '검증된 KPI'로 표기한다.

---

## 14. 실행 계획

**결정 사항(요약).** 주차별 실행 정본은 [12 §3–§5](12-execution-90days.md)다. 아래 표는 결정 기준과 큰 줄기만 담고, 12와 다르면 12를 따른다.
- **NVIDIA 서면 조건:** 요청서 발송 D5(2026-10-23), 1차 회신 기한 M3(2027-01), 최종 조건 기한 M10(2027-08). 회신이 없거나 부정적이면 G1에서 허용형 전용 경로를 확정할 수 있다.
- **베이크오프:** W1 2026-11-02 ~ W8 2026-12-27, 결정 메모 2027-01-08(2027-01 첫 주).
- **결정 규칙:** 작업 유형별로 성공률을 보정한 steps/s/$가 최대인 백엔드를 고른다. 차이가 10% 이내면 허용형 경로(Zone T 호환)를 우선한다.
- **기준일:** D0 = 2026-10-16(금, CEO 승인), D1 = 2026-10-19, D30 = 2026-11-17, D60 = 2026-12-17, D90 = 2027-01-16.

### 14.1 30/60/90일 실행계획 (D0 = 2026-10-16, CEO 승인일)

| 기간 | 핵심 실행 항목 | 산출물 | 책임 |
|---|---|---|---|
| **D1–30** (2026-10-19 ~ 11-17) | ① P0 ₩11.2억 승인·집행 ② Sim Architect·Head of Fidelity 서치 개시(리테인드 헤드헌터 + 재미 한인 네트워크) ③ NVIDIA Korea 서면 조건 요청서 발송(D5 = 10-23) + Inception 가입 ④ CEN NeRF 파이프라인 SPDX 감사 착수 + 거부 목록 CI 적용 ⑤ 앵커 3곳 타깃과 첫 데이터셋 고객 지정 ⑥ TIPS 운영사 접촉 ⑦ KOITA 연구소·벤처 인증·IRIS 계정 점검 ⑧ 국내 CSP 3사에 RT GPU·MIG·R580 견적 요청 ⑨ 베이크오프 W1–W2(이미지, 과제 명세, Run Manifest v0(11-06), 적합성 v0 C01–C05) ⑩ Test Cell 1 BOM 확정과 견적 3건(발주는 2026-11-30 = D43) ⑪ K-Humanoid Alliance 가입 신청 ⑫ 상표 검색 ⑬ CFO 가용 현금 확인(M1 첫 주)과 Series A 전환 브리지 협의 개시 | 요청서, 감사 착수 보고, 베이크오프 환경, 견적 3건 | CEO, CTO(대행), BD, CFO |
| **D31–60** (2026-11-18 ~ 12-17) | ① 베이크오프 W3–W6 ② gsplat/3DGRUT 이전 계획과 Forge v0 골격 ③ 장면 커밋 서비스·라이선스 레지스트리 v0(WS1), Test Cell 1 발주(11-30) ④ **AI·데이터 바우처 공급기업 등록(12월)** ⑤ TIPS 운영사 텀시트 ⑥ LOI 3건 초안 협의 ⑦ 첫 데이터셋 계약 제안(mAP 인수 조건) ⑧ Arena 공동서명 후보(KTL·KIRIA·TTA) 접촉 ⑨ 데이터권·측정권 계약 템플릿 ⑩ Cell-to-Policy PoC 오퍼 시트(인수 기준, 책임 상한) ⑪ NVIDIA 2차 미팅 ⑫ 상표 출원 | 바우처 등록 확인, 텀시트, 제안서, 오퍼 시트 | CTO, BD, Head of Fidelity(대행) |
| **D61–90** (2026-12-18 ~ 2027-01-16) | ① 베이크오프 W7–W8 → 결정 메모(2027-01-08) + Train 1 호환성 매트릭스 ② Test Cell 1 시운전, 측정 프로토콜 v1 ③ Forge v0로 첫 Silver 자산 50개 ④ **LOI 3건 서명** ⑤ TIPS 제출 패키지(TRL 4→7, 중복 매트릭스, 3책5공 배치표) ⑥ 첫 데이터셋 계약 서명(목표 M3–M4) ⑦ 바우처 수요기업 매칭 ⑧ G0 체크리스트 ⑨ Series A 데이터룸 골격과 KPI 대시보드 ⑩ 서울 RT 용량 계약 | 결정 메모, LOI, TIPS 패키지, 계약서 | CEO, CTO, BD |

### 14.2 NVIDIA 라이선스 협상 체크리스트
요청서는 NVIDIA Korea·Inception 담당자에게 서면으로 보내고, 답변도 서면(이메일 또는 계약서)으로만 인정한다.

| # | 항목 | 확인할 질문 | 우리가 원하는 결과 | 연동 결정 |
|---|---|---|---|---|
| 1 | 산출물 면제 | Isaac Sim, RTX, Replicator, NuRec로 생성한 데이터셋·영상·정책·USD 자산을 판매하고 마켓플레이스에서 재판매할 때 NVAIE가 필요 없는가 | 서면 확인 | Zone F 매출 전체, NVAIE 예비비 집행 여부 |
| 2 | 멀티테넌트 SaaS | Kit 앱과 Isaac Sim을 브라우저 스트리밍으로 제3자에게 제공할 때의 라이선스 형태(GPU당 / 동시 사용자당), NVAIE와 Omniverse Enterprise 중 무엇인가 | 가격표와 조건 | Zone T의 RTX 등급 출시 여부 |
| 3 | 가격 | NVAIE 리스트 가격($4,500/GPU/년 [U]), Inception 할인(75% [U]), 원화 견적, 클라우드 버스트 GPU 계산 방식 | 원화 서면 견적 | 예비비 ₩2.9억 조정 |
| 4 | 온프렘·에어갭 재배포 | Kit, Isaac Sim, ovrtx, ovphysx 바이너리, isaacsim/isaaclab 휠의 OEM·ISV 재배포 권리, 컨테이너 재배포, 에어갭 업데이트 | OEM 조건 또는 '불가' 확인 | Sovereign 에디션 RTX 번들(없으면 BYOL 유지) |
| 5 | BYOL 대행 운영 | 고객이 보유한 NVAIE 라이선스로 AICHEMIST 클라우드에서 대신 운영할 수 있는가 | 허용 여부 | Enterprise VPC의 RTX 옵션 |
| 6 | NVIDIA 자산 | SimReady, Isaac 자산, 텍스처를 데이터셋과 마켓플레이스에 번들·재판매할 수 있는가 | 범위 | 마켓플레이스 출처 규칙 |
| 7 | 텔레메트리 | Kit 익명 사용 데이터 비활성화, 에어갭 운용 | 비활성화 방법 | 국방·재벌 보안 심사 |
| 8 | cuRobo | Isaac Lab 설치본 cuRobo의 약관, Apache 태그 업스트림을 Isaac Lab 밖에서 써도 되는가, SkillGen 사용 | 서면 확인 | SkillGen 기능 활성화 |
| 9 | NuRec·3DGUT 컨테이너 | 성숙도, 라이선스, SaaS 사용 | 조건 | Forge·DATA 라인의 NuRec 도입 |
| 10 | ovrtx·ovphysx | GA 일정, 프로덕션 약관, ovstage 없이 ovphysx 소스를 빌드해도 되는가 | 로드맵과 조건 | Kit-less RTX 채택, PhysX 어댑터 대안 |
| 11 | 모델 약관 | GR00T N1.7 Open Model License(상업 파인튜닝, 파인튜닝 가중치 재배포, 군사 조항), Cosmos 3 OpenMDW-1.1(귀속·가드레일·사용 분야), Cosmos Transfer 2.5 | 서면 해석 | VLA 등급, 국방 프로파일 |
| 12 | Isaac Teleop·CloudXR | SaaS 텔레옵 라이선스 | 조건 | 테넌트 텔레옵 경로 |
| 13 | 파트너 프로그램 | Inception → NPN 등급, HMG·Samsung·SK·Naver 공동 판매, 얼리 액세스, SI 계열사와의 채널 충돌 | 파트너 계약 | GTM 채널 |
| 14 | 로드맵·안정성 | Isaac Sim 7.x·Kit의 API 동결 약속, LTS 계획, Isaac Lab 3.x GA 일정 | 일정 | 릴리스 트레인 |
| 15 | 국내 RT 용량 | NVIDIA 경유로 국내 CSP(Naver, KT, NHN)의 RTX PRO 6000·L40S를 확보할 수 있는가 | 연결 | RT 풀 조달 |
| 16 | 수출통제 | 중동·국방 고객 대상 GPU·모델 가중치의 EAR 지침 | 가이드 | Wave 3 해외 |

- **협상 원칙:** 서면 회신이 없거나 부정적이어도 사업은 계속된다(Zone T/S는 허용형 전용). NVIDIA에는 'GPU 사용량을 늘리는 파트너'로 포지셔닝한다. 독점 조항은 받아들이지 않는다.
- **시한:** 발송 D5(2026-10-23, D0 이후 첫 주). M3(2027-01)까지 1차 서면 회신, M10(2027-08)까지 최종 조건. M11 G1(2027-09-24)에서 '조건 확보' 또는 '허용형 전용 확정' 가운데 하나로 결정한다.

### 14.3 6–8주 엔진 베이크오프 계획 (W1 = 2026-11-02 ~ W8 = 2026-12-27, 결정 메모는 2027-01-08)
- **하드웨어(동일 이미지, 드라이버 R580 이상, CUDA 13):** RTX PRO 6000 Blackwell Server 1장, H100 1장(클라우드), SDG 단가 비교용 L40S 1장. 국내 CSP 이미지 1종에서 같은 이미지를 재현해 검증한다.
- **백엔드**
  - B1: Newton 1.6.x 단독(MJWarp, Kernel v0 경유)
  - B2: Isaac Lab 3.x(GA, 출시 지연 시 EA) Kit-less Newton(번들 핀 사용)
  - B3: Isaac Lab 3.x + PhysX(Isaac Sim 6.1, Zone F)
  - B4: MuJoCo 3.15 CPU(레퍼런스)
  - B5: mjlab 1.6.0(MJWarp 3.11 고정 이미지)
  - 오프라인 기준: Drake v1.57(삽입 접촉)
  - 선택: Genesis 1.4.3(2개 과제만, 관찰 목적)
  - **PhysX SDK 소스 어댑터는 아직 없으므로 베이크오프 대상이 아니다.**
- **과제(11개 + SDG):**
  - T1 G1 속도 추종(평지·험지), T2 BeyondMimic 모션 클립, T3 Franka 큐브 들기, T4 LEAP/Allegro 손안 재배치
  - T5 빈 피킹(한국 SKU 클러터), T6 폴리백 피킹(VBD), T7 페그·커넥터 삽입(SDF/hydroelastic, Drake 대조), T8 케이블 삽입
  - T9 천 접기(선택), T10 Kamino 폐루프 그리퍼, **T11 휴머노이드 + 양손 덱스터러스(60 DoF 초과) 스트레스 테스트**
  - SDG: 래스터·RTX·패스트레이싱 이미지/초/GPU(RTX PRO 6000 vs L40S)
- **측정 지표:**
  - 처리량: env-steps/s, 보상 임계 도달 벽시계 시간, VRAM, steps/s/$(온디맨드·스팟)
  - 이전성: 백엔드 간 정책 이전 편차. Zone F 정책은 Newton → PhysX → MuJoCo CPU 3개, Zone T/S 정책은 Newton ↔ MuJoCo CPU 2개 백엔드로 잰다. Tier 1(1,000 에피소드, 성공률 차 ≤10%p)과 Tier 2(초기조건 200개, 쌍별 ≤5%p·관절 RMSE ≤0.05 rad [A])를 함께 기록한다(§4.1)
  - 결정론: 반복 롤아웃 비트 일치(Newton 결정론 모드 N1–N5 시험, MuJoCo CPU), GPU 간(RTX PRO 6000·H100·L40S) 재현성
  - 실제 이전: Test Cell 1에서 T3·T5 실셀 성공률(셀 준비 시)
- **주차별 계획**

| 주 | 작업 |
|---|---|
| W1 | 이미지·드라이버·국내 CSP 검증, 과제 명세, Run Manifest v0, 측정 하네스 |
| W2 | 적합성 스위트 v0(C01 낙하 박스, C02 진자, C03 Franka 픽, C04 폴리백, C05 바퀴 차량) × 5개 실행 구성(B1–B5) |
| W3–W4 | 처리량 스윕(환경 1k–16k), VRAM, steps/s/$ |
| W5–W6 | 보상 임계까지 학습, 백엔드 간 이전, Drake 대조(T7) |
| W7 | 결정론(Newton N1–N5)·GPU 간 재현성, SDG 처리량, T11 스트레스 테스트 |
| W8 | 실셀 이전(가능 시), **결정 메모(2027-01-08 서명)**: 작업 유형별 기본 백엔드 매트릭스, Train 1 호환성 매트릭스, GPU 풀 사이징 수정안, 토큰 원가 갱신 |

- **결정 규칙:**
  - 작업 유형별로 '성공률을 보정한 steps/s/$'가 최대인 백엔드를 기본으로 정한다. 단, 적합성 스위트를 통과하고 sim2sim 이전 편차가 허용치 안이어야 한다.
  - 차이가 10% 이내면 **허용형 경로(Zone T 호환)를 우선**한다.
  - 벤더가 발표한 처리량 수치는 의사결정 근거에서 뺀다.
- **예산과 책임:** 클라우드 약 ₩0.4억(P0 컴퓨트 안). 책임은 CTO(대행)와 Kernel 리드.

---

## 15. 검증 필요 항목

다음 항목은 리서치 단계에서 1차 출처로 확인하지 못했다. **이사회, IR, 정부과제 제출에 쓰기 전에 반드시 재검증한다.** 담당과 기한을 함께 적는다.

| # | 항목 | 현재 상태 | 영향 | 검증 방법 | 기한 |
|---|---|---|---|---|---|
| 1 | NVIDIA SaaS 호스팅·산출물 면제·온프렘 재배포·텔레메트리 약관 | 미확인(가장 중요) | Zone 경계, 매출 라인 | 서면 회신(§14.2) | M3 1차, M10 최종 |
| 2 | NVAIE·Omniverse Enterprise 가격($4,500/GPU/년), Inception 75% 할인 | 미확인 | 예비비 | 원화 견적 | M2 |
| 3 | NuRec·3DGUT 컨테이너의 성숙도·라이선스(GA 여부 포함) | 미확인 | Forge·DATA | NVIDIA 서면 | M3 |
| 4 | OpenMDW-1.1 전문, GR00T Open Model License(파인튜닝 가중치 고객 납품 = 재배포), openpi 가중치 약관, SAM License(SAM 3D Objects·SAM 3)·VGGT-1B-Commercial 재배포·군사 조항 | 미확인 | VLA 등급, Zone T 호스팅 추론, Zone S 가중치 번들, 국방 | 법률 검토(V7) | M3 |
| 5 | 국내 CSP의 RT GPU(L40S, RTX PRO 6000) 공급·가격, MIG, R580 이미지 | 미확인 | RT 풀, 토큰 원가 | 견적·실측(V4) | M2 |
| 6 | 정부 GPU 배정 규칙(스타트업 접근성, 허용 워크로드) | 미확인 | TRAIN 업사이드 | NIPA·MSIT 문의 | M4 |
| 7 | Deep-tech TIPS(₩15억), 초격차(₩6억), AI 바우처(₩2–3억), 데이터 바우처(₩7,000만) 상한과 2027 공고 일정 | 중간·낮은 신뢰도 | 정부과제 맵 | IRIS·K-Startup·NIPA 공고 | 각 공고 시 |
| 8 | 2027 정부 예산안의 피지컬 AI·AI팩토리·휴머노이드 항목, K-Humanoid 작업패키지 개방 여부 | 미확인 | 컨소시엄 전략 | 예산안·부처 문의 | M2 |
| 9 | 시니어 급여 밴드(₩1.2–1.8억 이상) | 낮은 신뢰도 | 인건비 단가 | Wanted·Remember·헤드헌터(V5) | M2 |
| 10 | 260k GPU 딜 배분, HMG 약 USD 3B 클러스터 | 중간 신뢰도 | IR 서사 | 공식 보도자료 | IR 전 |
| 11 | Samsung의 Rainbow Robotics 지분 약 35%(시점 상충) | 중간·낮은 신뢰도 | 앵커 서술 | DART 공시 | IR 전 |
| 12 | 경쟁사 가치평가·ARR(Applied Intuition USD 15B·ARR 약 USD 830M 추정, Skild 등), Lightwheel 지역 거점 | 미확인 | 밸류에이션 서사 | 1차 보도·공시 | IR 전 |
| 13 | 시장 규모(디지털 트윈 USD 21–25B, 합성데이터 USD 0.3–0.6B, 로보틱스 시뮬 USD 1–3B) | 낮은 신뢰도 | TAM 서사 | 최신 애널리스트 보고서 | IR 전 |
| 14 | GAUGE·GPUSimBench 수치, SDQM r 약 0.87 | 미확인(arXiv 차단) | 충실도 서사 | 원문 확인 | M2 |
| 15 | Newton의 sim2real 사례(Unitree G1, Skild 랙 조립, Samsung 케이블 삽입) | NVIDIA·파트너 발표(중간 신뢰도) | 기술 서사 | 독립 검증 논문(CoRL 2026 등) | M3 |
| 16 | Newton '하드웨어 간 이식 가능 결정론' 주장과 결정론 모드 N1–N5 시험 | 미시험 | 인증서 정책(D0 경로 편입) | 베이크오프 W7 | M3 |
| 17 | RTX PRO 6000 MIG(최대 4분할)와 세션당 약 $0.84/시간 원가 | 미확인 | 세션 가격 | 실측 | M4 |
| 18 | Isaac Lab 3.x GA 날짜와 GA 기준 Newton·Warp 핀 | 2026년 10월 말 목표 | 릴리스 트레인 | GA 릴리스 노트 | GA 시 |
| 19 | Isaac Lab Kit-less 모드에서 Mimic·Teleop·TacSL 동작 여부 | 미확인 | 테넌트 기능 범위 | 사내 시험 | M6 |
| 20 | Blender 별도 프로세스 번들 GPL 해석, ovstage 대체 가능성, ArduPilot | 미확인 | 소버린 번들 | 법률 의견(V2) | M3 |
| 21 | MinIO(AGPL-3.0 [U]) 여부, SeaweedFS·Ceph RGW(LGPL) 라이선스와 의무 | [U] | 소버린 번들 | SPDX 확인 | M2 |
| 22 | UN ADS 규정(WP.29, 2026년 6월 승인), ISO 34505 수용 범위, 국내 Level-4·자율운항선박 성능검증의 시뮬레이션 인정 범위 | 미확인 | Wave 3 수요 | 규정 원문, KATRI·KRISO 문의 | M12 |
| 23 | 국내 물류(CJ, Coupang, Glovis)·조선사의 실제 수요와 데이터 공유 의사 | 미검증 | Wave 1 | LOI, 인터뷰 | M3 |
| 24 | AICHEMIST의 현재 현금, 기존 CEN 인력 재배치 가능 인원(6명 가정), 기존 CEN NeRF 구성요소 | 내부 확인 필요 | P0 자금, 인력 | CFO·CTO 내부 점검 | M1 |
| 25 | 명칭 'Athanor' 상표 충돌 | 미확인 | 브랜드 | KIPRIS·USPTO·EUIPO | M2 |
| 26 | Korea–US MASGA 투자 규모(USD 150B), Hanwha Philly 관련 수요 | 중간 신뢰도 | 미국 진출 서사 | 공식 자료 | IR 전 |
| 27 | Isaac Sim 6.1에 번들된 PhysX·Kit 버전(공개 SDK 5.11, kit-app-template 110.3.0과 같은지) | 미확인(릴리스 노트 접근 차단) | 호환성 매트릭스, Run Manifest 표기 | Isaac Sim 6.1 릴리스 노트·컨테이너 확인 | 베이크오프 W1 |
| 28 | Newton 1.6.1의 최소 Warp 버전(Warp 1.16 수용 여부) | 미확인 | 이중 핀 필요성, GPU·드라이버 하한 | pyproject 확인 | 베이크오프 W1 |
| 29 | Drake PyPI 휠에 번들된 서드파티 솔버 약관('Other/Proprietary') | 분류만 확인 | Zone S 번들 범위 | 법률 의견(V2) | M3 |
| 30 | Chrono CPU·클린룸 Fossen·PX4 SITL lockstep의 반복 비트 일치(D0 등록) | 미시험 | 차량·선박·드론 인증 범위 | N1–N4 동등 시험 | Chrono M22, Fossen M28 [A] |
| 31 | ROS 2 Humble EOL(2027-05) 이후 고객 브리지 보안 영향 | 일정은 확인 | 라이브 트윈·엣지 게이트웨이 | 고객별 배포 현황 점검 | M6 |

---

## 16. 문서 간 정합 결정 (Errata, v1.1)

01–12와 부록을 대조하며 찾은 불일치와 DR 자체의 기술 정정을 아래와 같이 확정한다. 이 표는 본문보다 우선하며, 본문의 해당 위치에도 같은 내용을 반영했다. '반영 문서'의 숫자는 문서 번호다.

| # | 항목 | 결정 | 반영 문서 |
|---|---|---|---|
| 1 | 학습 템플릿 배분 | 템플릿 ID 마스터는 06 §6.2(RL-/IL-/PE-), 팩별 배분 마스터는 08 §7.1. P0 RL 3종(팔 도달·큐브 들기, 빈 피킹(한국 SKU), 디팔레타이징)은 모두 조작 팩. 휴머노이드(G1 속도 추종·모션 추적)·사족(속도 추종)·덱스터러스(손안 재배치, 상태 기반)는 P1(M6–M12)에 처음 편입. 드론 PX4 SITL 기본 템플릿은 P2(M20–M24) RL 1종, 상업화는 P3 국방 에디션. P2 상업화는 휴머노이드·덱스터러스만, 사족은 템플릿·Crucible 평가로만 수익화 | DR v1.1·§4.4, 06, 07, 08 |
| 2 | 적합성 장면 정본 | 04 §4.6의 C01–C15 번호·장면·허용치가 정본. 05의 S 번호는 폐기하고 C 번호 대응표만 둔다. 05에만 있는 장면은 C16+ 확장 후보. 허용치 최종값은 베이크오프 결정 메모(2027-01-08)에서 고정 | DR §3.3·§4.1·§13.2·§14.3, 04, 05 |
| 3 | C01 낙하 박스 허용치 | 연속 해석해 대비 ≤3 mm, 또는 이산 적분기 해 대비 ≤1e-6 m로 판정. 반암시적 Euler의 1 m 낙하 오차가 약 ½·g·dt·t = 2.2 mm(dt = 1 ms)이므로 기존 1e-4 m는 어떤 백엔드도 통과할 수 없다 | 04, 05 |
| 4 | 적합성 백엔드 증설 | P0 Newton/MJWarp·MuJoCo CPU·Isaac Lab PhysX(3) → P1 + Drake(4) → P2 + Chrono(5) → P3 + 클린룸 Fossen 6-DOF(6, C13). FMU는 공동 시뮬레이션 브리지라 백엔드 수에서 제외. 조건부 PhysX SDK 어댑터(§3.4)는 착수 시 추가 백엔드로 셈. P0 '3 × 5'의 3은 B1–B5 중 Newton/MJWarp 계열·PhysX·MuJoCo CPU의 통과 백엔드 수 | DR §3.4·§4.1, 04, 05 |
| 5 | sim2sim 게이트 | 07 §7.3의 2단 구조가 정본. 교차 백엔드는 Zone F 3개(PhysX·Newton·MuJoCo CPU), Zone T/S 2개(Newton·MuJoCo CPU, PhysX SDK 어댑터 편입 시 3개). Tier 1(모든 수출 정책, 차단): 1,000 에피소드, 성공률 차 ≤10%p, 평균 반환 비율 ≥0.85, 지연·노이즈 후 하락 ≤15%p, ONNX 행동 최대 오차 ≤1e-3. Tier 2(인증서·Crucible 공식 캠페인): 초기조건 200개, 쌍별 ≤5%p, 관절 RMSE ≤0.05 rad. KPI '적용률 100%'는 Tier 1 기준. 베이크오프 '이전성' 지표도 같은 구분 | DR §4.1·§4.4·§14.3·부록, 04 §4.7, 05, 07 |
| 6 | 결정론 등급·D0 경로 | Run Manifest 필드 `D0_bitwise`/`D1_statistical`/`D2_generative`/`none`으로 정본화. Newton 결정론 모드는 N1–N5 시험(베이크오프 W7) 통과 후 D0 편입. Chrono CPU·클린룸 Fossen(Warp CPU)·PX4 SITL lockstep은 N1–N4 동등 시험 통과와 CTO 등록 후에만 인증 경로(목표 Chrono M22, Fossen M28 [A]). 등록 전 산출물은 D1 '통계적 재현', Scorecard만 납품하고 인증서는 자산·센서 항목에 한정. 변형체 산출물은 D1이며, MuJoCo CPU로 D0 재현한 정적 보정 시험 항목에만 'experimental' 인증서. 입상체·유체는 인증 제외 | DR §4.1·§6.3·§7.2·§15·부록, 01, 04, 05, 08 |
| 7 | Gold 오차 KPI | 'Gold 자산 질량/마찰 오차'는 자동 Forge 추정값(VLM 사전분포 + 영상 sysid)의 Gold 랩 실측 대비 상대오차 \|θ_auto − θ_lab\| / θ_lab(05 §16.1 D4). Gold 인증서에는 랩 실측값과 측정 불확도를 기록하고, KPI 수치를 인증 임계나 고객 보증 문구로 쓰지 않음. 시험기관 비교 지표는 'Gold 랩 실측 재현성' | DR §4.1, 01, 05, 11 |
| 8 | 엔진 릴리스 채택 기한 | P1 45일, P2 이후 30일 안에 사이드 브랜치에서 검증 완료 후보로 만들고, 프로덕션 반영은 다음 릴리스 트레인. KPI '채택 지연'도 같은 정의 | DR §1.4·§4.1, 01, 02, 03 §12.5, 10 |
| 9 | PhysX Vehicle2 구역 | Zone F(Isaac Lab·Isaac Sim 경유) 전용. Zone T/S의 AMR은 Newton 관절형 휠 모델, 차량은 Chrono::Vehicle. 테넌트·온프렘 개방은 PhysX SDK 소스 어댑터(X6) 또는 Mobility α 설계 메모(M17)의 C++ 바인딩 결정 이후 | DR v1.1·§2 #6·§4.1·§5.5·§6.2, 01, 03, 04, 08, 부록 A |
| 10 | 일정 기준일 | D0 = 2026-10-16(금, CEO 승인), D1 = 10-19, D30 = 11-17, D60 = 12-17, D90 = 2027-01-16. 베이크오프 W1 2026-11-02 ~ W8 2026-12-27, 결정 메모 2027-01-08. 게이트 심의일 G0 2027-02-26, G1 2027-09-24, G2 2028-04-28, G3 2028-10-27. 공동서명 MOU 2027-08-27, K-Pick Challenge 2027-10-22(모두 금요일). 단계 막대는 월 단위(M1 = 2026.11) 유지 | DR 머리말·§7.2·§14·부록, 01, 09, 12 |
| 11 | NVIDIA 서면 조건 요청 | '1주 차'는 D0 이후 첫 주이며 발송일은 D5(2026-10-23). 1차 회신 기한 M3(2027-01), 최종 조건 기한 M10(2027-08) | DR §0·§7.2·§12·§14, 02, 12 |
| 12 | Test Cell 1 | D1–30에 BOM 확정·견적 3건, 발주 2026-11-30(D43), 시운전과 측정 프로토콜 v1은 D61–90 | DR §7.2·§14.1, 05, 12 |
| 13 | Cosmos 시점 | P1 DATA 라인은 M5–M8 Cosmos Transfer 2.5(라벨 일관성 QA 동일), M9부터 Cosmos 3 Nano 16B 파인튜닝(§2 #13이 §7.2보다 우선) | DR §4.2·§7.2, 01, 05, 07 |
| 14 | Product Lead·가격표 | Product Lead는 M4 서치, M8 착석. 그 전까지 WS7 책임은 CTO 대행. 가격표 v1.0(M1)은 CEO와 CFO(기존 경영지원) 책임 | DR §7.2·§8.1·§8.3, 01, 06, 09, 10 |
| 15 | WS1-M 직무·시점 | '차량·해양 동역학 엔지니어(Chrono, FMI, Fossen)', 서치 M16, 착석 M18(늦어도 M20). 공백은 CTO 설계 메모(M17)와 WS1·WS3가 어댑터 골격 담당. 인원·예산 고정값 불변 | DR v1.1·§8.1·§8.3, 08, 09 |
| 16 | P0 소유권·인력 배치 | 재배치된 CEN 마켓플레이스·플랫폼 엔지니어 1명은 WS1(Kernel 리드 대행)에서 Run Manifest·장면 커밋 서비스·라이선스 레지스트리 백엔드 담당. Run Manifest v0는 2026-11-06(W1). P1부터 운영은 WS6, 레지스트리 UI는 WS7. WS6 P0 1명은 신규 K8s 엔지니어(M3), WS4 P0 1명은 sim-to-real 과학자(M4 착석). 단계 말 인원과 564 HM 불변 | DR §7.2·§8.1·§8.3·§14.1, 04, 09, 12 |
| 17 | Series A 납입 구조 | ₩80억 = M5 Series A 전환 조건부 브리지 ₩20억(할인 15–20%) + M10 1차 ₩30억 + M12 2차 ₩30억(G1 연동). 기존 현금 ₩15억은 M4에 약 ₩4억까지 내려가므로 브리지로 보강, 월말 저점은 M4 약 ₩4억·M9 약 ₩5억. CFO가 M1 첫 주에 현금 확인, 미달 시 브리지를 M3로. 총액·순소요 ₩81억·증빙 KPI·M24 잔액 약 ₩14억 불변. 부록의 'M9–M12'는 본 클로징 구간. 이번 달 승인 요청에 ⑥ 브리지 협의·현금 확인, ⑦ 보수안 자동 전환 규칙과 중단·축소 기준(09 §3.7a)의 이사회 사전 결의 추가 | DR §0·§9.4·§10.8·부록, 01, 09, 10 |
| 18 | G3 판정 기준 | 'ARR ≥₩20억'은 M24 시점 서명된 반복 계약의 연환산(계약 ARR, 정부재원 제외). '총마진 ≥55%'는 직전 분기(2028 Q3) 혼합 총마진. 2028년 연간 목표(혼합 총마진 약 52%, 연말 인식 ARR ₩20억)와 구분. Series B 증빙 KPI도 같은 정의 | DR §7.2·§10.8, 09, 10, 11 |
| 19 | 라인 총마진 | G1과 생산화 게이트의 '라인 총마진'은 10 §6.4의 완전원가 정의(컴퓨트·토큰, 인건비(개입·FDE·Skill·Forge 시간, HM ₩1,400만 환산), 랩·현장, 크레딧 이행, 인수 리스크 충당금 차감). 직접원가 마진은 쓰지 않음 | DR §0·§4.3·§7.2, 09, 10, 11 |
| 20 | Arena 거버넌스 헌장 | 헌장 초안 M8 → 공동서명 MOU M10(2027-08-27) → 헌장 서명 M12 초(K-Pick Challenge 2027-10-22 이전). 지연 시 K-Pick은 공동서명 기관 입회 아래 비순위 공개 시연. §13.3의 '2027 Q4 헌장 서명'은 이 일정으로 해석 | DR §5.3·§7.2·§12·§13.3, 01, 02, 07, 09, 11 |
| 21 | Studio·Explorer 베타와 좌석 | M9 베타는 Zone T 전용, Explorer는 대기자 명단 초대제(주간 승인 상한). 공개 가입과 Studio GA는 M15. Team '5석'은 편집 좌석이며 리뷰어·뷰어 좌석은 무료·무제한. Bronze 셀프서브 인증서는 Forge 서비스 계정이 자동 서명하고, `cert.issue`는 에이전트 단독 호출 불가 | DR §4.3·§6.4·§7.2·§10.3, 01, 06, 10 |
| 22 | 결과물 → 셀프서브 전환율 | P1은 결과물 고객 중 Studio 베타 워크스페이스 활성화 비율, P2부터는 12개월 안에 크레딧 외 유료 토큰·구독을 쓴 비율(06 §11.1의 2단 정의) | DR §13.2, 06, 10, 11 |
| 23 | 엔지니어 시간 KPI | '결과물당 엔지니어 시간 연 50% 감소'는 P0 기준선(지수 100) 대비 연율. P3 말 지수 15는 연 약 −51% | DR §4.3·§10.9, 10, 11 |
| 24 | 스토리지·이그레스 단가 | ₩40,000/TB-월·₩150/GB는 리서치 원가 기준 총마진 16–20%로 하한 30% 미달. '원가 회수 품목'으로 분류하고 자체 SeaweedFS·Ceph RGW 이전 후 30% 달성, 2027 Q1 재산정에서 실측 원가로 재판정 | DR §10.1·§10.2, 10 |
| 25 | Wave 3 트리거 | 기본 계획의 2028년 말 ARR은 ₩20억이므로 M25 착수는 확정 ₩5억 이상 앵커 계약(조선사 공동개발 또는 국방 과제) 경로로만 가능. ARR ₩30억 경로는 2029년 중 충족. M25는 트리거 판정 개시 시점, 국방 Air-gap은 M27부터. 2029년 Air-gap 약 ₩4.5억은 앵커 계약 전제 [A] | DR §0·§5.4·§7.2·부록, 01, 02, 08, 10 |
| 26 | 차량 문구·자동차 선택지 | '자동차는 안 한다'로 읽히는 v1.1 이전 문구를 정정. 도로 자율주행 HIL·인증 도구 시장과는 정면 경쟁하지 않되 차량 트윈 자체는 만든다(Mobility Pack α: 야드·저속 차량 동역학과 도로 시나리오 재생, M18–M24). 선택지는 ① α + 표준 연결(채택) ② 승용 ADAS 트윈 확장(조건부, X14 또는 NRE) ③ 도로 AV 시뮬레이터 자체 구축(기각) | DR §0·§1.2·§5.1·§5.4·§5.5, 01, 02, 08 |
| 27 | 첫 데이터셋 인수 기준 | 첫 데이터셋 계약(M3–M4)의 인수 하한은 합성 전용 mAP 비율 0.85(P0 KPI), 목표 0.90. 데이터셋 팩 정가 계약(P1 이후)은 0.90 | DR §5.2·§10.4, 05, 10 |
| 28 | mjlab 버전 고정 | mjlab은 MJWarp 3.11에 고정한 별도 이미지로 운영하고, 인증 재생은 MuJoCo 3.15 CPU에서 한다 | DR §2 #1·§7.1·§14.3, 03, 07 |
| 29 | [T-2] Replicator·테넌트 SDG | Replicator는 NVIDIA 독점(Kit·Omniverse 약관), Zone F 산출물 전용(서면확인 필요). 테넌트 SDG는 Newton Warp 래스터 + Warp Sensor Library(Zone T·S, OK). Apache-2.0·OK는 RF-DETR N–L에만(XL/2XL은 PML 1.0) | DR §2 #17·§4.4·§6.2, 03, 04, 07 |
| 30 | [T-3] 드론·차량 폴백 라이선스 | Pegasus 포팅은 Isaac Sim 런타임 의존이라 Zone F·BYOL 전용. BeamNG.tech와 고객 CarSim/CarMaker FMU는 BYOL이며 'OK' 대상 아님 | DR §2 #6·#7, 03, 08 |
| 31 | [T-4] Zone T/S 라이선스 구성 | '100% 허용형'을 '허용형(Apache-2.0/BSD/MIT)과 의무 이행이 가능한 약한 카피레프트(MPL-2.0: open62541·Selkies·OpenBao·Lichtblick, EPL-2.0: Ditto, LGPL: Ceph RGW)'로 정정. TSL·BSL·AGPL·GPL·비상업 제외. TimescaleDB는 Apache-2.0 에디션만 쓰거나 InfluxDB 3 Core로 대체. 03 §10.2 분류 흐름에 '약한 카피레프트: 의무 추적' 분기 추가 | DR §0·§2·§6.2, 01, 03, 04, 11 |
| 32 | [T-5] SAM·VGGT·GR00T 가중치 | SAM License(SAM 3D Objects·SAM 3)와 VGGT-1B-Commercial은 커스텀 사용 제한 라이선스(신청서, 군사·ITAR 제외): 'OK(민수)'를 '조건부(V7)'로. Zone T 호스팅 추론은 V7 통과 후, Zone S 가중치 번들은 재배포 조항 서면 확인 전 제외. GR00T N1.7은 학습·내부 사용 OK, 파인튜닝 가중치의 고객 납품은 V7(M3) 통과 후, 부정적이면 SmolVLA·ACT로 증류 납품 | DR §2 #12·#15·§3.3·§6.2·§15, 03, 05, 07, 부록 A |
| 33 | [T-6] Drake 휠 분류 | PyPI 휠은 'BSD and Other/Proprietary'(번들 서드파티 솔버 별도 약관). Zone F 내부 검증은 OK, Zone S 번들은 독점 솔버를 뺀 소스 빌드만(V2 법률 의견 후) | DR §2 #5·§3.3·§6.2·§15, 03 |
| 34 | [T-8] Isaac Sim 번들 버전 표기 | 'Isaac Lab 3.x + PhysX 5.x(Isaac Sim 6.1 번들 버전 [U], 공개 SDK 최신 5.11)', 'Kit 110.x [U]'로 표기. Run Manifest 예시도 같은 표기 | DR §0·§2 #2·#8·§7.1·§15, 03, 04, 05 |
| 35 | [T-9] MuJoCo flex | 3.15 Stable Neo-Hookean과 3.14 IPC 접촉은 둘 다 실험적 기능 | DR §2 #4, 03, 05 |
| 36 | [T-10] R0 브라우저 렌더 | 'three.js r186(WebGPU/WebGL2) + Spark 2.x(WebGL2), PlayCanvas 2.23(WebGPU), Babylon.js 9.29(OpenUSD WASM)'. WebGPU 미지원 브라우저는 WebGL2로 동작 | DR §2 #9·§3.1·§6.1·§10.3, 04, 06 |
| 37 | [T-11] Newton–Warp 버전 | 'Newton 1.6.1 단독 사용은 Warp 1.18 요구'를 'Newton 1.6.1의 최소 Warp 버전은 pyproject로 확인 [U]. 최신 Warp 1.18 휠은 Turing(sm_75) 이상·R580 이상(CUDA 13) 필요'로 정정 | DR §2·§15, 03, 04 |
| 38 | [T-12] MinIO 태그 | 'MinIO(AGPL [A])'를 'MinIO(AGPL-3.0 [U], SPDX 확인 M2)'로. 사실 주장이므로 [U] | DR §2 #19·§15 #21, 03, 04, 08, 11 |
| 39 | [T-13] ROS 2 수명 | Humble 2027-05 EOL(이후 보안 패치 없음), Jazzy 2029-05, Lyrical 2031-05. 신규 배포 기본은 Jazzy·Lyrical, Humble 브리지는 M7 이후 best-effort | DR §2 #21·§6.3·§15, 04, 08 |
| 40 | NEVER #22 후보 | MapAnything 기본(비 apache) 가중치를 NEVER #22 후보로 추가. 허용 대상은 MapAnything-apache 가중치로 한정 | DR §2 #12·§3.3, 03 §10.3, 05, 부록 A §0.3 |
| 41 | 엔진 표 사본 관리 | DR §2는 역할·라이선스·구역 판정의 정본, 03 §7·§12.3은 버전 문자열·구역 열·트리거의 운영 정본. README §2는 요약, 부록 A는 판정 등급만. 버전 변경은 03 먼저, DR은 분기 Errata로 동기화 | DR §2, 03, README, 부록 A |
| 42 | 실행 계획 정본 | 30/60/90일 실행, NVIDIA 체크리스트 우선순위, 베이크오프 주차 계획의 정본은 12 §3–§5. DR §14는 결정 기준과 큰 줄기만 유지 | DR §14, 03 §13, 12 |
| 43 | 플랫폼 정의·표기 | 한 줄 정의를 평이한 문장으로 바꾸고 '연성' 은유는 01 §2 브랜드 서사에만 둔다. 표준 용어는 '피지컬 AI'(첫 출현에 Physical AI 병기)와 'sim-to-real', sim2sim·sim2real은 게이트 이름에만. 적용 범위는 '본 문서 12종, README, 부록 A·B'. 내부 부록 제목은 '전 문서 공통 고정값(Canonical Numbers)'. Newton 표기는 'Newton 1.6.x(Isaac Lab 3.x GA 핀으로 통일, 2026-10 최신 1.6.1)'. 용어집은 README §9 | DR 머리말·§0·§2·부록, 01, 02, README |
| 44 | 계층 번호 | 시스템 계층은 L0–L8(§6.1), 현실감 4계층(§4.2)은 'L1–L4 현실감 계층'으로 따로 부른다. §6.1 계층도는 한국어 이름·설명으로 표기 | DR §4.2·§6.1, 04, 05 |
| 45 | 시장 규모 표현 | 목표에서 역산한 'SOM'은 쓰지 않고 '목표 매출과 요구 점유율'로 표기(2029년 목표는 한국 SAM 중간값의 약 14%, 글로벌 SAM의 0.6–2.1%) | DR §10.7, 02, 10 |
| 46 | sim/real r 표본 크기 | 정책 5개로 잰 r = 0.8의 95% CI는 약 [−0.28, 0.99]로 넓어 판정 근거가 되지 않는다(07 §8.3). KPI 보고 최소는 정책 ≥5개(Fisher 95% CI 병기)로 두되, 인증용 r과 G3 ⑤(r ≥0.8)는 정책 패밀리 ≥8개(권장 12) [A]로 잰다. PoC 인수의 '정책 5개 이상 r 보고'는 보고 요건으로 유지 | DR §4.2·§7.2·§13.2, 05 §13, 07 §8.3, 09 §3.5, 11 §3 |
| 47 | 보수안 발동 기준의 Series A 금액 | 'Series A < ₩60억'은 브리지 ₩20억을 포함한 Series A 총액 기준이다(브리지 ₩20억이면 본 클로징 텀시트 ₩40억 미만일 때 발동). Enterprise VPC의 RTX는 고객 자기 계정·VPC의 BYOL에 한정하고, AICHEMIST 운영 테넌시에서는 NVIDIA 서면 확인(§14.2 #5) 전까지 제공하지 않는다 | DR §9.3·§10.3, 09, 10, 12 |

---

## 부록. 전 문서 공통 고정값 (Canonical Numbers)

이 표는 별도 문서인 [부록 A 기술 카탈로그](appendix-a-technology-catalog.md)와 다르다. 값이 바뀌면 §16 Errata에 먼저 기록한다.

| 항목 | 고정값 |
|---|---|
| 플랫폼명 | CEN Athanor(하위: Forge, Data, Skill, Crucible, Studio, Live / 에디션: Cloud, Sovereign, Air-gap) |
| 기간 | M1 = 2026.11. P0 M1–M4, P1 M5–M12, P2 M13–M24, P3 M25–M36 |
| 일정 기준일 | D0 = 2026-10-16(금, CEO 승인), D90 = 2027-01-16. 베이크오프 W1 2026-11-02 ~ W8 2026-12-27, 결정 메모 2027-01-08 |
| 게이트 | G0 M4, G1 M11(인원 26명 상한 해제), G2 M18, G3 M24. 심의일 G0 2027-02-26, G1 2027-09-24, G2 2028-04-28, G3 2028-10-27 |
| 인원(단계 말) | 16 / 26 / 36 / 48 |
| Head-month(24개월) | 564 (44 / 160 / 360) |
| 인건비 단가 | ₩1,400만/HM(혼합, 완전부담) |
| 24개월 예산 | 기준 ₩122.0억(P0 11.2 / P1 37.0 / P2 73.8). 보수 ₩98.8억, 공격 ₩158.7억 |
| 예산 구성(기준) | 인건비 79.0, 컴퓨트 14.0, 라이선스 4.2, 법무·IP·인증 3.5, Fidelity Lab 6.8, GTM·관리 5.5, 예비비 9.0 |
| NVAIE 예비비 | ₩2.9억(46 GPU-year × $4,500 [U]) |
| RT 풀 | 자체 16 GPU(M5 8장 + M13 8장) + 클라우드 평균 3/5/8, P2 최대 약 32 |
| 매출 목표 | 2027 ₩15억 / 2028 ₩45억 / 2029 ₩110억. 연말 ARR 3 / 20 / 70 |
| 정부재원 비중 | 40% / 20% / 11% |
| 해외 비중 | 0% / 9% / 27% |
| 반복매출·총마진 | 10%·45% / 30%·52% / 50%·60% |
| 라운드 | Series A ₩80억(M9–M12는 본 클로징 구간: M5 전환 조건부 브리지 ₩20억 + M10 ₩30억 + M12 ₩30억, §9.4), Series B ₩250억(M25–M28) |
| 첫 매출 | M4 데이터셋 계약(≥₩0.5억). 바우처 납품 M5–M8. PoC 판매 M5부터 |
| 토큰 | 1 토큰 = ₩100. RT 60 / 서울 대화형 95 / TRAIN 80 / LIGHT 20 토큰/시간 |
| PoC | 12주, ₩1.5–2.5억, 선금 30%, 책임 상한 = 계약 금액 |
| 인증 등급 | Bronze(VLM 추정) / Silver(영상 식별) / Gold(랩 실측). KPI는 Silver/Gold만 집계 |
| 결정론 등급 | Run Manifest `D0_bitwise` / `D1_statistical` / `D2_generative` / `none`. 인증서는 D0 경로에서만 |
| sim2sim 게이트 | Zone F 3개(Newton·PhysX·MuJoCo CPU), Zone T/S 2개(Newton·MuJoCo CPU). Tier 1: 1,000 에피소드·≤10%p. Tier 2: 초기조건 200개·≤5%p·관절 RMSE ≤0.05 rad |
| 비치헤드 | 물체가 많은 조작, 18개월. Wave 2는 M12, Wave 3는 M25부터 트리거 판정(ARR ₩30억 또는 자금 확보 앵커. 기본 경로는 확정 ₩5억 이상 앵커), 국방 Air-gap은 M27부터 |

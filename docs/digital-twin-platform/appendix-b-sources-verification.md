# 부록 B. 출처 및 검증 현황

| 항목 | 내용 |
|---|---|
| 문서 번호 | Appendix B |
| 기준일 | 2026-10-06 |
| 버전 | v1.0 |
| 상위 문서 | [README](README.md) |
| 관련 문서 | [00 결정 기록](00-decision-record.md) · [03 엔진 선정](03-engine-selection-build-vs-buy.md) · [11 리스크·KPI·컴플라이언스](11-risk-kpi-compliance.md) · [부록 A 기술 카탈로그](appendix-a-technology-catalog.md) |
| 표기 | [A] 계획 가정 · [U] 1차 출처 미확인(대외 사용 전 재검증 필수) |

## 핵심 요약

- **리서치 범위:** 8개 영역을 병렬로 조사했다. 영역별로 엔진·도구·제품·프로그램을 평가하고 출처 URL을 붙였다(아래 §4).
- **적대적 팩트체크:** 의사결정에 결정적인 주장 48건을 재검증했다. 결과는 확인 29건, 정정 10건, 확인 불가 9건이며, 반박된 주장은 0건이다.
- **검증 강도 차이:** GitHub·PyPI·SkyPilot 가격 카탈로그로 확인한 사실(버전, 라이선스 파일, 릴리스 일자, 클라우드 단가)은 신뢰도가 높다. NVIDIA·Epic·국내 정부·언론 사이트는 접근이 제한되어, 시장 규모·투자 유치 금액·국내 정책 예산·벤더 리스트 가격은 **[U]로 남겼다**.
- **정정 사항은 모두 본 계획서에 반영했다.** 예: Newton 1.0.0 = 2026-03-10, ovphysx pip 휠은 독점 라이선스, PhysX SDK 코어는 Apache-2.0, Cosmos 3 = 64B/16B/4B, Warp 1.18은 R580 이상 드라이버 필요.
- **대외 사용 규칙:** [U] 수치는 IR·정부과제·이사회 자료에 그대로 쓰지 않는다. [11 문서 §7 검증 필요 항목](11-risk-kpi-compliance.md)의 담당자와 기한에 따라 재검증한 뒤에 쓴다.

## 1. 리서치 방법

| 단계 | 방법 | 산출물 |
|---|---|---|
| 1. 영역별 심층 조사 | 8개 영역 병렬 조사. 1차 출처(공식 문서, GitHub 저장소·LICENSE 파일, PyPI, 릴리스 노트, 논문, 보도자료) 우선 | 영역별 후보 평가표, 핵심 사실, 정량 데이터, 권고, 리스크 |
| 2. 적대적 팩트체크 | 결정에 영향이 큰 주장을 골라 반박을 시도. 1차 출처가 없으면 '확인 불가'로 판정 | 확인·정정·확인 불가 판정, 치명적 경고, 커버리지 공백 |
| 3. 전략 심사 | 독립 전략안 3종(NVIDIA 가속형, 소버린 오픈코어형, 결과물 팩토리형)을 CTO, 투자자, 고객·정부 평가단 3개 관점에서 12개 기준으로 채점 | 결정 기록([00](00-decision-record.md)) |
| 4. 문서화 | 결정 기록을 단일 기준(SSOT)으로 삼아 주제별 계획서 작성 | 01–12, 부록 A·B |

## 2. 팩트체크에서 나온 치명적 경고(요약)

1. **NVIDIA SaaS 약관은 미확인이다.** Isaac Sim이나 Kit을 제3자에게 서비스로 제공할 때 어떤 라이선스가 필요한지(NVAIE 여부, 산출물 면제 여부)를 1차 출처로 확인하지 못했다. NVIDIA Korea에 서면으로 확인받기 전까지 Zone F(내부 팩토리)에서만 사용한다.
2. **Kit-less가 라이선스 프리라는 뜻은 아니다.** ovphysx pip 휠, ovrtx, ovstage, isaacsim/isaaclab PyPI 휠은 모두 독점 약관이다. 완전 허용형 스택은 Newton, MuJoCo/MJWarp, Warp, 소스 빌드 Isaac Lab(BSD-3), 소스 빌드 PhysX SDK(Apache-2.0)뿐이다.
3. **Hunyuan3D 2.1 라이선스는 한국을 지역에서 제외한다**(출력물 사용 포함). Inria 3DGS 계열, Instant-NGP, nvdiffrast, MimicGen 코드, ManiSkill 자산, AgiBot GO-1, RLDX-1, Waymax도 비상업 조건이다.
4. **cuRobo 라이선스가 충돌한다.** 업스트림은 Apache-2.0이지만, Isaac Lab에 번들된 cuRobo는 별도 약관을 따른다. Apache 태그로 고정해 쓰고 NVIDIA 확인을 받는다.
5. **온프렘·에어갭 납품은 '배포'에 해당한다.** GPL(BlenderProc, Stonefish), Isaac Sim/Kit 재배포 조항, Epic EULA가 발동한다. AGPL(Ultralytics)은 SaaS에서도 발동한다. SAM License는 ITAR·군사 용도를 제한한다.
6. **GPU 풀은 둘로 나눠야 한다.** RTX 렌더링에는 RT 코어 GPU(A40 최소, L40S 권장, RTX PRO 6000 Blackwell 최적)가 필요하다. H100/H200/B200에는 RT 코어가 없다. 정부 배정 GPU는 학습 전용으로만 쓸 수 있다.
7. **드라이버 하한이 올라갔다.** Warp 1.18(Newton 핵심 의존성)은 Turing 이상 GPU와 R580 이상 드라이버(CUDA 13)를 요구한다. 국내 CSP 이미지를 미리 점검해야 한다.
8. **벤치마크를 잘못 쓸 위험이 있다.** MJWarp 나이틀리 수치는 물리 연산만 잰 값이고, Isaac Lab FPS는 학습을 포함한 값이다. Genesis 43M FPS는 출시 마케팅 수치다. 252×/475×는 벤더 주장이다. 의사결정에는 사내 베이크오프 수치만 쓴다.
9. **성숙도 리스크가 있다.** Isaac Lab 3.0은 EA(GA 2026년 10월 말 목표)이고, Isaac Sim 7.0은 alpha, MJWarp는 PyPI상 Alpha, Omniverse 라이브러리 전부가 alpha·pre-release, Newton Kamino는 experimental이다. Isaac Sim 스트리밍에는 인증·암호화가 없다.

## 3. 팩트체크 상세 (원문 유지)

> 판정은 2026-10-06 기준이다. 주장과 정정 내용은 검증 원문(영문)을 그대로 실었다.

| # | 판정 | 영역 | 검증 대상 주장 | 정정·비고 | 출처 |
|---|---|---|---|---|---|
| 1 | ⚠️ 확인 불가 | license/Isaac Sim SaaS | Isaac Sim source is Apache-2.0, but delivering Isaac Sim (with Kit) as a service to third parties, or redistributing it, requires NVIDIA AI Enterprise. Selling only outputs (datasets, videos) does not. | Confirmed: Isaac Sim runtime depends on proprietary NVIDIA components. Unverified: that NVAIE is the specific instrument required for SaaS and that output-only sales are exempt. Get written confirmation from NVIDIA before choosing an architecture. | https://github.com/isaac-sim/IsaacSim/blob/develop/LICENSE ; https://pypi.org/project/isaacsim/#history |
| 2 | ✅ 확인 | license/Isaac Lab pip wheel | Isaac Lab is BSD-3 (isaaclab_mimic Apache-2.0); the PyPI isaacsim/isaaclab wheels are labeled 'NVIDIA Proprietary Software'. | Build from the BSD-3 GitHub source, not the proprietary-labeled pip wheel, if you need clean licensing. | https://pypi.org/pypi/isaaclab/json ; https://github.com/isaac-sim/IsaacLab |
| 3 | ✏️ 정정 | license/ovphysx | (platform_arch) ovphysx is BSD-3-Clause. (robot_physics) ovphysx is 'LicenseRef-NVIDIA-Omniverse', not BSD. | ovphysx source is Apache-2.0. The pip binaries (and the ovstage dependency) are proprietary NVIDIA Omniverse-licensed. 'Kit-less' does not mean 'license-free'. | https://github.com/NVIDIA-Omniverse/PhysX/tree/main/ovphysx ; https://pypi.org/project/ovphysx/ ; https://pypi.org/pypi/ovstage/json |
| 4 | ✅ 확인 | license/ovrtx | ovrtx is proprietary (NVIDIA SLA + Product-Specific Terms for NVIDIA AI Products), alpha. |  | https://pypi.org/project/ovrtx/ ; https://github.com/NVIDIA-Omniverse/ovrtx |
| 5 | ✏️ 정정 | license/PhysX SDK | The PhysX SDK, including full GPU source, has been BSD-3 since PhysX 5.6 (April 2025); the latest SDK is 5.11.0. | The PhysX SDK 5.11 core is Apache-2.0 (permissive, with patent grant and NOTICE duties) and GPU source is in the repo. The repo root is still BSD-3. | https://raw.githubusercontent.com/NVIDIA-Omniverse/PhysX/main/physx/README.md ; https://raw.githubusercontent.com/NVIDIA-Omniverse/PhysX/main/LICENSE.md ; https://github.com/NVIDIA-Omniverse/PhysX/tree/main/physx/source |
| 6 | ✅ 확인 | engine status/Newton | Newton 1.0.0 released 2026-03-10; latest v1.6.1 on 2026-10-05; Apache-2.0; Linux Foundation; started by Disney Research, Google DeepMind and NVIDIA. (market_competition: v1.0.0 Apr 13, 2026. training: PyPI newton-physics 1.0.0 on 2026-02-27.) | Newton 1.0.0 is from 2026-03-10; Apr 13, 2026 was 1.1.0. Install 'newton', not the inactive 'newton-physics'. | https://pypi.org/project/newton/ ; https://github.com/newton-physics/newton ; https://pypi.org/pypi/newton-physics/json |
| 7 | ✏️ 정정 | hardware/Newton+Warp driver floor | Newton requires an NVIDIA GPU, Maxwell or newer, driver 545+. | With current Warp wheels, plan for Turing or newer GPUs and R580+ drivers (CUDA 13). Check that cloud and Korean-CSP GPU images ship R580+ drivers. | https://github.com/newton-physics/newton ; https://pypi.org/project/warp-lang/ |
| 8 | ✅ 확인 | engine capability/Newton solvers | Newton solvers are Featherstone, MuJoCo, SemiImplicit, XPBD, Kamino, VBD, Style3D and ImplicitMPM. Only Featherstone and SemiImplicit are differentiable (basic). Only Featherstone and MuJoCo support generalized-coordinate articulations. |  | https://raw.githubusercontent.com/newton-physics/newton/main/docs/solvers/index.rst |
| 9 | ✅ 확인 | engine capability/Newton determinism | Newton v1.4.0 added deterministic execution paths for bit-exact repeated rollouts, plus coupled solvers. |  | https://github.com/newton-physics/newton/releases/tag/v1.4.0 ; https://github.com/newton-physics/newton/releases.atom |
| 10 | ✅ 확인 | engine capability/MJWarp limits | MJWarp is not differentiable, is non-deterministic on GPU, uses float32, and struggles with single connected mechanisms above about 60 DoF; MJX exposes it as impl='warp'. |  | https://raw.githubusercontent.com/google-deepmind/mujoco/main/doc/mjwarp/index.rst ; https://pypi.org/project/mujoco-warp/ |
| 11 | ✅ 확인 | engine status/MuJoCo | MuJoCo Warp was officially released with MuJoCo 3.5.0 (2026-02-12), which added a system-identification toolbox. 3.14 added IPC flex contact; 3.15 (2026-10-05) added Stable Neo-Hookean flex. |  | https://raw.githubusercontent.com/google-deepmind/mujoco/main/doc/changelog.rst ; https://github.com/google-deepmind/mujoco/releases.atom ; https://pypi.org/pypi/mujoco/json |
| 12 | ✅ 확인 | benchmark/MJWarp nightly | MJWarp on RTX PRO 6000 Blackwell: humanoid 7.95M, Franka 36.97M, G1 flat/heightfield 3.79M/2.49M, ALOHA pot 3.37M, ALOHA clutter 0.46M steps/s. | The values are roughly right, but they are sim-only throughput. Do not compare them to Isaac Lab 'step+inference+train' FPS or use them as RL wall-clock estimates. | https://github.com/google-deepmind/mujoco_warp/pull/1748 |
| 13 | ⚠️ 확인 불가 | benchmark/MJWarp vs MJX speedups | MuJoCo Warp is up to 252x (locomotion) and 475x (manipulation) faster than MJX on RTX PRO 6000 Blackwell; the Newton beta figures were 152x and 313x on an RTX 4090. | Treat these as vendor 'up to' claims. Run your own benchmarks on target scenes. | https://developer.nvidia.com/blog/newton-adds-contact-rich-manipulation-and-locomotion-capabilities-for-industrial-robotics (blocked) |
| 14 | ✅ 확인 | benchmark/Isaac Lab | On an RTX 4090: G1 rough 94k/88k/82k FPS (4,096 envs, 6.1 GB); Shadow repose 200k/170k (8,192 envs); Cartpole 1.1M; Cartpole RGB 50k (16.7 GB). On 4 nodes × 4 L40: G1 960k, Shadow 1.8M train FPS. |  | https://raw.githubusercontent.com/isaac-sim/IsaacLab/main/docs/source/overview/reinforcement-learning/performance_benchmarks.rst |
| 15 | ✅ 확인 | engine status/Isaac Lab 3.0 | Isaac Lab v3.0.0-EA was released 2026-09-16 for Isaac Sim 6.1, PyTorch 2.11, Warp 1.16 and Newton 1.5.2; GA targeted end of Oct 2026. (robot_physics, citing beta2 docs: Newton backend is 'beta' with a focused set of environments.) | EA is not GA, and API stability is only promised from GA. Plan to pin release/3.0.0 after late-October 2026. | https://github.com/isaac-sim/IsaacLab/releases.atom ; https://github.com/isaac-sim/IsaacLab/releases/tag/v3.0.0-EA |
| 16 | ✏️ 정정 | engine status/Isaac Sim releases | Isaac Sim 6.0 GA on 2026-06-08; 6.1.0 on 2026-09-10; 7.0.0a1 on 2026-09-18. | The 6.0.0 GA tag is 2026-06-04 (the forum announcement may say Jun 8). 7.0 is alpha only. | https://github.com/isaac-sim/IsaacSim/releases ; https://pypi.org/project/isaacsim/#history |
| 17 | ✅ 확인 | hardware/Isaac Sim GPUs and RT cores | Isaac Sim datacenter GPUs: A40 minimum, L40S recommended, RTX PRO 6000 Blackwell Server best. H100/A100/B200 lack RT cores and cannot be used for RTX rendering. | Budget for two GPU pools: RT-core GPUs (L40S / RTX PRO 6000) for rendering and SDG, and H100/H200/B200 for training. Government-allocated B200/H200 cannot do RTX sensor rendering. | https://github.com/isaac-sim/IsaacSim ; https://github.com/NVIDIA-Omniverse/kit-app-template ; https://github.com/NVIDIA-Omniverse/ovrtx |
| 18 | ⚠️ 확인 불가 | hardware/MIG on RTX PRO 6000 | RTX PRO 6000 Blackwell supports MIG (up to 4 instances), L40S has no MIG, so an RTX session costs about $0.84/h at a 4-way split. | Do not build SaaS unit economics on $0.84/h until MIG plus RTX streaming is tested on g7e/G4 instances. | https://raw.githubusercontent.com/isaac-sim/IsaacLab/main/docs/source/overview/reinforcement-learning/performance_benchmarks.rst |
| 19 | ✅ 확인 | GPU prices/AWS | AWS us-east-1: g6e.xlarge (L40S) $1.861/h, g7e.2xlarge (RTX PRO 6000) $3.363/h, p5.48xlarge (8×H100) $55.04/h, p5en.48xlarge (8×H200) $63.30/h, p6-b200 $113.93/h. Seoul is 23-38% higher. | Confirmed against the SkyPilot catalog, which is derived from the AWS pricing API. aws.amazon.com itself was not reachable. | https://raw.githubusercontent.com/skypilot-org/skypilot-catalog/master/catalogs/v8/aws/vms.csv |
| 20 | ✅ 확인 | GPU prices/neoclouds | RunPod on-demand: L40S $1.09, RTX PRO 6000 $2.09, H100 PCIe $2.89 / SXM $3.49, B200 $6.79, RTX 4090 $0.74, L4 $0.49. GCP G4 (RTX PRO 6000) $4.50/h. |  | https://raw.githubusercontent.com/skypilot-org/skypilot-catalog/master/catalogs/v8/runpod/vms.csv ; https://raw.githubusercontent.com/skypilot-org/skypilot-catalog/master/catalogs/v8/gcp/vms.csv |
| 21 | ⚠️ 확인 불가 | license price/NVAIE and Omniverse Enterprise | NVIDIA AI Enterprise / Omniverse Enterprise is about $4,500 per GPU per year; $1,125 for Inception startups (75% off); about EUR 5,800 via an EU reseller. | Treat as a placeholder. Get a written NVIDIA Korea / NPN quote covering multi-tenant SaaS and on-prem redistribution, per GPU or per node. | https://pi3g.com/nvidia-ai-enterprise-subscription-cost-in-2026/ (blocked) |
| 22 | ⚠️ 확인 불가 | license price/Unreal Engine | Unreal Engine charges non-game companies with more than $1M annual revenue $1,850 per seat per year (since UE 5.4, April 2024). |  | https://www.unrealengine.com/en-US/license (blocked) |
| 23 | ✅ 확인 | engine status/Genesis | Genesis World 1.4.3 (2026-09-30) is Apache-2.0. The original '43M FPS Franka on RTX 4090' claim was criticized as misleading. | The 43M FPS figure is a launch marketing number; the size of the critique's gap is unverified. | https://pypi.org/project/genesis-world/ ; https://raw.githubusercontent.com/Genesis-Embodied-AI/Genesis/v0.2.1/README.md ; https://raw.githubusercontent.com/Genesis-Embodied-AI/Genesis/main/README.md |
| 24 | ✏️ 정정 | license/Genesis Nyx renderer | Nyx ships as a separate gs-nyx package; verify its license before embedding. | Nyx is effectively a closed-source binary with an ambiguous license. Do not treat Genesis's photoreal rendering path as open source. | https://pypi.org/project/gs-nyx/ ; https://github.com/Genesis-Embodied-AI/genesis-nyx |
| 25 | ✏️ 정정 | license/cuRobo | (training) SkillGen depends on cuRobo, which has proprietary terms. (build_vs_buy) cuRobo's LICENSE is now Apache-2.0. | Pin a cuRobo release that is Apache-2.0 at that tag, and ask NVIDIA which terms govern the version Isaac Lab installs. | https://github.com/NVlabs/curobo/blob/main/LICENSE ; https://raw.githubusercontent.com/isaac-sim/IsaacLab/main/docs/licenses/dependencies/cuRobo-license.txt |
| 26 | ✅ 확인 | license/MimicGen | MimicGen and DexMimicGen code is under the NVIDIA Source Code License; datasets are CC-BY-4.0. | MimicGen code is non-commercial. A commercial data-multiplication feature must use isaaclab_mimic (Apache-2.0) or an in-house reimplementation. | https://raw.githubusercontent.com/NVlabs/mimicgen/main/LICENSE ; https://github.com/NVlabs/mimicgen |
| 27 | ✅ 확인 | license/Hunyuan3D 2.1 | The Tencent Hunyuan 3D 2.1 Community License excludes the EU, UK and South Korea, and forbids using the Works or their outputs outside the Territory. | AICHEMIST, as a Korean company, cannot use Hunyuan3D 2.1 open weights or their outputs. | https://raw.githubusercontent.com/Tencent-Hunyuan/Hunyuan3D-2.1/main/LICENSE |
| 28 | ✅ 확인 | license/3D generation chain | TRELLIS.2-4B is MIT but depends on nvdiffrast (Nvidia Source Code License, 1-Way Commercial, non-commercial except NVIDIA); TRELLIS.2 generates 512³/1024³/1536³ in about 3/17/60 s on H100 with ≥24 GB VRAM. |  | https://github.com/microsoft/TRELLIS.2 ; https://raw.githubusercontent.com/NVlabs/nvdiffrast/main/LICENSE.txt |
| 29 | ✅ 확인 | license/Gaussian splatting stack | Inria 3DGS (and derivatives such as 2DGS and MILo) is research/evaluation only; Instant-NGP is non-commercial; 3DGRUT and gsplat are Apache-2.0; PhysX-Anything uses the S-Lab License. |  | https://raw.githubusercontent.com/graphdeco-inria/gaussian-splatting/main/LICENSE.md ; https://raw.githubusercontent.com/nv-tlabs/3dgrut/main/LICENSE ; https://raw.githubusercontent.com/nerfstudio-project/gsplat/main/LICENSE ; https://raw.githubusercontent.com/ziangcao0312/PhysX-Anything/main/README.md |
| 30 | ✅ 확인 | license/Cosmos 3 | Cosmos 3 (Super 64B, Nano 16B, Edge 4B) is under OpenMDW-1.1 for code and weights; press reports said 32B/8B; Cosmos-Predict2.5 and Transfer2.5 are in limited maintenance. | Use 64B/16B/4B; the 32B/8B press figures are wrong. Build on Cosmos 3, not 2.5. Have counsel review OpenMDW-1.1. | https://github.com/NVIDIA/Cosmos ; https://raw.githubusercontent.com/nvidia-cosmos/cosmos-predict2.5/main/README.md ; https://raw.githubusercontent.com/nvidia-cosmos/cosmos-transfer2.5/main/README.md |
| 31 | ✅ 확인 | license/Alpamayo and AlpaSim | AlpaSim is Apache-2.0. Alpamayo weights are OpenMDW-1.1 with commercial use permitted. Alpamayo 1.5 came in Mar 2026 and Alpamayo 2 Super (32B) on 1 Jun 2026. | Confirmed for AlpaSim and Alpamayo 1/1.5. Alpamayo 2 Super (32B) and the '~900 scenes' count remain unverified. | https://github.com/NVlabs/alpasim ; https://github.com/NVlabs/alpamayo |
| 32 | ✅ 확인 | license/GR00T N1.7 | GR00T N1.7 is GA: 3B parameters, Cosmos-Reason2-2B backbone, 20K h EgoScale human video, fine-tune on ≥40 GB GPUs, inference on ≥16 GB; code Apache-2.0, weights NVIDIA Open Model License. |  | https://github.com/NVIDIA/Isaac-GR00T |
| 33 | ✅ 확인 | license/datasets and model weights for marketplace | ManiSkill assets are CC BY-NC 4.0; AgiBot World and GO-1 are CC BY-NC-SA; Waymax is non-commercial; RLDX-1 weights are non-commercial; openpi weight license is unstated; VGGT-1B is non-commercial (only the -Commercial checkpoint allows commercial use); DA3 Large/Giant are CC BY-NC. |  | https://github.com/haosulab/ManiSkill ; https://raw.githubusercontent.com/OpenDriveLab/AgiBot-World/main/README.md ; https://raw.githubusercontent.com/waymo-research/waymax/main/README.md ; https://raw.githubusercontent.com/RLWRLD/RLDX-1/main/README.md ; https://raw.githubusercontent.com/facebookresearch/vggt/main/README.md ; https://raw.githubusercontent.com/ByteDance-Seed/Depth-Anything-3/main/README.md |
| 34 | ✅ 확인 | license/SAM 3D Objects | SAM 3D Objects is under the SAM License: royalty-free and worldwide, with commercial use allowed subject to restrictions (e.g., military). | Commercial use is OK, but ITAR and trade-control restrictions block Korean defense or ADD use cases for this component. | https://raw.githubusercontent.com/facebookresearch/sam-3d-objects/main/LICENSE |
| 35 | ✅ 확인 | license/copyleft and source-available infrastructure | lakeFS v1.87.0 moved from Apache-2.0 to BSL 1.1. Ultralytics is AGPL-3.0. RF-DETR N–L are Apache-2.0 (XL/2XL under PML 1.0). BlenderProc and Stonefish are GPL-3.0. | GPL is fine for pure SaaS but is triggered by on-prem delivery, which counts as distribution. AGPL is triggered by network use, so avoid Ultralytics in the hosted product. | https://github.com/treeverse/lakeFS/releases.atom ; https://raw.githubusercontent.com/ultralytics/ultralytics/main/README.md ; https://github.com/roboflow/rf-detr ; https://raw.githubusercontent.com/DLR-RM/BlenderProc/main/LICENSE ; https://github.com/patrykcieslak/stonefish |
| 36 | ✅ 확인 | engine status/CARLA | CARLA's latest tag is 0.10.0 (UE 5.5, Dec 2024), with no 0.10.x follow-up. The UE5 build needs an RTX 3070-class GPU with 16 GB+ VRAM and 32 GB+ RAM. Code is MIT, assets CC-BY. |  | https://github.com/carla-simulator/carla/releases.atom ; https://raw.githubusercontent.com/carla-simulator/carla/ue5-dev/README.md |
| 37 | ✅ 확인 | engine status/legacy engines | RaiSim v1 was archived 2026-04-25 and needs a license key. PyBullet's last release is 3.2.7 (2025-01-30). Brax physics is deprecated, with only brax/training maintained since 0.13.0. |  | https://github.com/raisimTech/raisimLib ; https://pypi.org/project/pybullet/#history ; https://github.com/google/brax |
| 38 | ✏️ 정정 | engine status/Chrono and Drake | Chrono 10.0.0 (spring 2026) is BSD-3 with refactored FSI, peridynamics and checkpointing; (build_vs_buy) Chrono 10.0.0 has an AMD ROCm GPU path. Drake v1.57.0 released 2026-09-10. | Chrono's AMD/ROCm and Vulkan/Metal sensor backends are dev-branch only and not in a release. | https://raw.githubusercontent.com/projectchrono/chrono/main/CHANGELOG.md ; https://pypi.org/project/drake/ |
| 39 | ✏️ 정정 | engine status/mjlab | (robot_physics) mjlab is in the 1.5.x series and pinned to MuJoCo Warp 3.11. (training) mjlab 1.6.0 was released 2026-08-09. | Latest mjlab is 1.6.0 (2026-08-09). It lags upstream MJWarp (pinned to 3.11). | https://pypi.org/pypi/mjlab/json ; https://raw.githubusercontent.com/mujocolab/mjlab/main/README.md |
| 40 | ✅ 확인 | interop/ROS 2 and Isaac Sim | ROS 2 Lyrical Luth was released 2026-05-22 as an LTS with EOL May 2031. The Isaac Sim ROS workspaces repo provides only Humble and Jazzy. ros_gz pairs Lyrical with Jetty. |  | https://raw.githubusercontent.com/ros2/ros2_documentation/rolling/source/Releases.rst ; https://github.com/NVIDIA-Omniverse/IsaacSim-ros_workspaces ; https://github.com/gazebosim/ros_gz |
| 41 | ✏️ 정정 | standards/OpenUSD and glTF | OpenUSD 26.03 (2026-02-24) added wasm and UsdVolParticleField (3DGS). UsdPhysics gained nested rigid bodies and kinematic articulations. 26.05 made Hydra 2 the default. (realism) KHR_gaussian_splatting is a Release Candidate. (platform_arch) KHR_gaussian_splatting is ratified. | UsdPhysics nesting and the Hydra 2 default arrived in 25.11. KHR_gaussian_splatting is now ratified. No normative physics standard exists yet. | https://raw.githubusercontent.com/PixarAnimationStudios/OpenUSD/release/CHANGELOG.md ; https://raw.githubusercontent.com/KhronosGroup/glTF/main/extensions/README.md ; https://github.com/aousd/specifications-public |
| 42 | ✏️ 정정 | platform/Omniverse libraries timing and streaming security | Omniverse libraries (ovrtx, ovphysx, ovstage) were announced at SIGGRAPH 2026 (robot_physics) or at GTC 2026 (platform_arch), in early access. Isaac Sim streaming has no auth or encryption. | ovrtx, ovphysx, ovstage and ovstorage are all alpha or pre-release as of Oct 2026, so none is production-stable. A multi-tenant streaming SaaS must add its own authentication and TLS layer. | https://pypi.org/pypi/ovrtx/json ; https://pypi.org/pypi/ovphysx/json ; https://pypi.org/pypi/ovstage/json ; https://github.com/isaac-sim/IsaacSim/blob/develop/tools/docker/README.md |
| 43 | ✅ 확인 | infra/K8s GPU scheduling | In the NVIDIA DRA driver, ComputeDomains are supported but GPU allocation is not yet officially supported and is disabled by default; it needs K8s 1.32+. KAI Scheduler is Apache-2.0. OSMO is Apache-2.0. |  | https://raw.githubusercontent.com/NVIDIA/k8s-dra-driver-gpu/main/README.md ; https://raw.githubusercontent.com/NVIDIA/KAI-Scheduler/main/README.md ; https://raw.githubusercontent.com/NVIDIA/OSMO/main/README.md |
| 44 | ✅ 확인 | vertical/drones | Pegasus Simulator v5.1.0 (26 Oct 2025) targets Isaac Sim 5.1 and PX4 1.14.3 (ArduPilot experimental). Project AirSim is MIT. | Pegasus has not been ported to Isaac Sim 6.x. A drone vertical on Isaac Sim 6.1 needs porting work or a different path (Project AirSim, Gazebo + PX4). | https://raw.githubusercontent.com/PegasusSimulator/PegasusSimulator/main/README.md ; https://raw.githubusercontent.com/iamaisim/ProjectAirSim/main/README.md |
| 45 | ⚠️ 확인 불가 | Korea policy/GPU and budget | NVIDIA committed 260k+ Blackwell GPUs to Korea on 31 Oct 2025 (government ~50k, Samsung/SK/HMG ~50k each, Naver ~60k), with an HMG physical-AI cluster of ~$3B. MSIT selected NHN (~7,656 B200), Naver (~3,056 H200) and Kakao (~2,424 B200). The 2026 budget is KRW 727.9T with AI at ~10.1T. The AI Basic Act took effect 22 Jan 2026. | Re-verify every Korean figure (budgets, GPU counts, program caps, 2027 call dates) against MSIT/MOTIE/MSS press releases before putting it in a CEO plan or grant proposal. | https://nvidianews.nvidia.com/news/south-korea-ai-infrastructure (blocked) ; https://www.law.go.kr (blocked) |
| 46 | ⚠️ 확인 불가 | Korea policy/startup programs | Deep-tech TIPS gives up to KRW 1.5B over 3 years (operator investment ≥ KRW 0.3B). Super-Gap 1000+ gives up to KRW 0.6B. The K-Humanoid Alliance launched 10 Apr 2025. The SME government R&D share is up to 75%. |  | https://www.jointips.or.kr (blocked) |
| 47 | ⚠️ 확인 불가 | market/funding and valuations | Applied Intuition $600M at $15B (Jun 2025); Figure $39B (Sep 2025); Physical Intelligence $600M at $5.6B (Nov 2025); Skild ~$14B (Jan 2026); Genesis AI $105M seed; Waabi $750M Series C (2026); Decart $300M at ~$4B (May 2026). | Use funding figures only as context, labeled 'reported', and do not use them for TAM or competitive-moat arguments. | https://www.electrive.com/2026/02/02/autonomy-startup-waabi-secures-750-million-and-partners-with-uber/ (blocked) |
| 48 | ⚠️ 확인 불가 | research benchmarks/fidelity | GPUSimBench (arXiv 2607.13059) found GPU-batched non-determinism, with ManiSkill EMD 2.520 cm and MJX 3.970 cm best. GAUGE (arXiv 2608.05948) found no uniformly faithful engine. Instant NuRec reconstructs a clip in ~1.5 s. SDQM r=0.8719. | Do not cite GPUSimBench or GAUGE numbers in the engine decision until the papers are read. Run an in-house sim-to-real fidelity benchmark instead. | https://arxiv.org/abs/2607.13059 (blocked) ; https://raw.githubusercontent.com/isaac-sim/IsaacLab/main/docs/source/features/reproducibility.rst |

### 3.1 커버리지 공백(후속 검증 과제)

- NVIDIA Isaac Sim 라이선스 FAQ, 'Isaac Sim Additional Software and Materials License', NVAIE·Omniverse 제품별 약관(PST), OpenMDW-1.1 원문
- Epic Unreal Engine EULA의 서버 측 Pixel Streaming SaaS 조항과 2026 좌석 가격, Unity 2026 HDRP·Industry 런타임 라이선스
- 국내 CSP(NHN, KT, Naver, Kakao, Samsung SDS)의 RT 코어 GPU(L40S, RTX PRO 6000) 공급·가격, 정부 GPU 사업의 RT GPU 포함 여부, 공공 SaaS용 CSAP 요건
- 국내 멀티테넌트 SaaS의 데이터 거주·개인정보(PIPA 국외 이전, AI 기본법 생성물 표시) 의무, 수출통제(EAR, SAM License의 ITAR 조항) 심사
- 엔진 간 독립 sim-to-real 충실도 비교 근거(GPUSimBench, GAUGE 원문, SDQM/SADGE 지표)
- NuRec·3DGUT NGC 컨테이너, Sensor RTX API, AV 시뮬레이션용 Omniverse Blueprint의 라이선스·성숙도
- 비 NVIDIA GPU 이식성(Genesis Quadrants, Chrono dev 브랜치의 ROCm)과 NVIDIA 단일 의존의 공급 리스크
- 데이터셋 상품의 하드웨어 간 재현성(Newton '결정론·이식 가능 실행' 주장 실측)
- 국내 앵커 고객(HMG, Samsung, HD Hyundai, Doosan)의 실제 수요·가격 근거와 MORAI의 포지션
- Isaac Sim 6.x의 ROS 2 Lyrical 지원 여부, 드론(Pegasus)·해양(OceanSim/MarineGym)의 Isaac Sim 6.x·Isaac Lab 3.0 포팅 경로

## 4. 출처 목록 (영역별)

> 리서치 단계에서 인용한 URL이다. 같은 영역 안의 중복은 제거했고, 도메인순으로 정렬했다.

### 4.1 로봇 물리엔진·GPU 병렬 시뮬레이션 (86건)

- <https://arxiv.org/abs/2511.04831>
- <https://arxiv.org/abs/2601.22074>
- <https://arxiv.org/abs/2603.16536>
- <https://arxiv.org/abs/2607.13059>
- <https://arxiv.org/abs/2608.05948>
- <https://arxiv.org/html/2502.08844v1>
- <https://autonews.gasgoo.com/articles/news/2102741730670886912>
- <https://blockchain.news/news/nvidia-newton-physics-engine-industrial-robotics-gtc-2026>
- <https://www.cgchannel.com/2025/04/nvidia-open-sources-physxs-gpu-simulation-code>
- <https://dataconomy.com/2026/03/17/nvidia-launches-newton-1-0-physics-engine-for-industrial-robot-training/>
- <https://developer.nvidia.com/blog/announcing-general-availability-for-nvidia-isaac-sim-5-0-and-nvidia-isaac-lab-2-2>
- <https://developer.nvidia.com/blog/integrate-physical-ai-capabilities-into-existing-apps-with-nvidia-omniverse-libraries/>
- <https://developer.nvidia.com/blog/newton-adds-contact-rich-manipulation-and-locomotion-capabilities-for-industrial-robotics>
- <https://developer.nvidia.com/blog/train-a-quadruped-locomotion-policy-and-simulate-cloth-manipulation-with-nvidia-isaac-lab-and-newton>
- <https://docs.isaacsim.omniverse.nvidia.com/6.1.0/common/license-faq.html>
- <https://docs.isaacsim.omniverse.nvidia.com/6.1.0/overview/release_notes.html>
- <https://drake.mit.edu/doxygen_cxx/group__hydroelastic__user__guide.html>
- <https://en.wikipedia.org/wiki/Project_Chrono>
- <https://forums.developer.nvidia.com/t/isaac-sim-6-0-general-availability/372621>
- <https://genesis-world.readthedocs.io/en/latest/user_guide/rendering/nyx_renderer.html>
- <https://genesis-world.readthedocs.io/en/latest/user_guide/theory/couplers/sap_coupler.html>
- <https://github.com/Genesis-Embodied-AI/Genesis>
- <https://github.com/Genesis-Embodied-AI/Genesis/releases>
- <https://github.com/NVIDIA-Omniverse/PhysX>
- <https://github.com/NVIDIA-Omniverse/PhysX/releases>
- <https://github.com/NVIDIA/warp>
- <https://github.com/RobotLocomotion/drake/releases>
- <https://github.com/bulletphysics/bullet3>
- <https://github.com/dartsim/dart>
- <https://github.com/dartsim/dart/releases>
- <https://github.com/dojo-sim/Dojo.jl>
- <https://github.com/erwincoumans/tiny-differentiable-simulator>
- <https://github.com/google-deepmind/mujoco/releases>
- <https://github.com/google-deepmind/mujoco/tree/main/plugin/sensor>
- <https://github.com/google-deepmind/mujoco_warp>
- <https://github.com/google-deepmind/mujoco_warp/pull/1748>
- <https://github.com/google/brax>
- <https://github.com/haosulab/ManiSkill>
- <https://github.com/isaac-sim/IsaacLab>
- <https://github.com/isaac-sim/IsaacLab/releases>
- <https://github.com/isaac-sim/IsaacSim>
- <https://github.com/jrouwe/JoltPhysics>
- <https://github.com/jrouwe/JoltPhysics/releases>
- <https://github.com/motphys>
- <https://github.com/mujocolab/mjlab>
- <https://github.com/newton-physics/newton>
- <https://github.com/newton-physics/newton/releases>
- <https://github.com/projectchrono/chrono/releases>
- <https://github.com/raisimTech/raisim2Lib>
- <https://github.com/raisimTech/raisimLib>
- <https://github.com/taichi-dev/taichi>
- <https://isaac-sim.github.io/IsaacLab/main/source/features/reproducibility.html>
- <https://isaac-sim.github.io/IsaacLab/release/3.0.0-beta2/source/overview/core-concepts/physical-backends/newton/index.html>
- <https://isaac-sim.github.io/IsaacLab/release/3.0.0/source/concepts/deformables.html>
- <https://isaac-sim.github.io/IsaacLab/release/3.0.0/source/concepts/ovphysx.html>
- <https://isaac-sim.github.io/IsaacLab/v3.0.0-EA/source/experimental-features/visuo_tactile_sensor.html>
- <https://www.marktechpost.com/2026/05/30/genesis-ai-releases-nyx-quadrants-and-genesis-world-1-0-physics-platform-for-scalable-robotics-foundation-model-evaluation/>
- <https://motrixsim.readthedocs.io/en/latest/index.html>
- <https://mujoco.readthedocs.io/en/3.7.0/changelog.html>
- <https://papers.neurips.cc/paper_files/paper/2025/hash/87d91d52272c3166315ca20b18519b9e-Abstract-Conference.html>
- <https://pi3g.com/nvidia-ai-enterprise-subscription-cost-in-2026/>
- <https://projectchrono.org/news/>
- <https://pypi.org/project/drake/>
- <https://pypi.org/project/genesis-world/>
- <https://pypi.org/project/mani-skill/>
- <https://pypi.org/project/mujoco-warp/>
- <https://pypi.org/project/mujoco/>
- <https://pypi.org/project/newton/>
- <https://pypi.org/project/ovphysx/>
- <https://pypi.org/project/pybullet/>
- <https://pypi.org/project/warp-lang/>
- <https://radiancefields.com/nvidia-s-isaac-sim-6.0-ships-with-nurec-gaussian-splatting>
- <https://raw.githubusercontent.com/google-deepmind/mujoco/main/doc/mjwarp/index.rst>
- <https://raw.githubusercontent.com/haosulab/ManiSkill/main/docs/source/user_guide/additional_resources/performance_benchmarking.md>
- <https://raw.githubusercontent.com/isaac-sim/IsaacLab/main/docs/source/overview/reinforcement-learning/performance_benchmarks.rst>
- <https://raw.githubusercontent.com/newton-physics/newton/main/docs/solvers/index.rst>
- <https://research.nvidia.com/publication/2025-01_tacsl-library-visuotactile-sensor-simulation-and-learning>
- <https://roboticsproceedings.org/rss21/p020.html>
- <https://roboticsproceedings.org/rss22/p093.html>
- <https://roboverse.wiki/metasim/features/support_matrix>
- <https://stoneztao.substack.com/p/the-new-hyped-genesis-simulator-is>
- <https://techcrunch.com/2026/05/06/khosla-backed-robotics-startup-genesis-ai-has-gone-full-stack-demo-shows/>
- <https://www.therobotreport.com/nvidia-launches-newton-physics-engine-gr00t-ai-corl-2025/>
- <https://www.uctoday.com/immersive-workplace-xr-tech/nvidia-omniverse-libraries-agent-toolkit-siggraph-2026/>
- <https://us.fitgap.com/products/omniverse>
- <https://x.com/linuxfoundation/status/2033674046349713474>

### 4.2 차량·드론·해양 시뮬레이션 (127건)

- <https://www.aap.com.au/aapreleases/globenewswire1000969676/>
- <https://aimotive.com/w/aimotive-unveils-aisim-5-pioneering-next-gen-autogi-for-adas/ad-simulation>
- <https://www.alphaxiv.org/abs/2607.14203>
- <https://www.ansys.com/blog/2026-r1-avxcelerate-sensors-software>
- <https://www.ansys.com/products/av-simulation/ansys-avxcelerate-sensors>
- <https://www.ansys.com/resource-center/webinar/leveraging-virtual-testing-for-ncap-2026-crash-avoidance-and-beyond>
- <https://api.chrono.projectchrono.org/vehicle_terrain_crm_api_.html>
- <https://api.projectchrono.org/wheeled_tire.html>
- <https://www.appliedintuition.com/news/mechanical-simulation-corporation>
- <https://ardupilot.org/dev/docs/sitl-with-gazebo.html>
- <https://arxiv.org/html/2501.12408v1>
- <https://arxiv.org/html/2503.01471v1>
- <https://arxiv.org/html/2510.06160v1>
- <https://arxiv.org/html/2511.07687v1>
- <https://arxiv.org/pdf/2307.05263>
- <https://arxiv.org/pdf/2503.01074>
- <https://arxiv.org/pdf/2506.09042>
- <https://www.asam.net/standards/detail/openlabel/>
- <https://www.asam.net/standards/detail/openmaterial/>
- <https://www.automotiveworld.com/news/nvidia-launches-alpamayo-2-super-open-reasoning-model/>
- <https://www.automotiveworld.com/news/wayve-unveils-gaia-2-cutting-edge-scalable-video-generation-for-assisted-and-automated-driving/>
- <https://www.automotiveworld.com/news/wayve-unveils-gaia-3-for-autonomous-driving-tests/>
- <https://www.autonomousvehicleinternational.com/news/simulation/sony-uses-rfpros-av-elevate-simulation-platform-to-demonstrate-next-gen-camera-technology.html>
- <https://www.autonomousvehicleinternational.com/news/software/nvidia-launches-alpamayo-2-super-for-reasoning-based-autonomous-driving.html>
- <https://www.autonomousvehicleinternational.com/news/testing/foretellix-integrates-foretify-data-automation-toolchain-with-nvidia-omniverse-blueprint-and-cosmos.html>
- <https://www.axios.com/2026/06/01/nvidia-ai-push-cosmos-3-world-model>
- <https://beamng.tech/blog/beamng-tech-039/>
- <https://blogs.nvidia.com/?p=76844>
- <https://blogs.nvidia.com/blog/drive-sim-nvidia-omniverse>
- <https://www.carahsoft.com/duality-ai>
- <https://carla.org/2024/12/19/release-0.10.0>
- <https://carla.org/2025/09/16/release-0.9.16>
- <https://www.cbinsights.com/company/cognata>
- <https://www.cimdata.com/en/industry-summary-articles/item/26787-applied-intuition-acquires-episci-strengthening-position-as-leader-in-all-domain-autonomy-software-for-national-security>
- <https://developer.nvidia.com/blog/accelerating-av-simulation-with-neural-reconstruction-and-world-foundation-models/>
- <https://dgist.elsevierpure.com/>
- <https://dgist.elsevierpure.com/en/publications/>
- <https://discourse.openrobotics.org/t/ros-news-for-the-week-of-september-29th-2025/50409>
- <https://docs.isaacsim.omniverse.nvidia.com/6.0.0/overview/release_notes.html>
- <https://docs.isaacsim.omniverse.nvidia.com/latest/common/license-faq.html>
- <https://docs.px4.io/v1.17/en/releases/1.16>
- <https://docs.px4.io/v1.17/en/releases/1.17>
- <https://documentation.beamng.com/beamng_tech/>
- <https://www.dspace.com/en/pub/home/news/dspace_pressroom/press/dspace-omnivision-2025.cfm>
- <https://www.dt.co.kr/article/11034257>
- <https://www.eenewseurope.com/en/rfpro-launches-simulator-for-autonomous-vehicle-development/>
- <https://www.electrive.com/2026/02/02/autonomy-startup-waabi-secures-750-million-and-partners-with-uber/>
- <https://www.emergentmind.com/papers/2606.03159>
- <https://en.wikipedia.org/wiki/Waabi>
- <https://finder.techleap.nl/news/feed/applied-intuition-raises-600m-at-15b-valuation>
- <https://www.foretellix.com/foretellix-raises-85-million-in-series-c-closing/>
- <https://www.foretellix.com/what-is-asam-openscenario-dsl>
- <https://forums.developer.nvidia.com/t/drive-sim-access-or-omniverse-truck-sim/289147>
- <https://forums.developer.nvidia.com/t/isaac-sim-6-0-general-availability/372621>
- <https://www.freightwaves.com/news/waabi-750m-series-c-unicorn>
- <https://functionbay.com/documentation/onlinehelp/Documents/mfswift.htm>
- <https://github.com/BeamNG/BeamNGpy>
- <https://github.com/Field-Robotics-Lab/dave>
- <https://github.com/NVIDIA/Cosmos>
- <https://github.com/NVlabs/alpamayo>
- <https://github.com/NVlabs/alpasim>
- <https://github.com/PegasusSimulator/PegasusSimulator>
- <https://github.com/carla-simulator/carla>
- <https://github.com/carla-simulator/carla/releases>
- <https://github.com/iamaisim/ProjectAirSim>
- <https://github.com/ntnu-arl/aerial_gym_simulator>
- <https://github.com/nv-tlabs/3dgrut>
- <https://github.com/nvidia-cosmos>
- <https://github.com/nvidia-cosmos/cosmos-predict2.5>
- <https://github.com/osrf/vrx>
- <https://github.com/patrykcieslak/stonefish>
- <https://github.com/projectchrono/chrono/releases/tag/10.0.0>
- <https://github.com/uos/radarays>
- <https://github.com/uzh-rpg/flightmare>
- <https://github.com/waymo-research/waymax>
- <https://www.globalpolicywatch.com/2026/05/un-regulation-and-gtr-on-automated-driving-systems-current-state-of-play/>
- <https://www.hellenicshippingnews.com/hd-hyundai-drives-koreas-shipbuilding-future-with-digital-twins-autonomy-ai-robots/>
- <https://hexagon.com/company/newsroom/press-releases/2025/hexagon-ramps-up-adas-software-innovation-with-cloud-native-quality-test-automation-solution>
- <https://holoocean.readthedocs.io/en/latest/changelog/changelog.html>
- <https://www.humanoidsdaily.com/news/tesla-ai-chief-details-unified-world-simulator-for-fsd-and-optimus>
- <https://ipg-automotive.com/fileadmin/data/applications/autonmous_vehicles/references/MOLIT_Autonomous_Vehicle-in-the-Loop.pdf>
- <https://www.ipg-automotive.com/press/press-detail/ipg-automotive-sets-new-standards-in-virtual-vehicle-development-with-carmaker-150>
- <https://www.iso.org/standard/78954.html>
- <https://www.iso.org/standard/83303.html>
- <https://itbrief.co.uk/story/hexagon-launches-cloud-based-test-drive-software-vtdx>
- <https://koreatechdesk.com/morai-an-autonomous-driving-simulation-technology-will-cooperate-with-m-city-an-experimental-city-dedicated-to-self-driving-in-the-u-s-to-verify-and-research-autonomous-driving-technology>
- <https://www.koreatimes.co.kr/business/companies/20250228/hd-hyundai-collaborates-with-palantir-siemens-for-ai-based-shipbuilding>
- <https://www.kuglermaag.com/news/iso-26262-v3/>
- <https://listmonk.beamng.com/archive/2026-tech-fourth-newsletter-6236>
- <https://www.mathworks.com/help/vdynblks/ref/combinedslipwheelcpi.html>
- <https://microsoft.github.io/AirSim/>
- <https://news.mtn.co.kr/news-detail/2026031917191428069>
- <https://news.un.org/en/story/2026/06/1167797>
- <https://www.newsseoul.co.kr/news/view/1065579017176859>
- <https://www.newsseoul.co.kr/news/view/1065579620501557>
- <https://www.newswire.ca/news-releases/inverted-ai-secures-seed-round-for-generative-ai-in-av-adas-development-845079282.html>
- <https://nexus.hexagon.com/home/product/virtual-test-drive>
- <https://www.nvidia.com/en-sg/use-cases/autonomous-vehicle-simulation/>
- <https://www.nvidia.com/en-us/agreements/enterprise-software/nvidia-open-model-license>
- <https://openscenario.asam.net/ASAM_OpenSCENARIO_DSL/latest/introduction.html>
- <https://pi3g.com/nvidia-ai-enterprise-subscription-cost-in-2026/>
- <https://projectchrono.org/news/>
- <https://radiancefields.com/aimotive-brings-relightable-gaussian-splatting-to-aisim-6-with-pbr-splatting>
- <https://radiancefields.com/carla-adds-nurec-support-with-v0-9-16>
- <https://radiancefields.com/nvidia-omniverse-nurec-reaches-general-availability>
- <https://radiancefields.com/wayve-announces-prism-1>
- <https://www.remcom.com/articles-and-papers/auto-radar-drive-scenario-simulation-increasing-realism-with-multipath-diffuse-scattering-and-micro-doppler>
- <https://research.nvidia.com/labs/cosmos-lab/cosmos-predict2.5>
- <https://research.nvidia.com/labs/sil/projects/omnidreams-blog/>
- <https://sacra.com/research/applied-intuition-at-830m-year/>
- <https://sbel.wisc.edu/2025/10/04/sbel-researchers-develop-chronocrm-simulator-for-fast-and-scalable-rover-terrain-interaction/>
- <https://www.tech42.co.kr/?p=85819>
- <https://techcrunch.com/?p=1733822>
- <https://techcrunch.com/?p=3079883>
- <https://the-decoder.com/waymo-taps-google-deepminds-genie-3-to-simulate-driving-scenarios-its-cars-have-never-seen/>
- <https://thebrakereport.com/euro-ncap-unveils-major-2026-safety-testing-protocols/>
- <https://thedigitalship.com/news/electronics-navigation/samsung-ai-ship-crosses-pacific-on-its-own/>
- <https://www.therobotreport.com/duality-ai-continues-work-with-nasa-jpl-darpa-racer-program/>
- <https://www.therobotreport.com/morai-raises-208m-autonomous-driving-simulation/>
- <https://thevc.kr/morai>
- <https://www.ul.com/news/ul-4600-edition-3-updates-incorporate-autonomous-trucking>
- <https://www.unrealengine.com/en-US/blog/we-are-updating-unreal-engine-twinmotion-and-realitycapture-pricing-in-late-april>
- <https://www.unrealengine.com/spotlights/dspace-drives-advancements-in-autonomous-vehicle-testing>
- <https://www.vehicledynamicsinternational.com/news/simulation/ipg-automotive-releases-carmaker-15-0-for-virtual-vehicle-development.html>
- <https://waymo.com/blog/2026/02/the-waymo-world-model-a-new-frontier-for-autonomous-driving-simulation>
- <https://waymo.com/open/about>
- <https://winbuzzer.com/2026/03/17/nvidia-gtc-2026-uber-robotaxi-physical-ai-drive-hyperion-xcxwbn/>

### 4.3 시각·센서 현실감, Real2Sim (114건)

- <https://80.lv/articles/aswf-adobe-autodesk-released-openpbr-1-0>
- <https://80.lv/articles/unity-unveils-2026-render-pipelines-strategy/>
- <https://aecmag.com/reality-capture-modelling/khronos-announces-gltf-gaussian-splatting-extension/>
- <https://ai.meta.com/blog/sam-3d/>
- <https://aiwiki.ai/wiki/gaia_3_wayve>
- <https://www.alphaxiv.org/abs/2603.23973.md>
- <https://alternativeto.net/news/2025/11/blender-5-0-launches-with-aces-color-enhanced-rendering-and-tighter-vfx-integration/>
- <https://app.cinevva.com/news/2026-01-05-webgpu-era>
- <https://arxiv.org/abs/2606.31101>
- <https://arxiv.org/html/2411.07375v1>
- <https://arxiv.org/html/2501.18982v1>
- <https://arxiv.org/html/2508.17643v1>
- <https://arxiv.org/html/2511.04665v2>
- <https://arxiv.org/html/2602.18525v1>
- <https://arxiv.org/pdf/2006.07722>
- <https://arxiv.org/pdf/2304.06706>
- <https://arxiv.org/pdf/2311.12198>
- <https://arxiv.org/pdf/2406.08474>
- <https://arxiv.org/pdf/2510.11689>
- <https://arxiv.org/pdf/2511.10647>
- <https://arxiv.org/pdf/2511.13648>
- <https://arxiv.org/pdf/2512.16881>
- <https://arxiv.org/pdf/2602.09153>
- <https://arxiv.org/pdf/2603.16866>
- <https://arxiv.org/pdf/2607.08098>
- <https://arxiv.org/pdf/2609.03304>
- <https://www.automotiveworld.com/news/wayve-unveils-gaia-3-for-autonomous-driving-tests/>
- <https://www.autonomousvehicleinternational.com/news/ai-sensor-fusion/wayves-gaia-3-generative-world-model-now-available-for-autonomous-driving-validation.html>
- <https://cgworld.jp/flashnews/01-202603-Spark2.html>
- <https://cgworld.jp/flashnews/202501-MaterialX1392.html>
- <https://comfyui-wiki.com/news/2025-12-18-microsoft-trellis2-3d-generation>
- <https://costbench.com/software/ai-3d-generation/meshy/>
- <https://datanorth.ai/news/nvidia-launches-cosmos-3>
- <https://developer.nvidia.com/blog/revolutionizing-neural-reconstruction-and-rendering-in-gsplat-with-3dgut/>
- <https://developer.nvidia.com/omniverse/nurec>
- <https://digitalproduction.com/2026/01/28/godot-4-6-arrives-with-major-cg-friendly-updates/>
- <https://docs.api.nvidia.com/nim/re/reference/nvidia-cosmos-1_0-diffusion-7b>
- <https://docs.isaacsim.omniverse.nvidia.com/6.0.0/overview/release_notes.html>
- <https://docs.isaacsim.omniverse.nvidia.com/latest/py/source/extensions/isaacsim.sensors.experimental.rtx/docs/index.html>
- <https://docs.nvidia.com/learning/physical-ai/sim-to-real-so-101/latest/14-strategy3-cosmos.html>
- <https://docs.omniverse.nvidia.com/materials-and-rendering/latest/rtx-renderer_rt_overview.html>
- <https://docs.worldlabs.ai/marble/export/gaussian-splat.md>
- <https://dupple.com/reviews/rodin-ai>
- <https://www.edge-ai-vision.com/2025/08/nvidia-opens-portals-to-world-of-robotics-with-new-omniverse-libraries-cosmos-physical-ai-models-and-ai-computing-infrastructure/>
- <https://www.emergentmind.com/papers/2605.22467>
- <https://en.wikipedia.org/wiki/Genie_(world_model>
- <https://www.fast.io/resources/stability-ai-review-2026.md>
- <https://gamedev.net/news/2274-blender-51-release/>
- <https://gamedev.net/news/3999-unreal-engine-58-released/>
- <https://github.com/Anttwo/MILo>
- <https://github.com/ByteDance-Seed/Depth-Anything-3>
- <https://github.com/NVIDIA/Cosmos>
- <https://github.com/NVIDIA/Cosmos/blob/main/LICENSE>
- <https://github.com/NVlabs/alpasim>
- <https://github.com/NVlabs/instant-ngp>
- <https://github.com/NVlabs/neuralangelo>
- <https://github.com/SarahWeiii/CoACD>
- <https://github.com/Taccel-Simulator/Taccel>
- <https://github.com/Tencent-Hunyuan/Hunyuan3D-2.1>
- <https://github.com/XPandora/PhysGaussian>
- <https://github.com/facebookresearch/map-anything>
- <https://github.com/facebookresearch/sam-3d-objects>
- <https://github.com/facebookresearch/vggt>
- <https://github.com/isaac-sim/IsaacLab/releases>
- <https://github.com/isaac-sim/IsaacSim>
- <https://github.com/isaac-sim/IsaacSim/releases>
- <https://github.com/microsoft/TRELLIS>
- <https://github.com/microsoft/TRELLIS.2>
- <https://github.com/nerfstudio-project/gsplat>
- <https://github.com/nerfstudio-project/nerfstudio>
- <https://github.com/nv-tlabs/3dgrut>
- <https://github.com/nv-tlabs/3dgrut/releases>
- <https://github.com/nvidia-cosmos/cosmos-predict2.5>
- <https://github.com/nvidia-cosmos/cosmos-transfer2.5>
- <https://github.com/openvdb/fvdb-reality-capture>
- <https://github.com/sparkjsdev/spark>
- <https://github.com/vlongle/articulate-anything>
- <https://github.com/ziangcao0312/PhysX-Anything>
- <https://help.scenario.com/articles/5967392966-hunyuan-3d-models-the-essentials>
- <https://invideo.io/blog/world-labs-marble-3d-worlds/>
- <https://isaac-sim.github.io/IsaacLab/release/3.0.0/source/experimental-features/visuo_tactile_sensor.html>
- <https://www.krea.ai/blog/best-ai-3d-model-generators-2026>
- <https://www.kucoin.com/news/flash/decart-launches-oasis-3-for-photorealistic-driving-simulations-via-api>
- <https://labs.invenglobal.com/articles/22900/unreal-engine-6-to-feature-fundamental-overhaul-targeting-early-access-release-by-late-2027>
- <https://letsdatascience.com/news/deepmind-opens-project-genie-for-interactive-worlds-eb2fec7e>
- <https://metavert.io/compare/gaussian-splatting-vs-neural-radiance-fields>
- <https://openaccess.thecvf.com/content/ICCV2025/html/Jiang_PhysTwin_Physics-Informed_Reconstruction_and_Simulation_of_Deformable_Objects_from_Videos_ICCV_2025_paper.html>
- <https://papers.neurips.cc/paper_files/paper/2025/hash/87d91d52272c3166315ca20b18519b9e-Abstract-Conference.html>
- <https://pasqualepillitteri.it/en/news/3945/nvidia-cosmos-3-physical-ai>
- <https://www.phoronix.com/search/Godot%204>
- <https://playground.roboflow.com/models/meta/sam-3d-objects>
- <https://radiancefields.com/nvidia-advances-fvdb-with-major-0.4-release-ahead-of-gtc>
- <https://radiancefields.com/nvidia-s-isaac-sim-6.0-ships-with-nurec-gaussian-splatting>
- <https://radiancefields.com/nvidia-unveils-alpasim-at-ces>
- <https://radiancefields.com/openusd-26.03-adds-native-gaussian-splat-support>
- <https://radiancefields.com/playcanvas-releases-supersplat-3.0>
- <https://radiancefields.com/xgrids-adds-real-time-lights-and-shadows-to-gaussian-splats-in-lcc-unity-sdk-2.2.0>
- <https://radiancefields.com/yags-yandex-open-sources-a-3dgs-plugin-for-unreal-engine-5.5–5.7>
- <https://raw.githubusercontent.com/NVlabs/nvdiffrast/main/LICENSE.txt>
- <https://raw.githubusercontent.com/Tencent-Hunyuan/Hunyuan3D-2.1/main/LICENSE>
- <https://raw.githubusercontent.com/graphdeco-inria/gaussian-splatting/main/LICENSE.md>
- <https://raw.githubusercontent.com/hbb1/2d-gaussian-splatting/main/LICENSE.md>
- <https://raw.githubusercontent.com/zju3dv/PGSR/main/LICENSE.md>
- <https://research.nvidia.com/labs/cosmos-lab/cosmos-predict2.5/>
- <https://research.nvidia.com/labs/cosmos-lab/cosmos3/technical-report.pdf>
- <https://research.nvidia.com/publication/2025-01_tacsl-library-visuotactile-sensor-simulation-and-learning>
- <https://www.robotics247.com/article/nvidia-gtc-2026-nvidia-global-robotics-leaders-look-to-take-physical-ai-to-the-real-world>
- <https://runwayml.com/research/introducing-runway-gwm-1>
- <https://simready.artlabs.ai/compare/v-hacd-vs-coacd-vs-manual-hulls>
- <https://stability.ai/license>
- <https://startupfortune.com/decart-opens-its-world-model-to-developers-for-two-cents-a-second-betting-it-can-own-physical-ais-simulation-layer-before-the-big-players-build-one-themselves/>
- <https://unity.com/topics/render-pipelines-strategy-for-2026>
- <https://www.unrealengine.com/news/unreal-engine-5-7-is-now-available>
- <https://yourstory.com/ai-story/google-deepmind-project-genie-launch>

### 4.4 플랫폼 아키텍처·표준·클라우드 (80건)

- <https://aousd.org/uncategorized/foundations-of-open-3d-development-introducing-aousd-core-specification-1-0/>
- <https://dataconomy.com/2026/03/17/nvidia-launches-newton-1-0-physics-engine-for-industrial-robot-training/>
- <https://developer.nvidia.com/blog/integrate-physical-ai-capabilities-into-existing-apps-with-nvidia-omniverse-libraries/>
- <https://discourse.openrobotics.org/t/ros-2-lyrical-luth-and-11-years-of-fast-dds-as-ros-2-default-middleware/55062>
- <https://docs.ros.org/en/lyrical/Releases/Release-Lyrical-Luth.html>
- <https://forums.developer.nvidia.com/t/omniverse-launcher-update/321326>
- <https://github.com/BabylonJS/Babylon.js/releases>
- <https://github.com/EpicGamesExt/PixelStreamingInfrastructure>
- <https://github.com/KhronosGroup/glTF/tree/main/extensions>
- <https://github.com/Lichtblick-Suite/lichtblick>
- <https://github.com/NVIDIA-Omniverse>
- <https://github.com/NVIDIA-Omniverse-blueprints/digital-twins-for-fluid-simulation>
- <https://github.com/NVIDIA-Omniverse-blueprints/omniverse-dsx-blueprint-for-ai-factories>
- <https://github.com/NVIDIA-Omniverse/IsaacSim-ros_workspaces>
- <https://github.com/NVIDIA-Omniverse/PhysX>
- <https://github.com/NVIDIA-Omniverse/kit-app-template>
- <https://github.com/NVIDIA-Omniverse/kit-usd-agents>
- <https://github.com/NVIDIA-Omniverse/ovrtx>
- <https://github.com/NVIDIA-Omniverse/ovstorage>
- <https://github.com/NVIDIA-Omniverse/usd-exchange>
- <https://github.com/NVIDIA-Omniverse/web-viewer-sample>
- <https://github.com/NVIDIA/KAI-Scheduler>
- <https://github.com/NVIDIA/KAI-Scheduler/releases>
- <https://github.com/NVIDIA/OSMO>
- <https://github.com/NVIDIA/OSMO/releases>
- <https://github.com/NVIDIA/gpu-operator/releases>
- <https://github.com/NVIDIA/k8s-dra-driver-gpu>
- <https://github.com/OpenModelica/OpenModelica/releases>
- <https://github.com/OpenSimulationInterface/open-simulation-interface/releases>
- <https://github.com/PixarAnimationStudios/OpenUSD/releases>
- <https://github.com/SlinkyProject/slurm-operator>
- <https://github.com/adobe/USD-Fileformat-plugins>
- <https://github.com/ahujasid/blender-mcp>
- <https://github.com/aousd/specifications-public>
- <https://github.com/carla-simulator/carla/releases>
- <https://github.com/chongdashu/unreal-mcp>
- <https://github.com/eclipse-ditto/ditto/releases>
- <https://github.com/foxglove/mcap>
- <https://github.com/gazebosim/gz-sim/releases>
- <https://github.com/gazebosim/ros_gz>
- <https://github.com/gazebosim/sdformat/releases>
- <https://github.com/google-deepmind/mujoco/releases>
- <https://github.com/google-deepmind/mujoco/tree/main/src/experimental/usd>
- <https://github.com/google-deepmind/mujoco_warp/releases>
- <https://github.com/huggingface/lerobot/releases>
- <https://github.com/influxdata/influxdb/releases>
- <https://github.com/isaac-sim/IsaacLab>
- <https://github.com/isaac-sim/IsaacLab/releases/tag/v3.0.0-EA>
- <https://github.com/isaac-sim/IsaacSim>
- <https://github.com/isaac-sim/IsaacSim/releases>
- <https://github.com/modelcontextprotocol/modelcontextprotocol>
- <https://github.com/modelica/fmi-standard/releases>
- <https://github.com/modelica/ssp-standard>
- <https://github.com/mrdoob/three.js/releases>
- <https://github.com/nerfstudio-project/viser>
- <https://github.com/newton-physics>
- <https://github.com/newton-physics/newton>
- <https://github.com/newton-physics/newton-usd-schemas>
- <https://github.com/newton-physics/newton/releases>
- <https://github.com/omni-mcp/isaac-sim-mcp>
- <https://github.com/open62541/open62541/releases>
- <https://github.com/playcanvas/engine/releases>
- <https://github.com/ray-project/ray/releases>
- <https://github.com/rerun-io/rerun/releases>
- <https://github.com/robotmcp/ros-mcp-server>
- <https://github.com/ros2/rmw_zenoh>
- <https://github.com/ros2/ros2_documentation/blob/rolling/source/Releases.rst>
- <https://github.com/ros2/rosbag2>
- <https://github.com/selkies-project/selkies>
- <https://github.com/skypilot-org/skypilot>
- <https://github.com/skypilot-org/skypilot-catalog>
- <https://github.com/sparkjsdev/spark>
- <https://github.com/timescale/timescaledb>
- <https://github.com/treeverse/lakeFS/releases>
- <https://github.com/treeverse/lakeFS/releases/tag/v1.87.0>
- <https://www.linuxfoundation.org/press/aousd_prmarch2026>
- <https://raw.githubusercontent.com/NVIDIA-Omniverse/PhysX/main/README.md>
- <https://raw.githubusercontent.com/NVIDIA-Omniverse/kit-app-template/main/CHANGELOG.md>
- <https://raw.githubusercontent.com/PixarAnimationStudios/OpenUSD/release/CHANGELOG.md>
- <https://raw.githubusercontent.com/huggingface/lerobot/main/docs/source/lerobot-dataset-v3.mdx>

### 4.5 모델 학습 레이어 (94건)

- <https://arxiv.org/abs/2109.11978>
- <https://deepmind.google/discover/blog/genie-3-a-new-frontier-for-world-models/>
- <https://www.figure.ai/news/helix>
- <https://github.com/DLR-RM/BlenderProc>
- <https://github.com/Genesis-Embodied-AI/Genesis>
- <https://github.com/HybridRobotics/motion_tracking_controller>
- <https://github.com/HybridRobotics/whole_body_tracking>
- <https://github.com/NVIDIA-AI-IOT/synthetic_data_generation_training_workflow>
- <https://github.com/NVIDIA-Omniverse/synthetic-data-examples>
- <https://github.com/NVIDIA/Cosmos>
- <https://github.com/NVIDIA/Cosmos/blob/main/README.md>
- <https://github.com/NVIDIA/Isaac-GR00T>
- <https://github.com/NVIDIA/Isaac-GR00T/blob/main/README.md>
- <https://github.com/NVIDIA/Isaac-GR00T/tree/main/examples>
- <https://github.com/NVIDIA/IsaacTeleop>
- <https://github.com/NVlabs/DEXTRAH>
- <https://github.com/NVlabs/GR00T-WholeBodyControl>
- <https://github.com/NVlabs/HOVER>
- <https://github.com/NVlabs/dexmimicgen>
- <https://github.com/NVlabs/mimicgen>
- <https://github.com/OpenDriveLab/AgiBot-World>
- <https://github.com/Physical-Intelligence/openpi>
- <https://github.com/Physical-Intelligence/openpi/blob/main/examples/libero/README.md>
- <https://github.com/PufferAI/PufferLib>
- <https://github.com/RLWRLD>
- <https://github.com/RLWRLD/RLDX-1>
- <https://github.com/RLinf/RLinf>
- <https://github.com/StanfordVL/BEHAVIOR-1K>
- <https://github.com/Toni-SM/skrl>
- <https://github.com/danijar/dreamerv3>
- <https://github.com/facebookresearch/sam3>
- <https://github.com/facebookresearch/vjepa2>
- <https://github.com/google-deepmind/gemini-robotics-sdk>
- <https://github.com/google-deepmind/mujoco_playground>
- <https://github.com/google-research/kubric>
- <https://github.com/haosulab/ManiSkill>
- <https://github.com/huggingface/lerobot/releases>
- <https://github.com/isaac-sim/IsaacLab>
- <https://github.com/isaac-sim/IsaacLab-Arena>
- <https://github.com/isaac-sim/IsaacLab/blob/main/source/isaaclab_mimic/config/extension.toml>
- <https://github.com/isaac-sim/IsaacLab/releases>
- <https://github.com/isaac-sim/IsaacLab/releases/tag/v3.0.0-EA>
- <https://github.com/isaac-sim/IsaacSim>
- <https://github.com/leggedrobotics/legged_gym>
- <https://github.com/leggedrobotics/rsl_rl/releases>
- <https://github.com/meta-pytorch/LeanRL>
- <https://github.com/moojink/openvla-oft>
- <https://github.com/mujocolab/mjlab>
- <https://github.com/newton-physics/newton>
- <https://github.com/newton-physics/newton/releases>
- <https://github.com/nvidia-cosmos/cosmos-predict2.5>
- <https://github.com/nvidia-cosmos/cosmos-transfer2.5>
- <https://github.com/openvla/openvla>
- <https://github.com/orgs/nvidia-cosmos/repositories>
- <https://github.com/robo-arena/roboarena>
- <https://github.com/robocasa/robocasa>
- <https://github.com/roboflow/rf-detr>
- <https://github.com/simpler-env/SimplerEnv>
- <https://github.com/thu-ml/RDT2>
- <https://github.com/ultralytics/ultralytics>
- <https://github.com/wuphilipp/gello_software>
- <https://pypi.org/project/blenderproc/>
- <https://pypi.org/project/brax/>
- <https://pypi.org/project/genesis-world/>
- <https://pypi.org/project/isaaclab/>
- <https://pypi.org/project/isaacsim/>
- <https://pypi.org/project/kubric/>
- <https://pypi.org/project/lerobot/>
- <https://pypi.org/project/libero/>
- <https://pypi.org/project/mani-skill/>
- <https://pypi.org/project/mjlab/>
- <https://pypi.org/project/mlflow/>
- <https://pypi.org/project/mujoco-warp/>
- <https://pypi.org/project/newton-physics/>
- <https://pypi.org/project/onnxruntime/>
- <https://pypi.org/project/playground/>
- <https://pypi.org/project/pufferlib/>
- <https://pypi.org/project/ray/>
- <https://pypi.org/project/rl-games/>
- <https://pypi.org/project/rlinf/>
- <https://pypi.org/project/rsl-rl-lib/>
- <https://pypi.org/project/skrl/>
- <https://pypi.org/project/stable-baselines3/>
- <https://pypi.org/project/tensorrt/>
- <https://pypi.org/project/torchrl/>
- <https://pypi.org/project/wandb/>
- <https://raw.githubusercontent.com/huggingface/lerobot/main/README.md>
- <https://raw.githubusercontent.com/huggingface/lerobot/main/docs/source/lerobot-dataset-v3.mdx>
- <https://raw.githubusercontent.com/huggingface/lerobot/main/docs/source/smolvla.mdx>
- <https://raw.githubusercontent.com/isaac-sim/IsaacLab/main/docs/source/overview/imitation-learning/teleop_imitation.rst>
- <https://raw.githubusercontent.com/isaac-sim/IsaacLab/main/docs/source/overview/reinforcement-learning/performance_benchmarks.rst>
- <https://raw.githubusercontent.com/isaac-sim/IsaacLab/main/docs/source/overview/reinforcement-learning/rl_frameworks.rst>
- <https://raw.githubusercontent.com/moojink/openvla-oft/main/LIBERO.md>
- <https://raw.githubusercontent.com/mujocolab/mjlab/main/README.md>

### 4.6 시장·경쟁 구도 (30건)

- <https://github.com/DoosanRobotics>
- <https://github.com/Genesis-Embodied-AI/Genesis>
- <https://github.com/Genesis-Embodied-AI/Genesis/releases>
- <https://github.com/MORAI-Autonomous>
- <https://github.com/MicrosoftDocs/azure-docs/blob/main/articles/digital-twins/overview.md>
- <https://github.com/MicrosoftDocs/azure-docs/tree/main/articles/digital-twins>
- <https://github.com/MicrosoftDocs/fabric-docs/blob/main/docs/real-time-intelligence/digital-twin-builder/overview.md>
- <https://github.com/NVIDIA-Omniverse>
- <https://github.com/NVIDIA-Omniverse-blueprints>
- <https://github.com/NVIDIA-Omniverse/usd-content-agents>
- <https://github.com/NVIDIA/Isaac-GR00T>
- <https://github.com/Physical-Intelligence/openpi>
- <https://github.com/aws-samples/aws-iot-twinmaker-samples>
- <https://github.com/carla-simulator/carla/releases>
- <https://github.com/google-deepmind/mujoco/releases>
- <https://github.com/haosulab/ManiSkill>
- <https://github.com/isaac-sim/IsaacLab/releases>
- <https://github.com/isaac-sim/IsaacLab/releases/tag/v3.0.0-beta>
- <https://github.com/isaac-sim/IsaacSim>
- <https://github.com/isaac-sim/IsaacSim/releases>
- <https://github.com/lightwheelai>
- <https://github.com/newton-physics/newton>
- <https://github.com/newton-physics/newton/releases>
- <https://github.com/newton-physics/newton/releases?page=2>
- <https://github.com/nvidia-cosmos>
- <https://github.com/parallel-domain>
- <https://github.com/wayveai>
- <https://www.marketsandmarkets.com/Market-Reports/digital-twin-market-225269522.html>
- <https://pypi.org/project/anatools/>
- <https://pypi.org/project/isaacsim/>

### 4.7 국내 정책·자금·GTM (51건)

- <https://www.aica-gj.kr>
- <https://www.aihub.or.kr>
- <https://www.aivoucher.kr>
- <https://aws.amazon.com/activate/>
- <https://cloud.google.com/startup>
- <https://www.dapa.go.kr>
- <https://dart.fss.or.kr>
- <https://docs.isaacsim.omniverse.nvidia.com/latest/installation/requirements.html>
- <https://ec.europa.eu/info/funding-tenders/opportunities/portal>
- <https://www.exportvoucher.com>
- <https://www.fsc.go.kr>
- <https://www.iitp.kr>
- <https://www.iris.go.kr>
- <https://isms.kisa.or.kr>
- <https://www.iso.org/committee/6483279.html>
- <https://www.iso.org/standard/75066.html>
- <https://www.jointips.or.kr>
- <https://www.k-startup.go.kr>
- <https://kdata.or.kr/datavoucher>
- <https://www.kdata.or.kr>
- <https://www.keit.re.kr>
- <https://www.kiat.or.kr>
- <https://www.kiria.org>
- <https://www.kotra.or.kr>
- <https://www.kotsa.or.kr>
- <https://www.krit.re.kr>
- <https://www.ksc.re.kr>
- <https://www.kvic.or.kr>
- <https://www.law.go.kr>
- <https://www.meti.go.jp>
- <https://www.microsoft.com/en-us/startups>
- <https://www.moef.go.kr>
- <https://www.mof.go.kr>
- <https://www.mois.go.kr>
- <https://www.molit.go.kr>
- <https://www.motie.go.kr>
- <https://www.msit.go.kr>
- <https://www.mss.go.kr>
- <https://www.navercorp.com>
- <https://www.nia.or.kr>
- <https://www.nipa.kr>
- <https://www.nvidia.com/en-us/omniverse/>
- <https://www.nvidia.com/en-us/startups/>
- <https://nvidianews.nvidia.com/news/south-korea-ai-infrastructure>
- <https://www.pipc.go.kr>
- <https://www.pps.go.kr>
- <https://research-and-innovation.ec.europa.eu>
- <https://www.rnd.or.kr>
- <https://www.smtech.go.kr>
- <https://www.tta.or.kr>
- <https://www.whitehouse.gov>

### 4.8 Build vs Buy·라이선스·비용 (45건)

- <https://github.com/EpicGames/PixelStreamingInfrastructure>
- <https://github.com/Genesis-Embodied-AI/Genesis>
- <https://github.com/Genesis-Embodied-AI/Genesis/blob/v0.2.1/README.md>
- <https://github.com/NVIDIA-Omniverse/PhysX>
- <https://github.com/NVIDIA-Omniverse/kit-app-template>
- <https://github.com/NVIDIA/Cosmos>
- <https://github.com/NVlabs/curobo/blob/main/LICENSE>
- <https://github.com/RobotLocomotion/drake>
- <https://github.com/carla-simulator/carla>
- <https://github.com/carla-simulator/carla/releases>
- <https://github.com/gazebosim/gz-sim>
- <https://github.com/google-deepmind/mujoco>
- <https://github.com/google-deepmind/mujoco/blob/main/doc/overview.rst>
- <https://github.com/google-deepmind/mujoco/releases>
- <https://github.com/google-deepmind/mujoco_playground>
- <https://github.com/google-deepmind/mujoco_warp/blob/main/benchmarks/README.md>
- <https://github.com/isaac-sim/IsaacLab>
- <https://github.com/isaac-sim/IsaacLab/blob/main/docs/source/overview/reinforcement-learning/performance_benchmarks.rst>
- <https://github.com/isaac-sim/IsaacLab/releases>
- <https://github.com/isaac-sim/IsaacLab/releases/tag/v3.0.0-EA>
- <https://github.com/isaac-sim/IsaacSim>
- <https://github.com/isaac-sim/IsaacSim/blob/develop/LICENSE>
- <https://github.com/isaac-sim/IsaacSim/blob/develop/tools/docker/README.md>
- <https://github.com/isaac-sim/IsaacSim/releases>
- <https://github.com/newton-physics/newton>
- <https://github.com/newton-physics/newton-governance>
- <https://github.com/newton-physics/newton/releases>
- <https://github.com/nvidia-cosmos>
- <https://github.com/nvidia-cosmos/cosmos-predict2.5>
- <https://github.com/projectchrono/chrono>
- <https://github.com/skypilot-org/skypilot-catalog>
- <https://github.com/skypilot-org/skypilot-catalog/commits/master>
- <https://pypi.org/project/genesis-world/>
- <https://pypi.org/project/gs-nyx/>
- <https://pypi.org/project/isaacsim/>
- <https://pypi.org/project/isaacsim/#history>
- <https://pypi.org/project/mujoco-warp/>
- <https://pypi.org/project/newton/>
- <https://pypi.org/project/newton/#history>
- <https://pypi.org/project/ovphysx/>
- <https://pypi.org/project/ovrtx/>
- <https://pypi.org/project/warp-lang/>
- <https://raw.githubusercontent.com/RobotLocomotion/drake/master/LICENSE.TXT>
- <https://raw.githubusercontent.com/isaac-sim/IsaacSim/develop/VERSION>
- <https://raw.githubusercontent.com/projectchrono/chrono/main/LICENSE>

**총 고유 출처: 545건**

## 결정 사항 및 다음 액션

| 액션 | 책임 | 기한 |
|---|---|---|
| NVIDIA 약관 서면 확인(SaaS·온프렘·산출물·텔레메트리) | CEO + 얼라이언스·라이선스 매니저 | M3 1차, M10 최종 |
| [U] 정책·시장 수치를 공고·공시·1차 보도로 재검증 | BD·정부과제 담당 | IR·제안서 제출 전 |
| GPUSimBench·GAUGE 원문 검토와 사내 충실도 벤치마크 설계 | Head of Fidelity | M2 |
| 국내 CSP RT GPU 견적·드라이버 이미지 실측 | Platform Lead | M2 |
| 출처 목록을 분기마다 갱신(엔진 릴리스·약관 변경 추적) | CTO | 분기 |

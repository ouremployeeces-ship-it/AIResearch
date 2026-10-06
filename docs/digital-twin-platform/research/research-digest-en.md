# RESEARCH CORE DIGEST (as of 2026-10-06)

NOTE: Researchers hit a shared web-search budget cap and a proxy that blocked many vendor/news/Korean-gov sites. GitHub/PyPI facts are high-confidence; market sizes, funding, Korean program budgets, vendor list prices are medium/low and must be flagged "검증 필요" in final docs.

## FACT-CHECK: critical warnings
- VERIFICATION SCOPE: The shared web-search budget was used up (200 calls per turn), and the egress proxy blocked almost everything except github.com, raw.githubusercontent.com and pypi.org. Blocked sources include nvidia.com (docs, forums, blogs, newsroom), arxiv, huggingface, unrealengine.com, all
  Korean government and news sites, and press sites. So every Korean policy figure, funding or valuation figure, license price (NVAIE, Omniverse Enterprise, UE, Unity), NVIDIA blog benchmark ratio, and 2026 arXiv paper in the digest is UNVERIFIED. These must be re-checked before any CEO or board
  decision or grant application.
- KIT-LESS IS NOT LICENSE-FREE: ovphysx pip binaries (LicenseRef-NVIDIA-Omniverse), ovrtx (LicenseRef-NvidiaProprietary), ovstage (LicenseRef-NvidiaProprietary), and even the isaacsim and isaaclab PyPI wheels ('NVIDIA Proprietary Software') carry proprietary terms. Only Newton + MuJoCo/MJWarp + Warp
  (Apache-2.0) + Isaac Lab built from GitHub source (BSD-3) + the PhysX SDK built from source (now Apache-2.0) form a fully permissive stack. The build_vs_buy 'Strategy D' licensing score (4/5) only holds if the OVPhysX and OVRTX backends are excluded from the SaaS tier.
- The central SaaS licensing claim (NVAIE is required to offer Isaac Sim or Kit as a service; selling outputs is exempt) could NOT be read from a primary source. Only the LICENSE preamble ('Isaac Sim Additional Software and Materials License' for Kit, models and textures) was verified. The
  $4,500/GPU/yr list price and the '$1,125 Inception 75% discount' are also unverified. Get written terms from NVIDIA Korea covering (a) multi-tenant browser streaming SaaS, (b) on-prem delivery to Korean enterprise or defense customers (= redistribution), and (c) dataset-only sales.
- Hunyuan3D 2.1's license explicitly excludes South Korea, including use of outputs. AICHEMIST cannot use it for the NeRF/photo-to-3D marketplace pipeline. Other non-commercial traps verified: Inria 3DGS (and 2DGS/MILo derivatives), Instant-NGP, nvdiffrast (a hard dependency of the MIT-licensed
  TRELLIS.2), MimicGen code, PhysX-Anything (S-Lab), ManiSkill assets, AgiBot World/GO-1, Waymax/WOD, RLDX-1 weights, DA3-Large/Giant, original VGGT-1B. openpi weight terms are unstated. Use gsplat or 3DGRUT (Apache-2.0), VGGT-1B-Commercial, DA3 Small/Base/Metric/Mono, MapAnything-apache.
- cuRobo licensing conflict: upstream NVlabs/curobo is now Apache-2.0, but Isaac Lab still ships cuRobo under the 'Isaac Lab Additional Software and Materials License', which forbids use outside Isaac Lab. Any SkillGen or motion-planning feature in CEN needs a pinned Apache-tagged cuRobo and NVIDIA
  confirmation.
- On-prem or air-gapped delivery, which Korean chaebol and defense customers commonly require, counts as DISTRIBUTION. That triggers GPL-3.0 obligations (BlenderProc, Stonefish), Isaac Sim/Kit redistribution terms and Epic EULA terms that pure SaaS may avoid. AGPL-3.0 (Ultralytics YOLO) is triggered
  by network SaaS use as well. The SAM License (SAM 3D, SAM 3) forbids ITAR and trade-control-prohibited end uses, which affects any Korean defense or ADD vertical.
- GPU pool split is confirmed: Isaac Sim, ovrtx and Kit need RT-core RTX GPUs (datacenter A40 min, L40S recommended, RTX PRO 6000 Blackwell best). H100/H200/B200 do not appear in any requirement list. Government-allocated B200/H200 capacity can cover training but not RTX sensor or SDG rendering.
  Verified AWS Seoul rates are 23-38% above us-east-1 (L40S $2.288/h, RTX PRO 6000 $4.135/h, 8×H100 $75.96/h). The $0.84/h MIG-split streaming cost is untested.
- Driver floor: warp-lang 1.18 (Newton's core dependency) now needs a Turing+ GPU and an R580+ driver (CUDA 13.4 wheels). The Newton README's 'Maxwell+, driver 545' is stale. Cloud images and Korean-CSP GPU nodes must be checked for R580+ drivers.
- Benchmark misuse risk: MJWarp nightly numbers (e.g., Franka 36.98M steps/s, humanoid 7.95M on RTX PRO 6000) are physics-only with an unstated world count. Isaac Lab numbers (G1 82k, Shadow 170k FPS on RTX 4090) include inference and training. Genesis' 43M FPS is a launch-README marketing figure.
  The 252x/475x MJWarp-vs-MJX ratios are unverified vendor claims. None of these should feed a weighted decision matrix without in-house benchmarks on target scenes.
- Maturity risk: Isaac Lab 3.0 is Early Access (GA targeted end of Oct 2026), Isaac Sim 7.0 is alpha, MJWarp is 'Alpha' on PyPI, all Omniverse libraries (ovrtx, ovphysx, ovstage, ovstorage) are alpha or pre-release, Newton's Kamino solver is experimental, and the Genesis Nyx renderer is closed-
  source binary-only with no declared PyPI license. Isaac Sim streaming has no authentication or encryption. Isaac Sim ROS workspaces support only Humble and Jazzy, not the new Lyrical LTS. Pegasus (drones) is still on Isaac Sim 5.1.
- Cross-researcher inconsistencies to correct in the final plan: Newton 1.0.0 is 2026-03-10, not Apr 13 (that was 1.1.0); 'newton-physics' on PyPI is an inactive name. ovphysx is not BSD-3. The PhysX SDK core is now Apache-2.0. Cosmos 3 sizes are 64B/16B/4B, not 32B/8B, and Cosmos 2.5 repos are in
  limited maintenance. KHR_gaussian_splatting is ratified, not an RC. The mjlab latest is 1.6.0. OpenUSD's UsdPhysics nesting and Hydra 2 default arrived in 25.11. Chrono's AMD/ROCm support is dev-branch only. Waabi funding figures conflict.

## FACT-CHECK: corrected/refuted claims
- [corrected] (license/ovphysx) (platform_arch) ovphysx is BSD-3-Clause. (robot_physics) ovphysx is 'LicenseRef-NVIDIA-Omniverse', not BSD. => ovphysx source is Apache-2.0. The pip binaries (and the ovstage dependency) are proprietary NVIDIA Omniverse-licensed. 'Kit-less' does not mean 'license-
  free'. | https://github.com/NVIDIA-Omniverse/PhysX/tree/main/ovphysx ; https://pypi.org/project/ovphysx/ ; https://pypi.org/pypi/ovstage/json
- [corrected] (license/PhysX SDK) The PhysX SDK, including full GPU source, has been BSD-3 since PhysX 5.6 (April 2025); the latest SDK is 5.11.0. => The PhysX SDK 5.11 core is Apache-2.0 (permissive, with patent grant and NOTICE duties) and GPU source is in the repo. The repo root is still BSD-3. |
  https://raw.githubusercontent.com/NVIDIA-Omniverse/PhysX/main/physx/README.md ; https://raw.githubusercontent.com/NVIDIA-Omniverse/PhysX/main/LICENSE.md ; https://github.com/NVIDIA-Omniverse/PhysX/tree/main/physx/source
- [corrected] (hardware/Newton+Warp driver floor) Newton requires an NVIDIA GPU, Maxwell or newer, driver 545+. => With current Warp wheels, plan for Turing or newer GPUs and R580+ drivers (CUDA 13). Check that cloud and Korean-CSP GPU images ship R580+ drivers. | https://github.com/newton-
  physics/newton ; https://pypi.org/project/warp-lang/
- [corrected] (engine status/Isaac Sim releases) Isaac Sim 6.0 GA on 2026-06-08; 6.1.0 on 2026-09-10; 7.0.0a1 on 2026-09-18. => The 6.0.0 GA tag is 2026-06-04 (the forum announcement may say Jun 8). 7.0 is alpha only. | https://github.com/isaac-sim/IsaacSim/releases ;
  https://pypi.org/project/isaacsim/#history
- [corrected] (license/Genesis Nyx renderer) Nyx ships as a separate gs-nyx package; verify its license before embedding. => Nyx is effectively a closed-source binary with an ambiguous license. Do not treat Genesis's photoreal rendering path as open source. | https://pypi.org/project/gs-nyx/ ;
  https://github.com/Genesis-Embodied-AI/genesis-nyx
- [corrected] (license/cuRobo) (training) SkillGen depends on cuRobo, which has proprietary terms. (build_vs_buy) cuRobo's LICENSE is now Apache-2.0. => Pin a cuRobo release that is Apache-2.0 at that tag, and ask NVIDIA which terms govern the version Isaac Lab installs. |
  https://github.com/NVlabs/curobo/blob/main/LICENSE ; https://raw.githubusercontent.com/isaac-sim/IsaacLab/main/docs/licenses/dependencies/cuRobo-license.txt
- [corrected] (engine status/Chrono and Drake) Chrono 10.0.0 (spring 2026) is BSD-3 with refactored FSI, peridynamics and checkpointing; (build_vs_buy) Chrono 10.0.0 has an AMD ROCm GPU path. Drake v1.57.0 released 2026-09-10. => Chrono's AMD/ROCm and Vulkan/Metal sensor backends are dev-branch only
  and not in a release. | https://raw.githubusercontent.com/projectchrono/chrono/main/CHANGELOG.md ; https://pypi.org/project/drake/
- [corrected] (engine status/mjlab) (robot_physics) mjlab is in the 1.5.x series and pinned to MuJoCo Warp 3.11. (training) mjlab 1.6.0 was released 2026-08-09. => Latest mjlab is 1.6.0 (2026-08-09). It lags upstream MJWarp (pinned to 3.11). | https://pypi.org/pypi/mjlab/json ;
  https://raw.githubusercontent.com/mujocolab/mjlab/main/README.md
- [corrected] (standards/OpenUSD and glTF) OpenUSD 26.03 (2026-02-24) added wasm and UsdVolParticleField (3DGS). UsdPhysics gained nested rigid bodies and kinematic articulations. 26.05 made Hydra 2 the default. (realism) KHR_gaussian_splatting is a Release Candidate. (platform_arch)
  KHR_gaussian_splatting is ratified. => UsdPhysics nesting and the Hydra 2 default arrived in 25.11. KHR_gaussian_splatting is now ratified. No normative physics standard exists yet. | https://raw.githubusercontent.com/PixarAnimationStudios/OpenUSD/release/CHANGELOG.md ;
  https://raw.githubusercontent.com/KhronosGroup/glTF/main/extensions/README.md ; https://github.com/aousd/specifications-public
- [corrected] (platform/Omniverse libraries timing and streaming security) Omniverse libraries (ovrtx, ovphysx, ovstage) were announced at SIGGRAPH 2026 (robot_physics) or at GTC 2026 (platform_arch), in early access. Isaac Sim streaming has no auth or encryption. => ovrtx, ovphysx, ovstage and
  ovstorage are all alpha or pre-release as of Oct 2026, so none is production-stable. A multi-tenant streaming SaaS must add its own authentication and TLS layer. | https://pypi.org/pypi/ovrtx/json ; https://pypi.org/pypi/ovphysx/json ; https://pypi.org/pypi/ovstage/json ; https://github.com/isaac-
  sim/IsaacSim/blob/develop/tools/docker/README.md

## FACT-CHECK: confirmed
- (license/Isaac Lab pip wheel) Isaac Lab is BSD-3 (isaaclab_mimic Apache-2.0); the PyPI isaacsim/isaaclab wheels are labeled 'NVIDIA Proprietary Software'. | https://pypi.org/pypi/isaaclab/json ; https://github.com/isaac-sim/IsaacLab
- (license/ovrtx) ovrtx is proprietary (NVIDIA SLA + Product-Specific Terms for NVIDIA AI Products), alpha. | https://pypi.org/project/ovrtx/ ; https://github.com/NVIDIA-Omniverse/ovrtx
- (engine status/Newton) Newton 1.0.0 released 2026-03-10; latest v1.6.1 on 2026-10-05; Apache-2.0; Linux Foundation; started by Disney Research, Google DeepMind and NVIDIA. (market_competition: v1.0.0 Apr 13, 2026. training: PyPI newton-physics 1.0.0 on 2026-02-27.) |
  https://pypi.org/project/newton/ ; https://github.com/newton-physics/newton ; https://pypi.org/pypi/newton-physics/json
- (engine capability/Newton solvers) Newton solvers are Featherstone, MuJoCo, SemiImplicit, XPBD, Kamino, VBD, Style3D and ImplicitMPM. Only Featherstone and SemiImplicit are differentiable (basic). Only Featherstone and MuJoCo support generalized-coordinate articulations. |
  https://raw.githubusercontent.com/newton-physics/newton/main/docs/solvers/index.rst
- (engine capability/Newton determinism) Newton v1.4.0 added deterministic execution paths for bit-exact repeated rollouts, plus coupled solvers. | https://github.com/newton-physics/newton/releases/tag/v1.4.0 ; https://github.com/newton-physics/newton/releases.atom
- (engine capability/MJWarp limits) MJWarp is not differentiable, is non-deterministic on GPU, uses float32, and struggles with single connected mechanisms above about 60 DoF; MJX exposes it as impl='warp'. | https://raw.githubusercontent.com/google-deepmind/mujoco/main/doc/mjwarp/index.rst ;
  https://pypi.org/project/mujoco-warp/
- (engine status/MuJoCo) MuJoCo Warp was officially released with MuJoCo 3.5.0 (2026-02-12), which added a system-identification toolbox. 3.14 added IPC flex contact; 3.15 (2026-10-05) added Stable Neo-Hookean flex. | https://raw.githubusercontent.com/google-deepmind/mujoco/main/doc/changelog.rst ;
  https://github.com/google-deepmind/mujoco/releases.atom ; https://pypi.org/pypi/mujoco/json
- (benchmark/MJWarp nightly) MJWarp on RTX PRO 6000 Blackwell: humanoid 7.95M, Franka 36.97M, G1 flat/heightfield 3.79M/2.49M, ALOHA pot 3.37M, ALOHA clutter 0.46M steps/s. | https://github.com/google-deepmind/mujoco_warp/pull/1748
- (benchmark/Isaac Lab) On an RTX 4090: G1 rough 94k/88k/82k FPS (4,096 envs, 6.1 GB); Shadow repose 200k/170k (8,192 envs); Cartpole 1.1M; Cartpole RGB 50k (16.7 GB). On 4 nodes × 4 L40: G1 960k, Shadow 1.8M train FPS. | https://raw.githubusercontent.com/isaac-
  sim/IsaacLab/main/docs/source/overview/reinforcement-learning/performance_benchmarks.rst
- (engine status/Isaac Lab 3.0) Isaac Lab v3.0.0-EA was released 2026-09-16 for Isaac Sim 6.1, PyTorch 2.11, Warp 1.16 and Newton 1.5.2; GA targeted end of Oct 2026. (robot_physics, citing beta2 docs: Newton backend is 'beta' with a focused set of environments.) | https://github.com/isaac-
  sim/IsaacLab/releases.atom ; https://github.com/isaac-sim/IsaacLab/releases/tag/v3.0.0-EA
- (hardware/Isaac Sim GPUs and RT cores) Isaac Sim datacenter GPUs: A40 minimum, L40S recommended, RTX PRO 6000 Blackwell Server best. H100/A100/B200 lack RT cores and cannot be used for RTX rendering. | https://github.com/isaac-sim/IsaacSim ; https://github.com/NVIDIA-Omniverse/kit-app-template ;
  https://github.com/NVIDIA-Omniverse/ovrtx
- (GPU prices/AWS) AWS us-east-1: g6e.xlarge (L40S) $1.861/h, g7e.2xlarge (RTX PRO 6000) $3.363/h, p5.48xlarge (8×H100) $55.04/h, p5en.48xlarge (8×H200) $63.30/h, p6-b200 $113.93/h. Seoul is 23-38% higher. | https://raw.githubusercontent.com/skypilot-org/skypilot-
  catalog/master/catalogs/v8/aws/vms.csv
- (GPU prices/neoclouds) RunPod on-demand: L40S $1.09, RTX PRO 6000 $2.09, H100 PCIe $2.89 / SXM $3.49, B200 $6.79, RTX 4090 $0.74, L4 $0.49. GCP G4 (RTX PRO 6000) $4.50/h. | https://raw.githubusercontent.com/skypilot-org/skypilot-catalog/master/catalogs/v8/runpod/vms.csv ;
  https://raw.githubusercontent.com/skypilot-org/skypilot-catalog/master/catalogs/v8/gcp/vms.csv
- (engine status/Genesis) Genesis World 1.4.3 (2026-09-30) is Apache-2.0. The original '43M FPS Franka on RTX 4090' claim was criticized as misleading. | https://pypi.org/project/genesis-world/ ; https://raw.githubusercontent.com/Genesis-Embodied-AI/Genesis/v0.2.1/README.md ;
  https://raw.githubusercontent.com/Genesis-Embodied-AI/Genesis/main/README.md
- (license/MimicGen) MimicGen and DexMimicGen code is under the NVIDIA Source Code License; datasets are CC-BY-4.0. | https://raw.githubusercontent.com/NVlabs/mimicgen/main/LICENSE ; https://github.com/NVlabs/mimicgen
- (license/Hunyuan3D 2.1) The Tencent Hunyuan 3D 2.1 Community License excludes the EU, UK and South Korea, and forbids using the Works or their outputs outside the Territory. | https://raw.githubusercontent.com/Tencent-Hunyuan/Hunyuan3D-2.1/main/LICENSE
- (license/3D generation chain) TRELLIS.2-4B is MIT but depends on nvdiffrast (Nvidia Source Code License, 1-Way Commercial, non-commercial except NVIDIA); TRELLIS.2 generates 512³/1024³/1536³ in about 3/17/60 s on H100 with ≥24 GB VRAM. | https://github.com/microsoft/TRELLIS.2 ;
  https://raw.githubusercontent.com/NVlabs/nvdiffrast/main/LICENSE.txt
- (license/Gaussian splatting stack) Inria 3DGS (and derivatives such as 2DGS and MILo) is research/evaluation only; Instant-NGP is non-commercial; 3DGRUT and gsplat are Apache-2.0; PhysX-Anything uses the S-Lab License. | https://raw.githubusercontent.com/graphdeco-inria/gaussian-
  splatting/main/LICENSE.md ; https://raw.githubusercontent.com/nv-tlabs/3dgrut/main/LICENSE ; https://raw.githubusercontent.com/nerfstudio-project/gsplat/main/LICENSE ; https://raw.githubusercontent.com/ziangcao0312/PhysX-Anything/main/README.md
- (license/Cosmos 3) Cosmos 3 (Super 64B, Nano 16B, Edge 4B) is under OpenMDW-1.1 for code and weights; press reports said 32B/8B; Cosmos-Predict2.5 and Transfer2.5 are in limited maintenance. | https://github.com/NVIDIA/Cosmos ; https://raw.githubusercontent.com/nvidia-cosmos/cosmos-
  predict2.5/main/README.md ; https://raw.githubusercontent.com/nvidia-cosmos/cosmos-transfer2.5/main/README.md
- (license/Alpamayo and AlpaSim) AlpaSim is Apache-2.0. Alpamayo weights are OpenMDW-1.1 with commercial use permitted. Alpamayo 1.5 came in Mar 2026 and Alpamayo 2 Super (32B) on 1 Jun 2026. | https://github.com/NVlabs/alpasim ; https://github.com/NVlabs/alpamayo
- (license/GR00T N1.7) GR00T N1.7 is GA: 3B parameters, Cosmos-Reason2-2B backbone, 20K h EgoScale human video, fine-tune on ≥40 GB GPUs, inference on ≥16 GB; code Apache-2.0, weights NVIDIA Open Model License. | https://github.com/NVIDIA/Isaac-GR00T
- (license/datasets and model weights for marketplace) ManiSkill assets are CC BY-NC 4.0; AgiBot World and GO-1 are CC BY-NC-SA; Waymax is non-commercial; RLDX-1 weights are non-commercial; openpi weight license is unstated; VGGT-1B is non-commercial (only the -Commercial checkpoint allows
  commercial use); DA3 Large/Giant are CC BY-NC. | https://github.com/haosulab/ManiSkill ; https://raw.githubusercontent.com/OpenDriveLab/AgiBot-World/main/README.md ; https://raw.githubusercontent.com/waymo-research/waymax/main/README.md ;
  https://raw.githubusercontent.com/RLWRLD/RLDX-1/main/README.md ; https://raw.githubusercontent.com/facebookresearch/vggt/main/README.md ; https://raw.githubusercontent.com/ByteDance-Seed/Depth-Anything-3/main/README.md
- (license/SAM 3D Objects) SAM 3D Objects is under the SAM License: royalty-free and worldwide, with commercial use allowed subject to restrictions (e.g., military). | https://raw.githubusercontent.com/facebookresearch/sam-3d-objects/main/LICENSE
- (license/copyleft and source-available infrastructure) lakeFS v1.87.0 moved from Apache-2.0 to BSL 1.1. Ultralytics is AGPL-3.0. RF-DETR N–L are Apache-2.0 (XL/2XL under PML 1.0). BlenderProc and Stonefish are GPL-3.0. | https://github.com/treeverse/lakeFS/releases.atom ;
  https://raw.githubusercontent.com/ultralytics/ultralytics/main/README.md ; https://github.com/roboflow/rf-detr ; https://raw.githubusercontent.com/DLR-RM/BlenderProc/main/LICENSE ; https://github.com/patrykcieslak/stonefish
- (engine status/CARLA) CARLA's latest tag is 0.10.0 (UE 5.5, Dec 2024), with no 0.10.x follow-up. The UE5 build needs an RTX 3070-class GPU with 16 GB+ VRAM and 32 GB+ RAM. Code is MIT, assets CC-BY. | https://github.com/carla-simulator/carla/releases.atom ; https://raw.githubusercontent.com/carla-
  simulator/carla/ue5-dev/README.md
- (engine status/legacy engines) RaiSim v1 was archived 2026-04-25 and needs a license key. PyBullet's last release is 3.2.7 (2025-01-30). Brax physics is deprecated, with only brax/training maintained since 0.13.0. | https://github.com/raisimTech/raisimLib ;
  https://pypi.org/project/pybullet/#history ; https://github.com/google/brax
- (interop/ROS 2 and Isaac Sim) ROS 2 Lyrical Luth was released 2026-05-22 as an LTS with EOL May 2031. The Isaac Sim ROS workspaces repo provides only Humble and Jazzy. ros_gz pairs Lyrical with Jetty. | https://raw.githubusercontent.com/ros2/ros2_documentation/rolling/source/Releases.rst ;
  https://github.com/NVIDIA-Omniverse/IsaacSim-ros_workspaces ; https://github.com/gazebosim/ros_gz
- (infra/K8s GPU scheduling) In the NVIDIA DRA driver, ComputeDomains are supported but GPU allocation is not yet officially supported and is disabled by default; it needs K8s 1.32+. KAI Scheduler is Apache-2.0. OSMO is Apache-2.0. | https://raw.githubusercontent.com/NVIDIA/k8s-dra-driver-
  gpu/main/README.md ; https://raw.githubusercontent.com/NVIDIA/KAI-Scheduler/main/README.md ; https://raw.githubusercontent.com/NVIDIA/OSMO/main/README.md
- (vertical/drones) Pegasus Simulator v5.1.0 (26 Oct 2025) targets Isaac Sim 5.1 and PX4 1.14.3 (ArduPilot experimental). Project AirSim is MIT. | https://raw.githubusercontent.com/PegasusSimulator/PegasusSimulator/main/README.md ;
  https://raw.githubusercontent.com/iamaisim/ProjectAirSim/main/README.md

## FACT-CHECK: unverifiable
- (license/Isaac Sim SaaS) Isaac Sim source is Apache-2.0, but delivering Isaac Sim (with Kit) as a service to third parties, or redistributing it, requires NVIDIA AI Enterprise. Selling only outputs (datasets, videos) does not.
- (benchmark/MJWarp vs MJX speedups) MuJoCo Warp is up to 252x (locomotion) and 475x (manipulation) faster than MJX on RTX PRO 6000 Blackwell; the Newton beta figures were 152x and 313x on an RTX 4090.
- (hardware/MIG on RTX PRO 6000) RTX PRO 6000 Blackwell supports MIG (up to 4 instances), L40S has no MIG, so an RTX session costs about $0.84/h at a 4-way split.
- (license price/NVAIE and Omniverse Enterprise) NVIDIA AI Enterprise / Omniverse Enterprise is about $4,500 per GPU per year; $1,125 for Inception startups (75% off); about EUR 5,800 via an EU reseller.
- (license price/Unreal Engine) Unreal Engine charges non-game companies with more than $1M annual revenue $1,850 per seat per year (since UE 5.4, April 2024).
- (Korea policy/GPU and budget) NVIDIA committed 260k+ Blackwell GPUs to Korea on 31 Oct 2025 (government ~50k, Samsung/SK/HMG ~50k each, Naver ~60k), with an HMG physical-AI cluster of ~$3B. MSIT selected NHN (~7,656 B200), Naver (~3,056 H200) and Kakao (~2,424 B200). The 2026 budget is KRW 727.9T
  with AI at ~10.1T. The AI Basic Act took effect 22 Jan 2026.
- (Korea policy/startup programs) Deep-tech TIPS gives up to KRW 1.5B over 3 years (operator investment ≥ KRW 0.3B). Super-Gap 1000+ gives up to KRW 0.6B. The K-Humanoid Alliance launched 10 Apr 2025. The SME government R&D share is up to 75%.
- (market/funding and valuations) Applied Intuition $600M at $15B (Jun 2025); Figure $39B (Sep 2025); Physical Intelligence $600M at $5.6B (Nov 2025); Skild ~$14B (Jan 2026); Genesis AI $105M seed; Waabi $750M Series C (2026); Decart $300M at ~$4B (May 2026).
- (research benchmarks/fidelity) GPUSimBench (arXiv 2607.13059) found GPU-batched non-determinism, with ManiSkill EMD 2.520 cm and MJX 3.970 cm best. GAUGE (arXiv 2608.05948) found no uniformly faithful engine. Instant NuRec reconstructs a clip in ~1.5 s. SDQM r=0.8719.

## FACT-CHECK: missing coverage
- Primary text of the NVIDIA Isaac Sim license FAQ, the 'Isaac Sim Additional Software and Materials License', the NVIDIA AI Enterprise / Omniverse Product-Specific Terms and OpenMDW-1.1 (all blocked). The exact SaaS, on-prem and output clauses are the single most decision-critical unknown.
- Epic Unreal Engine EULA terms for server-side Pixel Streaming offered to third parties as SaaS, and current 2026 seat pricing. Unity 2026 HDRP/URP status and Unity Industry runtime licensing.
- Korean cloud GPU availability and pricing for RT-core GPUs (L40S, RTX PRO 6000) at NHN Cloud, KT Cloud, Naver Cloud, Kakao Cloud and Samsung SDS, plus whether the government GPU programs include any RT-core capacity. CSAP certification requirements for selling the SaaS to public agencies.
- Data-residency and privacy compliance for a Korea-hosted multi-tenant SaaS (PIPA cross-border transfer, AI Basic Act obligations for generative-AI labeling). Export-control screening (US EAR on advanced GPUs and model weights; ITAR clauses in the SAM License) for defense and overseas customers.
- Independent sim-to-real fidelity evidence: the cited 2026 benchmark papers (GPUSimBench, GAUGE) and the realism metrics (SDQM, SADGE) could not be accessed. No verified head-to-head contact-rich or deformable fidelity comparison among PhysX, Newton/MJWarp, Genesis and Drake exists in the digest.
- Licensing and maturity of NuRec / 3DGUT containers on NGC, Sensor RTX APIs and the Omniverse Blueprint for AV simulation (early access only, terms unknown). Also the status of the claimed 'Instant NuRec' and 'OmniDreams' releases.
- Non-NVIDIA GPU portability: AMD ROCm paths exist only in Genesis Quadrants and in Chrono's unreleased dev branch. The supply-risk and lock-in analysis for an all-NVIDIA stack (Warp, Newton and MJWarp require NVIDIA GPUs for speed) is missing.
- Reproducibility across hardware for dataset products: Newton v1.4 claims 'deterministic and portable execution' while PhysX only guarantees same-hardware determinism and nothing for deformables. This should be tested, since CEN sells 'reproducible' synthetic data.
- Customer-validated demand and pricing evidence for Korean anchor customers (HMG, Samsung, HD Hyundai, Doosan, MORAI's position). Most of the market sizing and competitor funding in the digest is prior-knowledge-only and low confidence.
- Isaac Sim 6.x support for ROS 2 Lyrical (2031 LTS), and a porting plan for drone (Pegasus) and marine (OceanSim/MarineGym) verticals onto Isaac Sim 6.x / Isaac Lab 3.0.


# TOPIC: robot_physics
## Executive summary
Recommendation: do not write a new physics engine. The field has converged on a small set of permissively licensed GPU engines. Build a backend-agnostic simulation layer on top of them instead. Newton (Apache-2.0, Linux Foundation project, initiated by NVIDIA, Google DeepMind and Disney Research)
  reached 1.0 GA on 2026-03-10 at GTC 2026 and has shipped monthly since; the current release is v1.6.1 (2026-10-05). It bundles several solvers behind one Warp/OpenUSD API: MuJoCo Warp (MJWarp) for articulated rigid bodies, Kamino (Disney, a nonlinear-complementarity solver for closed kinematic
  loops), Featherstone, SemiImplicit, XPBD, VBD (cloth, cables, soft bodies), Style3D (cloth), and implicit MPM (granular and fluid), plus SDF collision and Drake-style hydroelastic contact. That covers robots, deformables and granular media in one embeddable package. MJWarp is the throughput
  leader. Nightly benchmarks on an RTX PRO 6000 Blackwell (2026-10-05) show about 7.9M humanoid steps/s, 37M Franka steps/s, 3.8M Unitree G1 flat-terrain steps/s and 0.46M steps/s for a cluttered ALOHA scene. NVIDIA reports MJWarp up to 252x (locomotion) and 475x (manipulation) faster than MJX.
  MJWarp has real limits: float32, non-deterministic on GPU (atomics), not differentiable, weak on single mechanisms above about 60 DoF, and its PyPI classifier still says Alpha. MuJoCo 3.15.0 (CPU, float64, deterministic, 2026-10-05) loads the same MJCF and is the natural reference and low-latency
  backend. Its 2026 releases added an MJWarp official release (3.5), a system-identification toolbox, DC-motor/PID/MIMO actuators, experimental IPC contact and Neo-Hookean flex. NVIDIA's own stack has split into modules. Isaac Sim 6.0 went GA on 2026-06-08 and 6.1 followed in September 2026 with
  experimental Newton 1.5, VBD, XPBD and hydroelastic contact. Isaac Lab 3.0.0-EA (BSD-3, 2026-09-16) offers one task API over PhysX, Newton/MJWarp and OVPhysX, and the Newton path can run without Kit or Isaac Sim. The PhysX 5 SDK is fully open source including its GPU kernels (BSD-3, since 5.6 in
  April 2025; now 5.11). The licensing trap is Isaac Sim with Omniverse Kit: the Isaac Sim source is Apache-2.0, but delivering it as a service to third parties requires an NVIDIA AI Enterprise license (list price about $4.5k per GPU per year). The new ovphysx library is under an NVIDIA Omniverse
  license. So a multi-tenant SaaS should embed Newton, MuJoCo or the PhysX SDK directly and offer Kit-based Isaac Sim only as a separately licensed or bring-your-own-license option. Selling only outputs, such as datasets, needs no AI Enterprise license. Genesis World 1.x (Apache-2.0, v1.4.3 on
  2026-09-30, 30k+ stars) is the broadest multi-physics alternative and the only serious one not tied to NVIDIA GPUs: its Quadrants compiler targets CUDA, ROCm, Metal and Vulkan, and it adds IPC, a Drake-derived SAP coupler and tactile sensors. However, its 43M FPS headline was shown to be
  misleading (about 150x off on realistic settings), and independent 2026 benchmarks (GPUSimBench, GAUGE) find no engine uniformly faithful to reality and real GPU non-determinism. Drake (BSD-3, v1.57.0 on 2026-09-10) still has the most rigorous hydroelastic/SAP contact but is CPU-only, so it suits
  offline validation, not RL scale. Project Chrono 10.0 (BSD-3) is the best open option for vehicles, terramechanics (SPH/CRM) and fluid-structure interaction. Several options are dead ends as a primary backend: PyBullet (last release 3.2.7, Jan 2025), Brax physics (deprecated; only brax/training is
  maintained), Dojo (inactive since 2023), RaiSim (v1 repo archived Apr 2026; RaiSim2 is proprietary) and Jolt (a game engine without reduced-coordinate articulations). Recommended primary robot backend: Newton with the MJWarp solver by default, Kamino for closed-loop mechanisms, VBD/MPM for
  deformables, and hydroelastic/SDF for contact-rich assembly. Pair it with MuJoCo CPU as the bit-reproducible reference and interactive backend, and expose PhysX through Isaac Lab 3.x as a compatibility backend. Use Isaac Lab 3.x running without Kit, or mjlab, as the training front end.
## Recommendations
- Build vs adopt: do NOT build a physics engine. Newton is co-built by NVIDIA, DeepMind and Disney with dozens of specialist engineers; a startup cannot match its contact solvers, GPU kernels and validation. Instead, build and own a backend-agnostic 'Physics Abstraction Layer'. Use OpenUSD as the
  canonical scene format with MJCF/URDF importers. Give it one task/env API following the Isaac Lab manager-based design (which mjlab also follows), shared sensor and actuator interfaces, and per-backend adapters. RoboVerse/MetaSim and Isaac Lab 3.0's multi-backend design prove the pattern.
- Primary robot backend: Newton (pin a minor version such as 1.6.x and upgrade quarterly). Use the MJWarp solver by default for locomotion, humanoid whole-body control and dexterous hands; Kamino for closed-loop linkages; VBD/Style3D for cloth and cables; ImplicitMPM for granular and food; SDF plus
  hydroelastic contact for assembly and insertion. It is Apache-2.0, so it can be embedded in a multi-tenant SaaS without royalties.
- Reference and interactive backend: MuJoCo 3.15+ on CPU (float64, deterministic) on the same MJCF. Use it for (a) the low-latency interactive editor, teleoperation and MPC in the CEN browser workspace, (b) a 'reproducible mode' for dataset provenance, and (c) nightly cross-checks that MJWarp
  rollouts stay within tolerance of MuJoCo.
- Compatibility backend: PhysX through Isaac Lab 3.x (PhysX SDK is BSD-3). Offer Kit-based Isaac Sim/RTX only as (i) an internal synthetic-data factory whose outputs CEN sells (license-exempt), or (ii) a customer bring-your-own NVIDIA AI Enterprise / partner-licensed premium workspace. Never ship
  Omniverse Kit or ovphysx to tenants without a written NVIDIA agreement.
- Training front end: Isaac Lab 3.x running without Kit on the Newton backend, plus mjlab for a lightweight path. Integrate RSL-RL, skrl, rl_games and Brax-training for RL; LeRobot and Isaac Lab Mimic for imitation learning and VLA data generation. Make env count, decimation and domain-randomization
  presets one-click in the UI, and expose the LLM text-command interface as a layer that edits USD scenes and launches training jobs.
- Vehicles, off-road and marine: add Project Chrono 10 (BSD-3) as a separate backend for vehicle dynamics, tires, CRM/SPH terramechanics and fluid-structure interaction, and PhysX Vehicle2 for light-duty driving. Do not force cars into the robot RL engine.
- Contact-fidelity program, as a differentiator for CEN's 'controllable, reproducible' positioning: build an internal real-measurement benchmark in the style of GAUGE and GPUSimBench (inclined plane, turntable, drop and bounce, cable sag, cloth drape, peg insertion). Calibrate marketplace assets
  with MuJoCo's sysid toolbox, using Drake hydroelastic as an offline gold standard for contact-rich parts, the way Lightwheel calibrates SimReady assets. Publish a per-asset 'fidelity score'.
- Tactile: expose one tactile sensor API backed by Isaac Lab TacSL (PhysX path), MuJoCo touch_grid (MuJoCo/MJWarp), and custom Warp kernels on Newton hydroelastic pressure fields. Evaluate Taccel or Genesis IPC tactile for high-fidelity dexterous hands.
- Determinism and reproducibility: document that GPU batched runs are statistically, not bitwise, reproducible (MJWarp atomics, PhysX across GPUs). Store seeds, engine and driver versions, GPU SKU and env count in every dataset's metadata. Provide a CPU-MuJoCo replay for audit.
- Hedge against NVIDIA lock-in: keep Genesis World (Apache-2.0; Quadrants runs on CUDA, ROCm, Metal and Vulkan) as an experimental adapter. Also use it for fluid/SPH and IPC demos. Do not use its speed claims in marketing without your own benchmarks.
- Run a 6-8 week bake-off before final commitment, on identical hardware (1x RTX PRO 6000 Blackwell plus 1x H100/H200). Tasks: G1 velocity tracking, a BeyondMimic motion clip, Franka cube lift, LEAP/Allegro in-hand reorientation, cable insertion, cloth folding and a Kamino closed-loop gripper.
  Measure env-steps/s, wall-clock to reward threshold, VRAM, steps per dollar, cross-backend policy transfer (Newton to PhysX to MuJoCo), and a real-robot transfer on at least one quadruped or humanoid and one arm.
- GPU fleet: RTX PRO 6000 Blackwell / L40S-class (RT cores) for combined physics, rendering and synthetic-data nodes, and H100/H200/B200-class for physics-only RL and VLA training. H100-class GPUs lack RT cores (based on general product knowledge, not checked against NVIDIA's spec pages here), so
  they are not suited to RTX sensor rendering. Use MIG or MPS to pack small tenant jobs and CUDA-graph capture (supported by Newton/MJWarp) to cut launch overhead.
- Team for the physics layer: about 5-7 engineers in year 1. Roles: 1 lead with contact mechanics and multibody background; 2 Warp/CUDA kernel engineers (custom sensors, actuators, Newton contributions); 1 USD/MJCF/URDF asset-pipeline engineer; 1 sysid and sim2real engineer with lab access to a
  quadruped or humanoid and a 7-DoF arm; 1 RL infrastructure engineer; plus 0.5 FTE for licensing and partner relations with NVIDIA Inception and the Linux Foundation Newton community. Contribute upstream to Newton (vehicle hooks, tactile, Korean industrial assets) to gain roadmap influence.
- Avoid as primary backends: PyBullet (stagnant since Jan 2025), Brax physics (deprecated), Dojo (inactive), RaiSim (proprietary; v1 archived), Jolt (no reduced-coordinate articulations; at most a browser-preview engine), ManiSkill assets (CC BY-NC) in commercial bundles.
## Risks
- Newton immaturity: 1.0 only since March 2026, monthly API changes, MJWarp still labelled 'Alpha' on PyPI, and Isaac Lab's Newton integration is beta/early access with a limited validated task set. Expect upgrade churn and regressions; pin versions and keep MuJoCo CPU and PhysX fallbacks.
- NVIDIA dependency: Newton, MJWarp and Warp are CUDA-only on GPU, so pricing, supply and export controls on NVIDIA GPUs (relevant for Korea, and for cloud GPU quotas) directly hit COGS. Genesis/Quadrants is the main non-NVIDIA hedge but is less proven.
- Licensing trap: hosting Isaac Sim with Omniverse Kit for tenants requires NVIDIA AI Enterprise (about $4.5k per GPU per year). ovphysx and ovrtx carry the proprietary 'NVIDIA-Omniverse' license. ManiSkill assets are CC BY-NC. Genesis's Nyx renderer package license was not yet public. Misreading
  these could create legal exposure for a commercial multi-tenant SaaS.
- Fidelity is not solved: GAUGE (2026) found no uniformly faithful engine, with the worst gaps in impulsive contact, fast cloth and volumetric deformation. Marketing 'high real-world similarity' requires your own measurement-grounded calibration.
- Reproducibility: GPUSimBench shows GPU-batched non-determinism in mainstream simulators, and MJWarp is explicitly non-deterministic in float32. That can undermine CEN's 'reproducible synthetic data' promise unless a deterministic replay path exists.
- Benchmark hype: vendor speedups (252x/475x vs MJX, Genesis 43M FPS) are not comparable across tasks, substeps, decimation and env counts. Isaac Lab 'env-step FPS' includes decimation and RL overhead, while MJWarp numbers are raw physics steps. Capacity planning must come from in-house benchmarks.
- Fragmentation and churn: Isaac Sim 5.0, 6.0 and 6.1 plus Isaac Lab 2.3 and 3.0 within about 15 months, and Omniverse libraries still early access. Integrations built on Kit internals may break.
- Differentiable simulation remains weak in production engines (only Newton's Featherstone and SemiImplicit; MJWarp not differentiable). Gradient-based sysid and design features may need custom Warp work.
- Scale limits: MJWarp struggles with single mechanisms above about 60 DoF (e.g., full humanoid plus two dexterous hands as one tree may underperform). Tactile at full-hand resolution is still orders of magnitude slower than rigid-body RL.
- Ecosystem risk on alternatives: Genesis AI has pivoted to its own foundation model (GENE-26.5), which may deprioritize the open simulator; ManiSkill has a tiny maintainer team; RaiSim and PyBullet show how single-company engines stall.
## Open questions
- Does AICHEMIST's browser GPU workspace, if it ever runs Isaac Sim/Kit for tenants, fall under 'delivering as a service', and what NVIDIA AI Enterprise or Inception/partner terms (per-GPU or per-concurrent-user) would NVIDIA Korea offer? Ask for a written opinion.
- What are the exact license terms of ovphysx, ovrtx and ovstage at their production release (late 2026)? Will they permit embedding in third-party SaaS without AI Enterprise?
- Per-engine numeric results in GAUGE (arXiv 2608.05948) and throughput/memory tables in GPUSimBench (arXiv 2607.13059) could not be read directly (arxiv.org was blocked by the egress proxy); verify before citing to investors.
- What are the benchmark configurations (worlds per scene, timestep, solver iterations) behind the MJWarp nightly numbers, so they can be normalized against Isaac Lab env-step FPS?
- Roadmap and timeline for MJWarp differentiability (issue #500), Newton deterministic GPU mode, and production status of Newton in Isaac Lab (task coverage beyond flat-terrain locomotion).
- Does Newton plan native tactile sensors or vehicle/tire models, and could AICHEMIST contribute these upstream for roadmap influence under LF governance?
- How mature is Genesis's Quadrants on AMD ROCm for real RL workloads, and what is the license and availability of the Nyx renderer wheel?
- Real sim2real evidence for Newton beyond NVIDIA-partner announcements (G1 locomotion, Skild rack assembly, Samsung cables): are there independent peer-reviewed results by CoRL 2026 (Nov 2026)?
- Whether Chrono's vehicle and terramechanics stack can be co-simulated with Newton robots (e.g., a mobile manipulator on deformable terrain) through a shared USD stage, or needs a custom co-simulation bridge.
- Exact Isaac Lab 3.0 GA date and API-freeze commitments; the EA release dates shown on GitHub should be re-checked.


# TOPIC: vehicle_sim
## Executive summary
1) In 2026 the AV simulation market has split into two layers. One is engineering-grade, standards-based toolchains sold to OEMs and Tier-1s: IPG CarMaker 15.0 (Nov 2025), CarSim/TruckSim (owned by Applied Intuition since Mar 2022), dSPACE AURELION, Hexagon VTD/VTDx, aiSim 5/6, rFpro AV elevate and
  Ansys/Synopsys AVxcelerate 2026 R1. These sell on HIL/SIL integration, ASAM OpenX support, determinism and tool qualification (aiSim 5 holds an ISO 26262 ASIL-D certificate). The other is neural/generative simulation for training and evaluating end-to-end driving policies: NVIDIA NuRec (GA at GTC
  2026), Instant NuRec (~1.5 s feed-forward reconstruction of a 10–20 s multi-camera clip), Cosmos 3 (1 Jun 2026), OmniDreams, AlpaSim and AlpaGym, the Waymo World Model (built on Genie 3, Feb 2026), Wayve GAIA-3 (15B, Dec 2025), Tesla's neural world simulator and Waabi World.
2) NVIDIA has largely given away the neural AV stack. AlpaSim code is Apache-2.0. Alpamayo weights and Cosmos 3 (Nano 16B / Super 64B / Edge 4B) are under OpenMDW-1.1, which allows commercial use. Cosmos Predict/Transfer 2.5 code is Apache-2.0, and 3DGRUT (the Gaussian ray-tracing/unscented-
  transform renderer) is Apache-2.0. A startup should not try to build its own neural reconstruction or world model from scratch; it should integrate these and differentiate on data, workflow and vertical content.
3) NVIDIA DRIVE Sim never became generally available. It was effectively replaced by the Omniverse Blueprint for AV simulation, Sensor RTX APIs, NuRec and Cosmos, delivered through partners: Foretellix, CARLA, Applied Intuition, Mcity and 51Sim in China.
4) CARLA is still the default open AV simulator. Code is MIT and assets CC-BY. The latest tag is still 0.10.0 (UE 5.5, Chaos physics, Dec 2024). The 0.9.16 release (Sep 2025, UE4) added Cosmos Transfer1, NuRec, native ROS 2 and a SimReady/OpenUSD converter. The ue5-dev branch is active (last push
  2026-10-02), but the leaderboard and most research still target 0.9.x. The UE5 build needs 16 GB+ VRAM and 32 GB+ RAM. Governance is led by CVC Barcelona with a small team.
5) For vehicle dynamics the open-source choice is Project Chrono 10.0 (Mar/Apr 2026, BSD-3). It offers Pacejka 89/2002, TMeasy, Fiala and FEA/ANCF tires, SCM deformable terrain, and GPU SPH "CRM" terrain (29 km of terrain on one H100) for off-road. CarSim and CarMaker remain the commercial reference
  for real-time HIL with Magic Formula 6.x, MF-Swift or FTire tire models. BeamNG.tech v0.39 (summer 2026; 2 kHz soft-body physics, native C++ ROS 2, MCP) is a strong crash and soft-body niche tool, licensed by quote.
6) Regulation is starting to require simulation credibility, not just simulation:
   - The UN ADS regulation was adopted by GRVA in Jan 2026 and approved by WP.29 in late June 2026. It requires evidence that virtual-testing toolchains are credible.
   - ISO 34505:2025 (Jun 2025) standardises scenario evaluation and test-case generation.
   - ISO/PAS 8800:2024 covers AI safety. ISO 26262 Ed. 3 is expected in 2027. UL 4600 Ed. 3 was published 17 Mar 2023.
   - Euro NCAP's 2026 protocols expand crash-avoidance scenario variants and add simulation-supported assessment.
7) Korea:
   - Level-4 performance certification became law on 20 Mar 2025.
   - MOLIT opened the Hwaseong "AI Autonomous Driving Hub" on 20 Mar 2026.
   - KATRI's K-City (360,000 m²) has a virtual twin that agreed with the real route 92.5% of the time within 0.288 m.
   - The Autonomous Ship Act took effect on 3 Jan 2025.
   - MORAI (100+ customers, Series B) is the domestic incumbent for HD-map-to-digital-twin AV simulation.
8) Drones are well served by open source: Pegasus Simulator v5.1.0 (Isaac Sim 5.1, PX4, BSD-3), Project AirSim (MIT, maintained by IAMAI), Aerial Gym (BSD-3, massively parallel RL), Gazebo Jetty LTS (supported to May 2031) and PX4 1.16/1.17 SITL with ArduPilot. Flightmare is effectively dormant.
9) Marine is the most fragmented area. Stonefish is GPL-3.0. HoloOcean 2.0 (UE 5.3, Fossen dynamics) is a preview, and the pip package is still 0.5.8. DAVE and VRX run on Gazebo. OceanSim is Isaac Sim-based. No commercial leader serves autonomous ships, ports and shipyards, while HD Hyundai
  (Omniverse/Siemens/Palantir; Avikus on ~350 vessels) and Samsung Heavy (SAS; autonomous trans-Pacific crossing in 2025) are investing heavily.
10) Recommendation: integrate the engines and build the workflow.
   - **Integrate:** OpenUSD/Isaac Sim as the scene core, NuRec/3DGRUT and Cosmos as the neural layer, AlpaSim/AlpaGym and Isaac Lab for training, Chrono for off-road and terramechanics, PX4/ArduPilot SITL for drones, an esmini/CARLA path for OpenSCENARIO, and FMI/OSI adapters to customers' CarSim or
  CarMaker.
   - **Build:** LLM text-to-scenario generation, Korean digital-twin content and a marketplace, sensor calibration and credibility evidence packs, and synthetic-dataset export.
   - **Most winnable niches:** maritime/port/shipyard autonomy first, then dual-use off-road UGV and drone perception. Do not compete head-on in OEM ADAS HIL validation (dSPACE, IPG, Applied Intuition at an estimated ~$830M ARR) or in generic neural driving simulation, where NVIDIA gives the stack
  away.
11) Licensing constraints to check before committing:
   - Offering Omniverse Kit or Isaac Sim as a service to third parties requires NVIDIA AI Enterprise (list price $4,500/GPU/yr; 75% Inception discount).
   - Unreal Engine charges non-game companies with more than $1M revenue $1,850 per seat per year.
   - Waymax and the Waymo Open Dataset are non-commercial.
   - Ray-traced sensor rendering needs RTX-class GPUs (L40S or RTX PRO 6000), not H100/B200.
## Recommendations
- BUILD vs INTEGRATE. Do not build a physics engine, renderer, neural reconstructor or world model for vehicles, drones or ships. NVIDIA (NuRec GA, 3DGRUT Apache-2.0, Cosmos 3 under OpenMDW-1.1, AlpaSim Apache-2.0) and the open-source community (Chrono BSD-3, CARLA MIT, PX4/Gazebo) already give
  these away. Build the layers they lack: (a) LLM text-to-scenario generation targeting ASAM OpenSCENARIO DSL 2.1/XML 1.3 plus OpenDRIVE 1.8; (b) a Korean digital-twin content pipeline from HD map/OpenDRIVE and drone or vehicle logs to OpenUSD plus NuRec scenes; (c) sensor calibration, sim-to-real
  KPIs and credibility evidence packs; (d) dataset export and labeling (OpenLABEL, COCO, nuScenes/Waymo formats) and the marketplace; (e) managed training jobs in the GPU cloud workspace.
- REFERENCE ARCHITECTURE for the mobility vertical:
- Scene core: OpenUSD on Isaac Sim 6.x / Omniverse Kit, shared with the robot platform.
- Rendering: RTX sensors for camera, lidar and radar, with OSI 3.7 output.
- Neural layer: NuRec/Instant NuRec for log replay; Cosmos Transfer 2.5 / Cosmos 3 Nano for appearance augmentation; OmniDreams-style generative closed loop as an advanced option.
- Vehicle dynamics, three plug-in levels: PhysX vehicle (kinematic or dynamic bicycle, L1–L2); Chrono::Vehicle co-simulation with Pac02/TMeasy tires and SCM/CRM terrain for off-road (L3–L5); FMI 2.0/3.0 FMU adapter so customers can bring licensed CarSim, CarMaker or MF-Tyre/FTire models.
- Drones: Pegasus-style PX4/ArduPilot SITL in Isaac, plus Gazebo Jetty for flight-stack CI.
- Marine: clean-room Fossen 6-DOF plus wave-spectrum module and OceanSim-style RTX sonar. Avoid copying GPL Stonefish code.
- Training: AlpaSim/AlpaGym gRPC interface for driving policies, Isaac Lab and Aerial Gym for drone/UGV RL, Cosmos post-training recipes for perception.
- OPEN-STANDARD BACKBONE. Make ASAM OpenX first-class: OpenDRIVE import/export, OpenSCENARIO XML (via esmini or CARLA ScenarioRunner) and DSL, OSI sensor-data interfaces, OpenLABEL annotations and OpenMATERIAL 3D material properties for lidar and radar reflectance. This is what lets OEMs and Tier-1s
  plug AICHEMIST into dSPACE, IPG and Applied pipelines instead of replacing them.
- LICENSING DUE DILIGENCE before month 1:
- Join NVIDIA Inception and price NVIDIA AI Enterprise for every GPU that serves Kit or Isaac Sim to customers (~$1,125/GPU/yr discounted vs $4,500 list).
- Keep Unreal-based components (CARLA, Project AirSim, HoloOcean) out of the commercial runtime, or budget $1,850/seat/yr once revenue exceeds $1M.
- Exclude non-commercial assets (Waymax, Waymo Open Dataset) from paid products.
- Honour 'Built on NVIDIA Cosmos' attribution and guardrail clauses.
- Get legal review of GPL-3 (Stonefish, ArduPilot) for any on-prem distribution.
- GPU PLANNING. Ray-traced sensor simulation and NuRec rendering need RT-core GPUs (L40S, RTX PRO 6000 Blackwell). Cosmos 3 Super fine-tuning needs H200/B200, and Nano runs on RTX PRO 6000/H100. Design the cloud workspace with two pools: an RTX pool for simulation and rendering, and an HGX pool for
  training and world models.
- MOST WINNABLE NICHE #1 – MARITIME / PORT / SHIPYARD AUTONOMY.
- Why: the open-source marine sims are fragmented and research-grade (Stonefish GPL, HoloOcean 2.0 unreleased, DAVE/VRX low-fidelity), and there is no dominant commercial vendor.
- Demand: Korea's Autonomous Ship Act (in force 3 Jan 2025) requires performance verification, and HD Hyundai (Avikus on ~350 vessels), Samsung Heavy (SAS) and Hanwha Ocean are spending heavily.
- Offer: synthetic perception datasets (EO/IR camera, marine radar, AIS-consistent traffic, fog, sea-state, night), port and shipyard digital twins, and collision-avoidance (COLREG) scenario libraries. Start with a co-development PoC with Avikus or SHI's SAS team.
- MOST WINNABLE NICHE #2 – DUAL-USE OFF-ROAD UGV AND DRONE PERCEPTION.
- Build on Chrono SCM/CRM terrain, Pegasus/PX4 and Cosmos augmentation to sell synthetic data plus closed-loop RL for Korean defense (unmanned ground vehicles, counter-drone detection, ISR drones) and agriculture/construction.
- Duality Falcon (US Army counter-drone contract) and Cognata's defense pivot validate the market. MORAI is also moving into defense, so differentiate with neural reconstruction and synthetic-data quality metrics rather than a classical simulator.
- NICHE #3 (secondary) – KOREAN ROAD PERCEPTION DATA-AS-A-SERVICE.
- Use NuRec/Instant NuRec reconstructions of Korean roads (Hangul signage, two-wheelers, local vehicle fleet, Hwaseong hub and K-City) plus Cosmos weather/lighting variation to sell long-tail perception datasets and closed-loop evaluation to Korean OEMs/Tier-1s, robotaxi startups and Level-4
  performance-certification applicants.
- Partner with KATRI/K-City and the Hwaseong AI Autonomous Driving Hub for sim-to-real correlation studies; K-City already publishes a 92.5%-within-0.288 m benchmark.
- DO NOT COMPETE HEAD-ON in OEM ADAS SIL/HIL homologation tooling (dSPACE, IPG CarMaker 15, Applied/CarSim, aiSim ASIL-D, VTD) or in generic neural driving simulators (NVIDIA AlpaSim/OmniDreams are free). Position AICHEMIST as the synthetic-data and digital-twin content layer that feeds those tools
  via OSI, FMI and OpenSCENARIO.
- CREDIBILITY AS A PRODUCT. From day one, generate a credibility dossier per scenario and sensor model:
- validation data;
- sim-vs-real metrics, e.g. detection-mAP gap and lidar point-distribution distances;
- scenario coverage per ISO 34505;
- a traceable safety-case fragment in UL 4600 / UNECE ADS format.
The UN ADS regulation (WP.29, Jun 2026) now requires demonstrating toolchain credibility, so this is a monetizable differentiator rather than overhead.
- LLM COMMAND INTERFACE. Expose the simulator through an MCP server (Isaac Sim 6.0 and BeamNG v0.39 already ship MCP) so CEN's LLM layer can author scenes, place agents, set weather and sea-state, and launch training. Constrain outputs to validated OpenSCENARIO DSL so generated scenarios are
  reproducible and exportable.
- ROADMAP for this vertical.
- Months 0–3: license due diligence; CARLA 0.9.16 + Cosmos Transfer PoC for Korean roads; Pegasus drone PoC on Isaac Sim 5.1/6.0; marine PoC with OceanSim plus a Fossen model.
- Months 3–9: USD scene pipeline; NuRec ingestion of customer logs; OpenSCENARIO runtime; RTX sensor calibration; first paid synthetic-dataset contracts (marine plus defense).
- Months 9–18: closed-loop training (AlpaGym/Isaac Lab/Aerial Gym); Chrono off-road co-simulation; credibility dossiers; K-City / Hwaseong correlation study.
- Months 18–30: marketplace of Korean road, port and shipyard twins; HIL partner bridges (dSPACE/IPG via OSI/FMI); generative closed-loop module.
- TEAM for this vertical (by month 12, ~12–18 FTE):
- 2 vehicle-dynamics/multibody engineers (Chrono, FMI, tire models)
- 2 sensor-physics engineers (RTX camera ISP, lidar/radar, sonar)
- 3 neural rendering / world-model engineers (3DGS/3DGUT, Cosmos post-training)
- 2 scenario and standards engineers (OpenSCENARIO/OpenDRIVE/OSI)
- 2 autonomy-stack engineers (PX4/ArduPilot, ROS 2, maritime COLREG)
- 3 platform/cloud engineers (Kit streaming, Kubernetes GPU scheduling)
- 1 functional-safety/credibility engineer (ISO 26262/21448/34505, UL 4600)
- 1–2 technical artists for digital-twin content
## Risks
- NVIDIA platform dependency: licensing (NVAIE for SaaS), API churn (Isaac Sim 5.x to 6.0, Alpamayo repo already 'not under active development') and NVIDIA giving away competing features (AlpaSim, OmniDreams, NuRec) can erase differentiation overnight.
- Neural and generative simulation lacks physical guarantees. Off-trajectory artifacts in NuRec and hallucinations in Cosmos/OmniDreams can make data or evaluations unusable as safety evidence; regulators (UN ADS, ISO 34505) require demonstrated credibility.
- Incumbent lock-in: OEMs and Tier-1s are standardized on dSPACE/IPG/Applied/VTD HIL chains with ISO 26262 tool qualification (aiSim ASIL-D). A startup tool will not be accepted for homologation evidence without years of validation.
- Domestic competition: MORAI is the incumbent with government ties and is expanding into defense, UAM and ships; HD Hyundai and Samsung Heavy may build marine twins in-house with NVIDIA, Siemens and Palantir.
- Unreal Engine exposure: CARLA, Project AirSim and HoloOcean are UE-based. Seat fees ($1,850/seat/yr above $1M revenue) and EULA constraints apply if they are embedded commercially.
- License contamination: non-commercial assets (Waymax, Waymo Open Dataset), GPL-3 code (Stonefish, ArduPilot), NVIDIA dataset licenses limited to internal AV development, and Cosmos guardrail clauses.
- Open-source maintenance risk: CARLA's small team and UE4/UE5 split, single-maintainer projects (Pegasus, Stonefish), Flightmare dormant, Aerial Gym still on deprecated Isaac Gym, HoloOcean 2.0 unreleased.
- GPU cost and supply: RTX-class GPUs are needed for sensor ray tracing, and H200/B200 for Cosmos 3 Super. Cloud margins on a token/subscription model can be negative for closed-loop neural simulation.
- Market timing: Korean Level-4 commercialization and autonomous-ship certification procedures are still being detailed. Demand for simulation-based certification evidence may lag the roadmap.
- Vehicle-dynamics fidelity gap: without licensed MF 6.x/FTire tire data and validated CarSim-class models, AICHEMIST cannot credibly serve chassis-control or ADAS longitudinal/lateral validation customers.
- Funding signals in the sector are mixed: Foretellix layoffs in Jan 2026 vs a $750M Waabi round. Tool vendors without a data or vertical moat are being squeezed.
## Open questions
- Exact NuRec GA licensing: is NuRec included in NVIDIA AI Enterprise, separately priced, or free on NGC for commercial SaaS? (Primary NVIDIA pages were blocked from this environment.)
- The precise Isaac Sim 6.x / Omniverse Kit terms for multi-tenant cloud workspaces such as CEN: per-GPU NVAIE, Inception pricing in Korea, and whether streaming to end users counts as 'service delivery'.
- Alpamayo weight licensing conflict: the GitHub README says OpenMDW-1.1 permits commercial use, while an earlier Hugging Face card said non-commercial with commercial use on request. Which applies to Alpamayo 1.5 and 2 Super?
- Full OpenMDW-1.1 terms for Cosmos 3: attribution, guardrail and acceptable-use clauses and any field-of-use limits.
- CARLA governance and roadmap: will a 0.10.x/1.0 release ship on UE5, and will the leaderboard move to UE5? What role do NVIDIA and Neya Systems play in maintenance funding?
- How much simulation evidence will Korea's Level-4 performance certification and the Autonomous Ship Act performance verification accept, and which bodies (KATRI/TS, KRISO, KR) will define simulation-credibility criteria?
- The exact Euro NCAP 2026 virtual-testing acceptance procedure (manufacturer-submitted simulation vs lab-run), and whether K-NCAP will follow.
- dSPACE AURELION UE5 general-availability date, and whether dSPACE, IPG or Applied will license third-party neural or synthetic assets via OSI/OpenMATERIAL.
- HoloOcean license and 2.0 release date; OceanSim actual open-source license; DAVE ROS 2/Gazebo Harmonic migration status.
- MORAI's 2025–2026 financing, product roadmap (neural/Omniverse) and defense contracts, which determine whether it is a partner or a direct competitor.
- Commercial pricing for CarSim, CarMaker and BeamNG.tech seats, needed to design FMI bring-your-own-model bundles and price comparisons.
- GPU-hour cost per closed-loop neural-simulation kilometre (NuRec vs OmniDreams vs classic RTX), needed to set token pricing.


# TOPIC: realism
## Executive summary
Recommendation: do not build a renderer. Build on the NVIDIA OpenUSD/Omniverse RTX stack. Isaac Sim 6.0 went GA in June 2026 and 6.1.0 is out (Sep 2026). Isaac Sim now renders 3D Gaussian splats (3DGS/3DGUT) via the Fabric Scene Delegate, with multi-GPU, light interaction with meshes and MaterialX.
  Splats are stored in the new OpenUSD 26.03 UsdVolParticleField3DGaussianSplat schema. Real-time path tracing (RTX Real-Time 2.0) is the default render mode, and RTX lidar/radar/ultrasonic sensors sit in the same scene. The neural-reconstruction core has converged on permissively licensed
  NVIDIA/Berkeley code: gsplat (Apache-2.0, v1.6.0; 3DGUT, spinning-lidar rasterization, NCore v4, multi-GPU) and 3DGRUT (Apache-2.0, v1.1.0 on 2026-06-10, v2.0.0 with Neural Harmonic Textures in June 2026). Both handle fisheye/rolling-shutter cameras, include a physically-plausible ISP, and export
  NuRec USDZ for Isaac Sim, AlpaSim (Apache-2.0, ~900 reconstructed AV scenes) and CARLA. NeRF is no longer competitive as a simulation runtime: 3DGS/3DGUT is 100-200x faster to render and is now standardized (OpenUSD ParticleField, Khronos KHR_gaussian_splatting RC Feb 2026). NeRF survives only as
  a niche offline/extrapolation tool. CEN's NeRF-based 2D->3D pipeline should therefore be migrated, and its license checked (Instant-NGP is Nvidia Source Code License-NC). The biggest hidden risk is licensing. The original Inria 3DGS code and most mesh-extraction research code are non-commercial:
  2DGS and MILo (Gaussian-Splatting License), PGSR (ZJU non-profit), and Neuralangelo, Instant-NGP and nvdiffrast (NVIDIA NC). TRELLIS.2 is MIT but depends on nvdiffrast. Tencent's Hunyuan3D 2.1 license explicitly excludes South Korea, the EU and the UK, so a Korean company cannot legally use it.
  Commercially usable building blocks exist and should form the default stack: gsplat, 3DGRUT, fVDB Reality Capture, TRELLIS/TRELLIS.2 (MIT, minus nvdiffrast), SAM 3D Objects (SAM License), VGGT-1B-Commercial, MapAnything-apache, Depth Anything 3 small/base/metric (Apache), CoACD/CuACD (MIT),
  Articulate-Anything (MIT), Cosmos 3 (OpenMDW-1.1) and Cosmos Transfer 2.5 (NVIDIA Open Model License). Generative world models are now credible tools for appearance-level sim-to-real augmentation and policy evaluation, but they cannot replace physics. Examples: Cosmos Transfer 2.5
  (depth/edge/blur/segmentation multi-ControlNet, distilled edge model Feb 2026), Cosmos 3 (omnimodel, May/June 2026), Wayve GAIA-3/4, Runway GWM-1 Robotics, Decart Oasis 3 ($0.02/s API) and Genie 3 (consumer prototype only, no API). Use them as a post-render domain-adaptation layer with label-
  preserving controls and as an evaluation oracle. Physics, ground-truth labels and sensors stay in the simulator. The strategic move for CEN is to turn 'NeRF photo->3D' into a Real2Sim Asset Factory. The pipeline: phone/robot video -> feed-forward poses/depth -> 3DGUT splat (visual) -> surface mesh
  plus generative completion -> part segmentation and articulation (URDF/MJCF/USD Physics) -> convex decomposition -> VLM priors for mass/friction refined by video system identification -> automated physics validation -> a SimReady USD with a measured 'sim2real certificate'. This product, sold
  through the existing marketplace together with Korea-specific captured environments (factories, logistics, Korean roads), is a defensible moat because NVIDIA supplies tools but not curated, validated, domain-specific sim-ready content. Gap measurement must be built in from day 1. FID alone does
  not predict detector mAP, while newer structure-plus-appearance metrics reach Pearson r≈0.87-0.88 with downstream mAP, and splat-based real-to-sim policy evaluation (PolaRiS, soft-body GS twins) shows strong sim/real success-rate correlation. CEN should ship a Sim2Real Gap Scorecard covering
  perception mAP-transfer ratio, policy success correlation, physical trajectory error and sensor statistics as a platform feature. Note: the session's web-search budget ran out after ~60 searches. Later verification used primary GitHub sources. Items marked low confidence below were not verifiable
  with the remaining tools.
## Recommendations
- Engine decision for realism: adopt, don't build. Use Omniverse RTX via Isaac Sim 6.1+ and Isaac Lab 3.0 as the physically based render + sensor runtime. Use Blender Cycles for offline ground-truth renders on non-RT GPUs. Use the PlayCanvas engine / Spark (MIT, WebGPU/WebGL2) for CEN browser
  previews. Keep UE 5.8/CARLA as an optional AV connector only. Skip Unity HDRP (frozen) and Godot for realism.
- Adopt a 4-layer realism architecture in one OpenUSD stage. (L1) Physics-grounded meshes with MDL/MaterialX/OpenPBR and physics schemas. (L2) Neural-reconstructed backgrounds as UsdVolParticleField3DGaussianSplat (NuRec/3DGUT), with hidden proxy meshes for collision. (L3) Calibrated sensor models:
  RTX camera + PPISP, lidar, radar, ultrasonic, IMU noise; event via v2e/EVIS; tactile via TacSL/Taccel. (L4) Optional generative post-render augmentation (Cosmos Transfer 2.5 now, Cosmos 3 Nano fine-tuned later) driven by depth/segmentation/edge controls, with automatic label-consistency checks so
  labels stay valid.
- Evolve CEN's NeRF photo->3D pipeline into a 'CEN Real2Sim Forge'. Step 1: capture (phone/robot video, optional lidar). Step 2: feed-forward poses and metric depth (VGGT-1B-Commercial, MapAnything-apache, DA3-Metric-Large Apache). Step 3: 3DGUT splat training on gsplat/3DGRUT (Apache) for the
  visual layer. Step 4: surface mesh via gsplat-2DGS/fVDB plus an in-house PGSR/MILo-style re-implementation. Step 5: generative completion of unseen parts with TRELLIS.2 (replace nvdiffrast) and SAM 3D Objects for single-view clutter. Step 6: part segmentation + articulation (Articulate-Anything
  MIT as baseline; in-house model fine-tuned on CEN synthetic articulated data). Step 7: CoACD/CuACD collision. Step 8: VLM priors for mass/friction/material, refined by short interaction videos (system identification). Step 9: automated physics QA (drop, stack, push, joint-limit tests in
  Newton/PhysX). Step 10: export SimReady USD + URDF/MJCF + glTF (KHR_gaussian_splatting) with a 'sim-ready certificate' score.
- Make the moat data plus validation, not models. Monetize (a) certified sim-ready assets and (b) captured Korean environments: factories, logistics centers, shipyards, retail, Korean roads and signage, BIM-aligned sites. Also sell (c) paired real/sim datasets with measured gap scores. Feed customer
  captures back to fine-tune the generative/articulation models under clear data-rights terms.
- Run an immediate license audit (weeks, not months). Identify what CEN's current NeRF uses: Instant-NGP is NC; nerfstudio is Apache. Remove all Inria-derived 3DGS code (2DGS, SuGaR, MILo, PGSR, original 3DGS rasterizer, TRELLIS v1 diffoctreerast), nvdiffrast/nvdiffrec, CC-BY-NC weights and
  Hunyuan3D 2.x (license excludes South Korea). Standardize on Apache/MIT/OpenMDW components and get NVIDIA written confirmation on Omniverse/NuRec use in a multi-tenant cloud SaaS.
- Ship a Sim2Real Gap Scorecard as a first-class CEN feature. Rendering: PSNR/SSIM/LPIPS on held-out views. Perception: mAP_real of a synth-trained model divided by mAP_real of a real-trained one, few-shot real fine-tune curves, plus SDQM/SADGE-style predictors; FID/KID/CMMD as secondary only.
  Policy: paired sim-vs-real success over ≥5 policies, reporting Pearson r and ranking agreement, following PolaRiS. Physics: trajectory ADE/FDE, rest-pose error, contact force error. Sensors: lidar range/intensity error, Chamfer distance, noise PSD.
- Domain strategy: use Real2Sim splats to remove the target-site gap; structured domain randomization (Replicator) for the long tail; generative domain adaptation (Cosmos Transfer) for appearance diversity only; and always a small real fine-tune. Prioritize by measured scorecard gain per GPU-hour.
- GPU plan: split the CEN cloud into an RT-core render pool (L40S / RTX PRO 6000 Blackwell; Isaac Sim min A40) and a training/generative pool (H100/H200/B200 for gsplat training, TRELLIS.2, Cosmos). Budget estimate (my estimate, not sourced): 16-32 RT-core GPUs plus 8-16 H100-class for the first 12
  months of the realism workstream.
- Team for this workstream (estimate): 2-3 neural reconstruction (3DGS/3DGUT, lidar splats); 2 geometry/sim-ready (meshing, CoACD, USD physics); 2 generative 3D (TRELLIS.2 fine-tune, articulation, physical-property VLM); 1-2 sensor modeling (camera ISP, lidar/radar, tactile); 2 world-model post-
  training (Cosmos Transfer/Cosmos 3); 1-2 evaluation/metrics + real-data capture ops; 1 technical artist/material (OpenPBR/MDL). About 11-14 FTE.
- Roadmap. Q4 2026: license audit; NeRF->3DGUT migration; Isaac Sim 6.1 NuRec import/export; WebGPU splat viewer in the marketplace. Q1-Q2 2027: rigid-object Forge v1 (mesh + collision + VLM mass/friction + physics QA), scene-scale capture for 2-3 Korean pilot sites, scorecard v1. Q3 2027:
  articulation + sensor profiles (lidar/radar/event) + Cosmos Transfer augmentation with label QA. Q4 2027-2028: deformables (PhysTwin-style), world-model-based policy evaluation (Cosmos 3), relightable splats; track the UE6 and Cosmos 3.x transitions.
- Track and benchmark quarterly, but do not build on: Genie 3 (no API), GAIA-3/4 (proprietary), Decart Oasis 3 and Runway GWM-1 (APIs could be optional long-tail video sources), World Labs Marble (possible environment API partner and also a competitor), Hunyuan3D 3.x (API only; Korea terms
  unverified).
## Risks
- License contamination. Most high-quality 3DGS mesh-extraction code (2DGS, MILo, PGSR, SuGaR?) and NVIDIA research code (Instant-NGP, nvdiffrast, Neuralangelo) are non-commercial. Hunyuan3D 2.1 explicitly bans use in South Korea. Shipping any of these in CEN creates IP liability and could block
  enterprise sales or M&A.
- NVIDIA lock-in. Omniverse license terms for multi-tenant cloud SaaS, the RT-core GPU requirement (H100 fleets cannot run RTX rendering efficiently) and rapid API churn (sensors.rtx deprecated in 6.0; Cosmos 2.5 superseded in ~8 months) raise switching costs.
- Splat limitations. Lighting is baked unless relightable variants are used. Splats have no inherent physics or collision, so proxy meshes are needed. Novel-view extrapolation away from capture trajectories degrades, and lidar/radar on splats is less mature than on meshes, so the sensor gap can
  persist even when RGB looks perfect.
- Generative 3D outputs are not simulation-truthful: they lack metric scale, contain hallucinated hidden geometry, are non-watertight and have no physical parameters. VLM-estimated mass/friction can be off by large factors, so policies trained on them may fail on contact-rich tasks without system-ID
  refinement.
- Generative world models (Cosmos, GAIA, Genie, Decart) can hallucinate physics and shift object boundaries. That silently corrupts labels in synthetic datasets, and they are costly per frame. Overreliance undermines CEN's 'controllable, reproducible' value proposition.
- Metric risk: FID/KID can look good while detector mAP or policy success does not transfer. Without paired real data the platform cannot prove realism claims to customers.
- Competitive risk: NVIDIA (NuRec, Cosmos, SimReady), World Labs (Marble splat+collider worlds) and Meshy/Tripo/Rodin are moving into sim-ready asset/world generation, so a pure 'photo->3D' feature will be commoditized within 12-18 months.
- Privacy and regulatory risk when capturing real Korean sites and roads (faces, license plates, factory IP) under PIPA and customer NDAs. Capture pipelines need anonymization (blurring/inpainting) before splat training and marketplace distribution.
- Engine transition risk: UE6 early access in late 2027 and Unity HDRP stagnation make game-engine-centric investments short-lived.
- Research-to-product risk: many key methods (PhysTwin, PolaRiS, PhysX-Anything, Articulate-Anything) are single-paper codebases with limited robustness and maintenance.
## Open questions
- What exactly does CEN's current NeRF pipeline use (Instant-NGP, nerfstudio, custom)? This determines license exposure and migration effort.
- Which vertical comes first (industrial manipulation, warehouses/AMRs, Korean AV, shipyards)? It decides whether radar/lidar/event/tactile realism or RGB realism dominates the investment.
- What are NVIDIA's terms for running Omniverse Kit/RTX, NuRec and Isaac Sim in a multi-tenant commercial cloud workspace (and Inception/partner options)? Could not verify; docs.nvidia.com was blocked.
- Cosmos 3 parameter sizes and licensing conflict (GitHub: 64B/16B/4B under OpenMDW-1.1; press: 32B/8B, NVIDIA Open Model License). Needs confirmation from the model cards.
- Does Isaac Sim 6.1 support RTX lidar/radar returns from splat (ParticleField) content, and automatic collision proxies for NuRec scenes? Release notes were unreachable (domain blocked).
- Current Epic Unreal licensing for non-game simulation SaaS in 2026, and whether CARLA's UE5 branch plus NuRec integration is production-ready. Not verified this session.
- Odyssey world model status, DIGIT/TACTO simulator maintenance, V-HACD license/version, and the full SAM License commercial terms were not verified (low confidence).
- Whether Tencent changed Hunyuan3D licensing after the July 2026 Hunyuan LLM Apache-2.0 switch. The current Hunyuan3D-2.1 LICENSE on GitHub still excludes South Korea.
- How much paired real data customers will share for gap measurement, and under what data-rights model it could improve CEN's shared models.
- Web-search budget for this session ran out after ~60 searches. Later items rely on primary GitHub fetches; SIGGRAPH 2026 / CoRL 2026 / RSS 2026-specific announcements beyond those captured above were not exhaustively searched.


# TOPIC: platform_arch
## Executive summary
Recommendation: build the platform layer in-house and adopt the engines. That means the control plane, scene/version service, twin connectors, web UX, MCP/agent layer, metering and multi-tenancy. Do NOT write a physics engine or renderer, because the open engines matured sharply in 2026. Make
  OpenUSD the canonical internal scene format. AOUSD Core Spec 1.0.1 was published 2025-12-12 under CC-BY-ND-4.0, and OpenUSD 26.08 shipped 2026-07-20 with UsdPhysics nested-rigid-body support, UsdValidation fixers, wasm builds and a Gaussian-splat UsdVolParticleField schema. Note that Core 1.0
  standardizes only the data model, composition and value resolution, not UsdPhysics. Express physics as UsdPhysics plus backend-namespaced applied schemas (newton-usd-schemas Apache-2.0 v0.x, mjcPhysics, PhysxSchema). URDF, MJCF, SDFormat, glTF, FBX, PLY and SPZ are edge formats, handled by
  Apache-2.0 converters: newton-physics/urdf-usd-converter, mujoco-usd-converter and adobe/USD-Fileformat-plugins. The engine-agnostic seam already exists and should be copied, not invented. Isaac Lab 3.0.0-EA (2026-09-16, built for Isaac Sim 6.1, Newton 1.5.2, Warp 1.16) lets you pick
  physics=isaacsim_physx|ovphysx|newton_mjwarp and renderer=isaacsim_rtx|ovrtx|newton_renderer, and supports Kit-less execution with Warp/DLPack tensor paths. AICHEMIST's 'Sim Kernel API' should mirror that factory pattern. Suggested backend defaults: Newton 1.6.1 (Apache-2.0, Linux Foundation,
  2026-10-05; MuJoCo-Warp/VBD/MPM/Kamino, deterministic paths since 1.4) for robot learning. ovphysx 0.6 (PhysX SDK 5.11, BSD-3, pip install) for USD-native industrial/vehicle rigid-body work. MuJoCo 3.15 CPU as the deterministic golden reference. ovrtx (pre-release, NVIDIA proprietary license) or
  Isaac Sim 6.1 for RTX camera/lidar/radar fidelity. NVIDIA itself is moving to modular headless libraries (ovrtx, ovphysx, ovstorage, announced GTC 2026, early access). Kit continues (Kit 110.3.0, 2026-08-28), but the Launcher (2025-10-01) and the old web-viewer-sample are deprecated. So confine
  Kit to where it is irreplaceable (Isaac Sim apps, Replicator SDG, ROS bridge, Kit App Streaming) and keep the physics path fully open-source to avoid lock-in. Live twins should flow OPC UA (open62541, MPL-2.0) / MQTT / ROS 2 (Lyrical Luth LTS, released 2026-05-22, EOL May 2031) into Kafka, then
  into a twin-state service (Eclipse Ditto-style with W3C WoT descriptions), then into a USD 'live session layer' plus a time-series DB (InfluxDB 3 or TimescaleDB). Simulation twins fork from a live snapshot for what-if, RL and synthetic-data runs. Standard formats per data class: MCAP (MIT; rosbag2
  default) for raw logs, LeRobotDataset v3 (many episodes per Parquet/MP4, Hub streaming) for training exports, FMI 3.0.2 FMUs plus SSP for vehicle and factory system models. UX should be browser-first and hybrid. The default is client-side WebGPU/WebGL with zero server GPU cost (three.js r186,
  Babylon.js 9.29 with an OpenUSD WASM loader, PlayCanvas 2.23 splat LOD streaming, Spark for 3DGS). Server-side WebRTC pixel streaming (Kit livestream, own NVENC pipeline, UE Pixel Streaming 2 for UE5.7/5.8) is used only for RTX-fidelity sessions and scales to zero when idle. Compute runs on
  Kubernetes + GPU Operator v26.7 + KAI Scheduler (Apache-2.0, the open-sourced Run:ai scheduler core: gang scheduling, fractional GPU, hierarchical DRF queues). Add Ray 2.59 for RL and data pipelines, SkyPilot for multi-cloud spot burst, and optionally Slinky (Slurm-on-K8s) and NVIDIA OSMO
  (Apache-2.0) for physical-AI workflow DAGs. Split GPU pools by capability. RT-core GPUs (L40S at $1.861/h, RTX PRO 6000 at $3.363/h on AWS us-east-1 on-demand; Seoul about 23% higher) handle rendering, streaming and SDG. H100/B200 ($6.88/GPU-h for H100) handle training and render-free physics
  only. Never time-slice GPUs across tenants. Version scenes as content-hashed USD layer stacks, and make replay reproducible by pinning container digest, driver, GPU SKU, seeds and an MCAP input log. lakeFS moved to BSL 1.1 in v1.87.0 (Sept 2026), so treat it as license-sensitive. Expose everything
  through a first-party MCP server plus a sandboxed USD code-generating agent with validation gates. Community MCPs (isaac-sim-mcp, blender-mcp, unreal-mcp) execute arbitrary code and are prototypes only. The biggest commercial risk is licensing: Kit, ovrtx and the Omniverse blueprints are under
  NVIDIA proprietary terms, so hosted-SaaS rights must be negotiated with NVIDIA before GA.
## Recommendations
- BUILD vs ADOPT. Build in-house: the control plane (tenancy, auth, metering into CEN tokens), scene/version service, twin-connector service, Sim Kernel API, web UX, first-party MCP server and agent, and dataset/marketplace integration. Adopt as pluggable backends: Newton, ovphysx/PhysX, MuJoCo,
  ovrtx/Isaac Sim RTX, Gazebo, CARLA and FMUs. Never fork or write a physics engine; contribute upstream to Newton (Linux Foundation, Apache-2.0) instead.
- REFERENCE ARCHITECTURE, 8 layers. L0 Infra: K8s + GPU Operator + KAI Scheduler, with node pools RT-render (L40S / RTX PRO 6000), Compute-train (H100/H200/B200) and Light (L4/CPU). L1 Data: S3-compatible object store (canonical blobs), Postgres (metadata, scene commits), Kafka (event backbone),
  TSDB (telemetry), Iceberg/DVC (datasets), model registry. L2 Scene model: OpenUSD stage service with validation. L3 Sim Kernel: engine-agnostic physics, sensor and co-sim orchestrator. L4 Twin runtime: Live mode, Simulation mode and Shadow/HIL mode. L5 Learning: Isaac Lab 3 / Newton envs, LeRobot,
  Ray RLlib, SDG pipelines, evaluation harness. L6 Platform APIs: REST/gRPC + Python SDK + MCP. L7 UX: browser-first WebGPU client, on-demand WebRTC streaming, Jupyter/VS Code in the CEN workspace. L8 Agents: LLM planner + sandboxed USD code generation + validation gates.
- CANONICAL INTERNAL STANDARDS. Scene, assets, robots and vehicles: OpenUSD (pin a version per platform release, e.g. 26.08), with UsdPhysics as the portable core plus namespaced applied schemas (newton:*, mjc:*, physx*) for backend extras, and UsdSemantics labels for SDG. Raw logs: MCAP. Robot-
  learning datasets: LeRobotDataset v3 (export COCO/KITTI/nuScenes-style for perception). System models: FMI 3.0 FMUs + SSP. Twin metadata: W3C WoT Thing Description (as in Ditto) mapped 1:1 to USD prim paths. Web delivery: glTF/GLB + SPZ/SOG splats compiled from USD. Edge-only formats: URDF, MJCF,
  SDF, FBX, OBJ, STL, OpenDRIVE, OpenSCENARIO, OSI.
- ENGINE-AGNOSTIC SIM KERNEL API. Copy Isaac Lab 3.0's factory pattern: backend = {physics: newton_mjwarp | ovphysx | mujoco_cpu | gazebo | fmu}, renderer = {ovrtx | isaacsim_rtx | newton_gl | none}. The minimal ABI: load(usd_stage_ref, backend_cfg); step(dt, substeps, n_envs); get_state/set_state
  as Warp/DLPack tensors; apply_actions; render(sensor_ids) to tensors; contacts(); snapshot() / restore(blob); set_seed(); capabilities(). Ship a conformance suite (falling box, pendulum, Franka pick, wheeled vehicle, cloth) that compares backends within tolerances and runs in CI on every backend
  upgrade.
- LIVE-TWIN vs SIMULATION-TWIN. Live mode: edge gateway (OPC UA via open62541, MQTT, ROS 2 over Zenoh or a DDS bridge) feeds Kafka, then the twin-state service (latest state + WoT model), then a per-twin USD session layer that overrides only transforms, joint states and signals at 10-60 Hz and is
  pushed to browsers over WebSocket. History goes to the TSDB. Simulation mode: headless batched runs faster than real time, on spot. Fork-from-live: snapshot the live state, then calibrate (system ID / parameter estimation), then run what-if or RL in Simulation mode on a scene branch, then compare
  predictions against later live data to score twin fidelity. Shadow/HIL mode: run real controllers against the sim with use_sim_time and a lockstep clock.
- BROWSER-FIRST UX. Make the WebGPU/WebGL client the default: Babylon.js 9.x if reading USD client-side, or three.js r186 + Spark for splats and glTF. Bake USD into glTF/splat LOD tiles server-side on asset commit. Offer a 'High-fidelity view' button that launches a WebRTC pixel-stream session: Kit
  USD Viewer template with livestream, or your own ovrtx + NVENC + WebRTC service. Put sessions behind a session manager with 5-10 minute idle auto-suspend and warm pools. Reuse CEN's browser virtual OS/JupyterLab (Selkies-style) for code-first users. Host streaming GPUs in Seoul for Korean
  customers, since latency matters more than the roughly 23% price premium.
- COST-EFFICIENT GPU SCHEDULING. Use KAI hierarchical queues: tenant, then tier (interactive / batch / training), with guaranteed quotas for paid tiers and preemptible over-quota. Run batch SDG, RL and evaluation on spot with frequent checkpointing (Newton/Isaac Lab state snapshots + MCAP), and
  burst through SkyPilot across AWS, GCP and Korean CSPs. Route render-free physics RL (Newton/MuJoCo Warp) to the cheapest adequate GPU: often an L40S or RTX PRO 6000 beats an H100 on price per env-step for simulation. Benchmark steps/s/$ per backend and GPU monthly. Reserve H100/B200 for
  VLA/foundation-model training. Use a reserved or on-prem RTX PRO 6000 baseline for steady interactive load. Meter GPU-seconds per tenant from DCGM and KAI into CEN tokens.
- MULTI-TENANT ISOLATION. Give each paying tenant whole GPUs or MIG slices (RTX PRO 6000 / H100). Allow time-slicing and KAI fractional sharing only within one tenant's own jobs, or for free-tier previews on dedicated 'untrusted' node pools. Run user code and agent-generated code in Kata Containers
  or gVisor (Ray Sandbox is experimental). Isolate networks per tenant namespace. Encrypt buckets per tenant. Add data-residency tags (KR / US / EU) enforced by the scheduler.
- DETERMINISM AND REPLAY. Define a 'Run Manifest': scene commit hash (USD layer-stack content hashes), asset blob hashes, container image digest, backend + version, GPU SKU + driver, seeds, dt and substeps, plus the MCAP input log (actions and external live data). Use Newton's deterministic mode
  (v1.4+) or MuJoCo CPU for bit-exact regression. Use tolerance-based comparison for GPU PhysX and RTX. Store manifests with every dataset and model for lineage, which also supports enterprise audits and the CEN marketplace provenance story.
- SCENE VERSIONING. Implement a thin 'scene commit' service rather than adopting lakeFS (now BSL 1.1). Each edit or session writes its own USD layer; commits are immutable manifests; branches are pointers; merges work at layer granularity with conflict detection on prim paths. Offer Git/Git-LFS and
  Perforce sync connectors for enterprise customers, and Iceberg or DVC snapshots for datasets.
- OBSERVABILITY. Use OpenTelemetry traces from job submit through scheduler, sim step, render and encode. Use Prometheus + DCGM exporter for GPU utilisation, memory, NVENC and power. Track sim-specific SLOs: real-time factor, steps/s/GPU, solver NaN/explosion detectors, contact counts, streaming RTT
  and frame drops. Use Rerun or Lichtblick embedded for episode debugging. Track cost per job and per tenant on dashboards.
- AGENT / MCP LAYER. Expose a first-party MCP server (spec rev 2026-07-28) with typed, permissioned tools: scene.search/query/diff, scene.apply_ops (high-level USD ops, not raw exec), asset.search (marketplace), sim.run/sweep, job.submit/status, twin.query/forecast, dataset.export, policy.evaluate.
  Add a code-generating authoring agent that writes USD Python in a sandbox. Gate its output with UsdValidation, physics sanity checks (mass/inertia, interpenetration, joint limits) and a backend smoke test before the commit lands on a branch; a human approves merges. Use NVIDIA kit-usd-agents MCPs
  for API grounding. Wrap ros-mcp-server behind tenant ACLs for robot connections. Do not expose community MCPs with arbitrary exec to tenants.
- NVIDIA LICENSING AND LOCK-IN. Before GA, obtain written NVIDIA terms for hosting Kit apps, ovrtx and Isaac Sim (Kit runtime) as multi-tenant SaaS (Omniverse Enterprise / OEM / partner program). Keep a fully open fallback path: Newton/MuJoCo/ovphysx (BSD) physics + newton_gl / web renderers +
  Gazebo. That way the core product survives a licensing change, with RTX fidelity sold as a premium tier.
- ROADMAP. M0-3 (MVP): USD scene service + importers (URDF/MJCF/glTF via converters), Sim Kernel with Newton + ovphysx + MuJoCo, batch jobs on K8s/KAI, three.js/Babylon viewer, MCAP logging, LeRobot v3 export, first-party MCP (read and run tools). M3-9: ovrtx/Isaac Sim RTX sensors and SDG, WebRTC
  premium sessions, Isaac Lab 3 training templates (RL + IL/VLA fine-tuning), live-twin connectors (ROS 2/Zenoh, MQTT, OPC UA) + TSDB, scene commits and branches, authoring agent with validation gates. M9-18: FMI/SSP co-simulation, vehicle module (OpenDRIVE/OpenSCENARIO/OSI), fork-from-live
  calibration, enterprise on-prem/VPC deployment (Helm), MIG-based tenancy, marketplace integration of SimReady assets and datasets, SOC2/ISMS-P.
- TEAM, about 22-26 FTE by month 12 (estimate). Platform/infra/SRE 4 (K8s, KAI, networking, security). Sim kernel and physics integration 4 (Newton/PhysX/MuJoCo, conformance, determinism). Rendering/sensors/streaming 3 (ovrtx, WebRTC, NVENC). Web 3D and frontend 3. Data/ML (SDG, RL/IL/VLA, LeRobot)
  4. IIoT/live-twin integration 2. LLM/agent/MCP 2. PM, solutions and DevRel 2. Hire at least one USD expert and one OPC UA/industrial engineer early.
- INFRA BUDGET (rough, derived from AWS list prices). Dev/staging: 1x 8-GPU RTX PRO 6000 node, about $24k/month on-demand or much less spot/reserved, or buy on-prem. Early production (approx. 20 concurrent premium sessions + batch): about $40-80k/month blended with 40-60% on spot. Training bursts:
  8x H100 at about $40k/month if always on, so schedule bursts instead. Default to client-side rendering to keep the GPU bill proportional to premium usage.
## Risks
- NVIDIA proprietary licensing: Kit SDK, ovrtx and the Omniverse blueprints are under NVIDIA SLA / Product-Specific Terms. Rights to host them as multi-tenant SaaS and to charge tokens for their use are unverified and could block or tax the premium fidelity tier.
- API churn in early-access and fast-moving components: ovrtx, ovphysx and ovstorage are pre-1.0; newton-usd-schemas is v0.x experimental; Isaac Lab 3.0 changed quaternion order and data types; Kit went through about 3 majors in 12 months. Integration maintenance could consume a large share of
  engineering time without a strict adapter layer and conformance suite.
- No normative physics standard: AOUSD Core 1.0 excludes UsdPhysics, and glTF physics is still a review draft. Cross-engine physics portability depends on vendor schemas, so the same USD asset can behave differently on Newton vs PhysX vs MuJoCo.
- GPU determinism limits: bit-exact replay is only realistic on CPU MuJoCo or Newton's deterministic paths on identical hardware and drivers. RTX rendering and GPU PhysX need tolerance-based validation, which complicates audit and replay claims.
- Multi-tenant GPU security: time-slicing and fractional sharing give no memory or fault isolation, and MIG availability on RT-core GPUs in Korean clouds is unverified. Agent-generated and user code is an RCE surface (community MCPs explicitly execute arbitrary Python).
- Cost blow-up from pixel streaming: a dedicated L40S per session is about $1.9-2.3/h. Without client-side default rendering, auto-suspend and warm pools, gross margins on subscriptions can go negative.
- License drift in the open-source stack: lakeFS moved to BSL 1.1 (v1.87.0), Foxglove Studio went closed (hence the Lichtblick fork), and TimescaleDB TSL restricts DBaaS. Every embedded dependency needs SPDX tracking and license review.
- ROS 2 fragmentation: customers on Humble, Jazzy and Lyrical at once, and Isaac Sim's ROS workspace lists only Humble and Jazzy. Bridges must be multi-distro and Zenoh/DDS-aware.
- NVIDIA hardware lock-in: Newton, Warp, ovrtx and Isaac all need CUDA/RTX, so there is no AMD/Intel fallback for GPU physics or rendering. Supply and price shocks pass straight through.
- Data residency and latency: Korean public-sector and manufacturing customers may require domestic hosting. Seoul GPU prices are about 23-38% higher and capacity for new SKUs (RTX PRO 6000, B200) may be limited.
- Research verification gap: the web-search budget ran out after a few queries, and many primary vendor domains (developer.nvidia.com, docs.omniverse.nvidia.com, docs.ros.org, aousd.org, gazebosim.org, AWS docs) were egress-blocked. Several 2026 facts were verified only through GitHub pages; GitHub
  release dates without a year were inferred as 2026 from version context.
## Open questions
- What are NVIDIA's exact commercial terms for hosting Kit apps, Isaac Sim and ovrtx in a multi-tenant SaaS (Omniverse Enterprise per-GPU pricing in 2026, OEM/partner programs, NVIDIA Inception benefits)? When do ovrtx, ovphysx and ovstorage reach 1.0/GA?
- Does RTX PRO 6000 Blackwell MIG (profile sizes, number of instances, RTX/NVENC availability per slice) work under GPU Operator v26.7 and KAI? Which Korean CSPs (Naver Cloud, KT Cloud, NHN Cloud, Samsung SDS) offer it, and at what price?
- What is the AOUSD roadmap for normative domain specs (UsdGeom, UsdShade, UsdPhysics) after Core 1.0, and should AICHEMIST join AOUSD to influence the physics/SimReady specs?
- When will Isaac Sim support ROS 2 Lyrical, and what are the full Isaac Sim 6.1 / 7.0 release notes on Kit version, Newton/ovphysx integration and streaming? (The docs site was blocked this session.)
- Exact Gazebo Jetty release and EOL dates; SSP 2.0 release status; current OpenDRIVE, OpenSCENARIO and OSI versions for the vehicle module.
- What are the SIGGRAPH 2026 (July) announcements on Omniverse libraries open-sourcing and the Agent Toolkit? Secondary coverage suggests expanded open-source libraries and agent tooling; this needs primary-source confirmation.
- What is measured steps/s/$ for Newton vs ovphysx vs MuJoCo Warp on L40S vs RTX PRO 6000 vs H100 for AICHEMIST's target tasks? (Internal benchmark needed before GPU pool sizing.)
- Is a CEN marketplace dataset in LeRobot v3 / MCAP formats acceptable to target customers, and which perception label formats (COCO, KITTI, nuScenes, OpenLABEL) must be supported for SDG exports?
- Should the live-twin state service build on Eclipse Ditto (EPL-2.0, JVM/MongoDB) or a lighter in-house service on Kafka + Postgres? This depends on expected twin counts and update rates.


# TOPIC: training
## Executive summary
Method note: the shared WebSearch budget (200 calls per turn across all agents) was already used up when this agent started, so I could not run any searches. I also could not reach arxiv.org, huggingface.co, nvidia.com, deepmind.google, pi.website or wikipedia (the network proxy blocked them).
  Everything marked high confidence was checked against primary sources I could reach: GitHub repos, release pages, raw docs and the PyPI JSON API. Facts about Gemini Robotics, pi*0.6, Figure Helix, Genie 3, DreamerV4, Jetson Thor specs and GTC/CoRL 2026 keynotes come from memory and are marked
  medium or low confidence.

Bottom line: do not build an RL/IL/VLA training engine. Integrate the open stack that is settling in 2026 and put AICHEMIST's engineering into orchestration, usability, data, evaluation and sim2real tooling. (1) Isaac Lab 3.0 shipped Early Access on 2026-09-16, with GA targeted for end of October
  2026. It brings multi-backend physics (PhysX, OVPhysX, Newton/MuJoCo-Warp), a 'Kit-less' mode that runs without the Isaac Sim installation, one `isaaclab` training command over RSL-RL, skrl, RL-Games, SB3 and RLinf (for VLA post-training), multi-GPU and multi-node RL, and Isaac Teleop. It also
  breaks APIs: quaternions change from WXYZ to XYZW and data now comes back as ProxyArray objects. (2) mjlab 1.6.0 (Apache-2.0, 2026-08-09) offers the same manager-based API on MuJoCo Warp 3.15 with no Omniverse dependency. That matters for a multi-tenant SaaS, because Isaac Sim/Kit binaries ship
  under NVIDIA's proprietary Omniverse terms. (3) For imitation learning and VLAs, LeRobot 0.6.1 (Apache-2.0, 2026-08-03) is the common layer. It provides the LeRobotDataset v3 format (Parquet + MP4 shards, streaming from the Hub) and ready-to-train ACT, Diffusion, pi0, pi0.5, pi0-FAST, SmolVLA,
  GR00T N1.7, X-VLA, Wall-X and EO-1, plus RoboCasa365, RoboTwin 2.0, LIBERO-plus and Isaac Lab Arena environments. (4) Default VLA bases with commercial-friendly licenses are NVIDIA GR00T N1.7 (3B, Cosmos-Reason2-2B backbone, code Apache-2.0, weights under the NVIDIA Open Model License), openpi
  pi0.5 (code Apache-2.0; weight terms still to be confirmed) and SmolVLA (450M, Apache-2.0). Gate out non-commercial weights such as AgiBot GO-1 (CC BY-NC-SA) and RLWRLD RLDX-1 (a non-commercial model license). (5) World models are now practical tools for training and data. NVIDIA Cosmos 3
  (May/June 2026, OpenMDW-1.1) comes as Super 64B, Nano 16B and Edge 4B and includes robot policy variants; Cosmos-Predict2.5 and Transfer2.5 are no longer actively developed. (6) Training compute is modest for RL controllers and large for foundation models. The Isaac Lab benchmark on one RTX 4090
  is about 82k env-steps/s for G1 rough-terrain locomotion including training, and about 170k for Shadow-hand in-hand cube reorientation. In practice a quadruped policy takes under an hour on one GPU, a humanoid velocity controller 1–2 h, and a generalist humanoid tracking teacher 23.3 h on a 4090
  (HOVER). SONIC-scale humanoid foundation controllers need 64+ GPUs just for fine-tuning. VLA fine-tunes run from about 4 A100-hours (SmolVLA, 20k steps) to hundreds of GPU-hours (OpenVLA-OFT: 8 GPUs, 150k steps). (7) Plan two GPU pools. Isaac Sim RTX rendering and synthetic-data generation need
  GPUs with RT cores (L40S, RTX PRO 6000, RTX 4090/5090), while VLA and world-model training needs H100/H200/B200; the RT-core requirement is from memory, medium confidence. (8) AICHEMIST's moat should be: a no-code/LLM-driven task, reward and domain-randomization editor on CEN's browser workspace;
  a Real2Sim asset pipeline (from its NeRF work to SimReady USD with physics parameters); a LeRobot-v3 dataset and synthetic-data marketplace with lineage; one-click Mimic data multiplication; a sim2real toolkit (system ID, actuator nets, sim2sim gates); closed-loop regression evaluation;
  ONNX/TensorRT packaging for Jetson; and a deployment→failure-mining→re-simulation data flywheel. (9) Licensing traps to design around: the Omniverse EULA for cloud hosting, the cuRobo license inside SkillGen, the NVIDIA Source Code License on MimicGen and DexMimicGen, GPL-3.0 BlenderProc, AGPL-3.0
  Ultralytics, CC BY-NC assets in ManiSkill, and the Llama 2 license on OpenVLA weights. (10) Suggested team for the training module: 8–12 FTE. A credible first release fits in 6 months on 1 H100/H200 node plus 2 RT-GPU nodes, or the cloud equivalent.
## Recommendations
- DECISION, build vs adopt: do not build physics, RL algorithms, VLA architectures or world models. Adopt Isaac Lab 3.0 (start on 3.0 EA now, pin to GA in Nov 2026) as the primary training runtime, with mjlab/MuJoCo-Warp (Apache-2.0) as the license-clean second backend behind one AICHEMIST task-spec
  abstraction. Build the product layer on top: orchestration, UX, data, evaluation, sim2real and deployment.
- DEFAULT STACK, RL: Isaac Lab 3.0 (PhysX for contact-rich manipulation, Newton/MuJoCo-Warp for locomotion and Kit-less jobs) + rsl_rl 5.5.x (PPO, distillation, symmetry, RND, bf16) as default; skrl 2.1 for multi-agent and off-policy; SB3 2.9 for the education tier; RLinf 0.3 for VLA RL post-
  training (phase 2). Skip PufferLib and LeanRL (archived) for robotics.
- DEFAULT STACK, imitation learning and VLA: LeRobot 0.6.x as the training engine and LeRobotDataset v3 as the single dataset format for CEN's marketplace (real, synthetic and teleop data). Offer three VLA tiers: SmolVLA (450M, Apache-2.0, ~4 A100-h fine-tune) for low cost; pi0.5 via openpi/LeRobot
  for arm manipulation (confirm weight terms with PI); GR00T N1.7 (NVIDIA Open Model License) for humanoids and bimanual robots. Keep ACT and Diffusion Policy as fast single-task baselines.
- DEFAULT STACK, data generation: Isaac Teleop (XR/Apple Vision Pro via CloudXR, MCAP) + GELLO/SpaceMouse for capture; Isaac Lab Mimic (Apache-2.0) to multiply 5–10 demos into ~1,000. Avoid the MimicGen/DexMimicGen code (NVIDIA Source Code License). Use SkillGen only after reviewing the cuRobo
  license.
- DEFAULT STACK, perception SDG: Isaac Sim 6.x Replicator with SimReady assets and domain randomization → COCO/KITTI; Cosmos 3 (OpenMDW-1.1) or Transfer-class augmentation for photoreal variation in phase 2; train RF-DETR (Apache-2.0 N–L) or other Apache detectors, not Ultralytics (AGPL), unless you
  buy an enterprise license; SAM 3.1 + VLM captioning for auto-labeling real data (legal review of the SAM License).
- DEFAULT STACK, MLOps: Kubernetes + KubeRay/Kueue job scheduler bound to CEN tokens; torchrun DDP and Isaac Lab multi-node; Hydra configs with full sim-config hashing; MLflow 3.x self-hosted as tracking and model registry (W&B optional connector); DVC or lakeFS + HF-Hub-compatible storage for
  datasets; Rerun/Viser in-browser rollout viewers; ONNX (opset-pinned) → TensorRT engine builder per JetPack version (Jetson Thor/Orin) with latency profiling; MCAP logs from the field.
- DAY-1 MUST-HAVES (MVP in about 6 months): (1) task template catalog: quadruped and humanoid velocity locomotion, humanoid motion tracking (BeyondMimic/HOVER-style), arm reach/pick/place, Mimic-based imitation learning, VLA fine-tune, synthetic-data detector; (2) GUI + YAML editors for rewards,
  observations, domain randomization (mass, friction, motor strength/latency, sensor noise, visuals) and curricula; (3) one-click RL training on 1–8 GPUs with live video rollouts and metrics; (4) teleop-to-dataset (LeRobot v3) + Mimic generation + imitation/VLA fine-tuning; (5) closed-loop
  evaluation harness (Isaac Lab Arena + LIBERO-plus/RoboCasa365 + customer scenario suites) with success-rate confidence intervals and regression gates; (6) automatic sim2sim gate (PhysX↔Newton/MuJoCo) before export; (7) ONNX/TorchScript/TensorRT export with a Jetson packaging recipe; (8) experiment
  tracking, model registry and lineage (assets → scene → dataset → checkpoint → evaluation); (9) license gating that blocks non-commercial weights and assets in commercial workspaces.
- PHASE 2 (6–12 months): multi-node RL and population-based training (PBT)/automatic domain randomization (ADR) sweeps; RLinf VLA RL post-training; HIL-SERL real-world RL and residual RL on top of VLAs; system-identification wizard (fit actuator nets and friction/mass/latency from real logs; ASAP-
  style delta-action correction); Real2Sim pipeline turning CEN NeRF/3DGS captures into SimReady USD with collision and physics parameters; Cosmos-based photoreal augmentation and world-model-based policy pre-screening; LLM text-to-environment/reward agent built on Isaac Lab 3.0 agent skills and
  CEN's LLM command interface.
- PHASE 3 (12–24 months): fleet data flywheel (field telemetry → failure mining with VLM/SAM → automatic scenario regeneration in sim → retrain → gated redeploy); hosted public leaderboards (Arena-based) in the marketplace; humanoid foundation-WBC fine-tuning service (SONIC-class, 64+ GPU jobs);
  vehicle/AV and drone training tracks (AV mostly perception and closed-loop scenario evaluation; drones via Isaac Lab multirotor/thruster actuators).
- SIM2REAL TOOLKIT to ship as productized defaults: domain randomization presets per robot class; actuator-network training from motor logs; privileged teacher → student distillation (rsl_rl distillation); observation-latency and noise injection; sim2sim cross-engine check; real2sim2real loop with
  Real2Sim scans; residual RL; systematic real-vs-sim evaluation correlation in the style of SimplerEnv MMRV/Pearson.
- COMPUTE PLAN: split pools. RT-core GPUs (L40S / RTX PRO 6000 / RTX 4090-5090) for Isaac Sim rendering, synthetic data and RL; H100/H200/B200 for VLA, Cosmos and large fine-tunes. Typical budgets: quadruped 0.3–1 GPU-h per run; humanoid velocity 1–2 GPU-h per run; humanoid generalist tracking
  teacher ~23 h on one RTX 4090 (HOVER); state-based dexterous 3–8 GPU-h; vision dexterous 200–600 GPU-h; SmolVLA ~4 A100-h; GR00T/pi0.5 single-task 2–40 H100-h; OpenVLA-OFT ~200–400 GPU-h; detector on 50k synthetic images ~15–70 GPU-h end-to-end. Price CEN tokens on GPU-hour × pool type.
- TEAM (training module, 8–12 FTE): 2 RL/sim2real engineers (locomotion, WBC, dexterous), 2 imitation-learning/VLA engineers, 1 synthetic-data/perception engineer, 1 world-model/Cosmos engineer (phase 2), 2–3 MLOps/platform engineers (K8s, Ray, registry, billing hooks), 1 robotics deployment
  engineer (ROS 2, Jetson, TensorRT), 1 product/UX lead for the no-code editors. Add part-time legal for model and asset licensing.
- PARTNERSHIPS: join NVIDIA Inception/Omniverse partner programs early to settle the Isaac Sim/Omniverse terms for multi-tenant cloud hosting; explore Korean VLA partners (RLWRLD RLDX-1 uses a synthetic-augmented pipeline, so CEN can sell data to them); contribute Newton/mjlab integrations to stay
  engine-neutral.
- GO-TO-MARKET FIT: position the training module as 'synthetic data + training + evaluation in one place'. CEN's marketplace of assets, datasets and benchmarks plus one-click Mimic data multiplication and closed-loop evaluation is the differentiator; raw training throughput is a commodity.
## Risks
- Isaac Lab 3.0 is Early Access with heavy breaking changes (quaternion order, ProxyArray, actuator API, teleop moved to Isaac Teleop). Wrap it behind an internal task-spec/adapter layer and pin versions per workspace.
- Licensing for multi-tenant SaaS: Isaac Sim/Kit binaries are under the proprietary Omniverse terms. Cloud-hosting rights for third-party users must be confirmed with NVIDIA, which is why a license-clean MuJoCo-Warp/mjlab/Newton backend should exist.
- Model and asset license contamination: GO-1 (CC BY-NC-SA), RLDX-1 (non-commercial), ManiSkill assets (CC BY-NC), MimicGen code (NVIDIA Source Code License), cuRobo (proprietary), Ultralytics (AGPL), BlenderProc (GPL-3.0), OpenVLA (Llama 2 terms), SAM License, unclear openpi weight terms. The
  platform needs automatic license tagging and gating.
- NVIDIA ecosystem lock-in (Isaac, GR00T, Cosmos, Jetson, TensorRT). Mitigate with Newton (Linux Foundation), MuJoCo-Warp, LeRobot format and ONNX export.
- Fast obsolescence: Cosmos-Predict2.5 and Transfer2.5 already superseded by Cosmos 3 within about 8 months; LeanRL archived; GR00T moved N1.5→N1.7 within about a year. Design model integrations as plugins.
- Benchmark saturation (LIBERO ~97–99%) can mislead customers. Needs harder suites (LIBERO-plus, RoboCasa365, BEHAVIOR-1K), customer-specific scenario suites and real-world validation.
- Sim2real gap remains largest for contact-rich dexterous work, deformables and vision. Camera-based RL is about 16x slower than state-based in Isaac Lab, so vision-policy jobs get expensive.
- GPU supply and cost: RT-core GPUs are needed for rendering while H100-class GPUs are needed for VLAs, so poor pool planning will waste capacity. Data-sovereignty demands from Korean customers may require on-prem deployments.
- Real-robot data and evaluation remain essential. Without partner labs or customer fleets, the flywheel (failure mining → re-simulation) cannot be closed.
- Information risk for this report: web search was exhausted and many vendor sites were blocked, so claims about Gemini Robotics, pi*0.6, Figure Helix, Genie 3, DreamerV4, Jetson Thor specs, cloud GPU prices and GTC/CoRL 2026 announcements are unverified (medium or low confidence).
## Open questions
- What are the exact Omniverse/Isaac Sim license terms (and cost) for hosting Isaac Sim-based training for third-party users in a multi-tenant cloud (CEN)? Is an Omniverse Enterprise or OVX agreement required?
- What license covers the openpi checkpoints (pi0/pi0.5 base weights) for commercial fine-tuning and redistribution of fine-tuned weights?
- Is there a GR00T N2 or DreamZero public release (referenced by Isaac Lab Arena and RLinf), and what are its license and compute needs?
- What is the current state (Oct 2026) of Gemini Robotics: any 2.x models, API availability for VLA fine-tuning, and pricing? Not verifiable here (deepmind.google blocked).
- Did Physical Intelligence open-source any pi0.6 / pi*0.6 / RECAP components in 2026?
- What did GTC 2026 (March), SIGGRAPH 2026, RSS 2026, ICRA 2026 and CoRL 2026 announce beyond what GitHub releases show (Isaac Lab 3.0 beta in GTC week, Cosmos 3 in May/June 2026)? Web search was exhausted, so this needs a follow-up search.
- What are the exact Jetson AGX Thor / T4000 specs and 2026 pricing, and measured GR00T N1.7 / pi0.5 inference latency on Thor?
- What do H100/H200/B200 and L40S/RTX PRO 6000 GPU-hours cost from Korean clouds (Naver Cloud, KT, NHN) versus global neoclouds in 2026, and are there national GPU-support programs AICHEMIST qualifies for?
- Which Korean physical-AI programs (e.g., K-Humanoid Alliance, government Physical AI initiatives, Samsung/Rainbow Robotics, LG, NAVER LABS) could be data or compute partners? Only RLWRLD RLDX-1 was verified here.
- What is Isaac Lab 3.0 GA's final API surface and its performance with Newton versus PhysX on contact-rich manipulation (to decide default backend per task class)?


# TOPIC: market_competition
## Executive summary
RESEARCH CAVEAT: the shared web-search budget for this run was already used up (0 of the planned 15+ searches ran), and the egress proxy blocked every news, analyst, vendor and Korean media domain tried (nvidianews, appliedintuition, marketsandmarkets, globenewswire, prnewswire, techcrunch,
  wikipedia, arxiv, huggingface, etnews, morai.ai, dart.fss.or.kr). Only github.com and pypi.org could be fetched. Facts checked there are marked HIGH confidence. Market sizes, funding rounds and incumbent M&A come from the model's prior knowledge and are marked MEDIUM (well-known events up to 2025)
  or LOW (2026 events, prices, small companies); every one of these should be checked again before it goes into a board deck. (1) Market size: analysts put digital twins at roughly USD 21-25B in 2024/25, growing 34-48% a year to about USD 150B by 2030 (MarketsandMarkets, Grand View). Estimates
  differ by 3-10x because firms define the scope differently (IIoT, PLM, BIM). The narrower markets are much smaller: synthetic-data tools are about USD 0.3-0.6B (35-46% CAGR), and robotics or AV simulation software is about USD 1-3B each (low confidence). (2) Where the money goes: private capital
  is flowing to autonomy stacks and robot foundation models, not to standalone simulators. Examples are Applied Intuition (USD 15B, Jun 2025), Figure (USD 39B, Sep 2025), Physical Intelligence (USD 5.6B, Nov 2025), a reported Skild AI round at about USD 14B (Jan 2026, low), Field AI (USD 2B) and
  Genesis AI (USD 105M seed). For these firms the simulator is an internal tool or a data engine, not the product. (3) NVIDIA is turning the simulation layer into a free commodity, and this is verified on GitHub. The Isaac Sim repo is Apache-2.0, but the PyPI runtime is NVIDIA Proprietary; the
  latest stable is 6.1.0 (Sep 10, 2026), with 7.0 alpha out Sep 18, 2026. Isaac Lab 3.0 (beta at GTC on Mar 17, 2026) supports several physics backends (PhysX plus Newton/MuJoCo-Warp) and can run without Omniverse Kit. Newton 1.0 shipped Apr 13, 2026 under the Linux Foundation, co-founded with
  DeepMind and Disney. GR00T N1.7 has open weights, Cosmos 2.5 code is Apache-2.0, and NVIDIA now even automates SimReady asset authoring (usd-content-agents, Apache-2.0). Building your own physics engine or generic simulator is therefore not defensible. The value sits in workflow, data, assets,
  vertical scenarios, evaluation and sovereign deployment. (4) Incumbents and AV simulation: the industrial vendors (Siemens with Altair, Synopsys with Ansys, Dassault, PTC, Bentley with Cesium, AVEVA, Cognite) own engineering and operations twins sold per seat or by enterprise license, and they
  bolt on NVIDIA for rendering and AI. None of them produces policies that can learn from the twin, and the gap between a PLM twin and a learnable simulator is the largest white space. The hyperscalers have stepped back from generic twin PaaS: Microsoft Fabric digital twin builder was still in
  preview in May 2026 and is separate from Azure Digital Twins, and the AWS IoT TwinMaker status is unverified. AV simulation is crowded (Applied Intuition, Foretellix, dSPACE, IPG, Siemens Prescan, Ansys, rFpro, Cognata, free CARLA on UE5.5, MORAI in Korea), and neural/world-model simulation (Waabi
  World, Wayve GAIA, Cosmos) is overtaking hand-built scenes, so a generic AV-sim entry would be late. Synthetic-data specialists (Parallel Domain, Rendered.ai, Bifrost, Duality) stayed small and survive mainly through defense and aerospace. (5) Korea: MORAI is the only scaled domestic simulator
  vendor (AV, UAM, maritime; GitHub active through Sep 2026). E8 (NDX PRO) and VIRNECT are listed but small industrial/urban twin players. NAVER LABS (ALIKE mapping, ARC robots, 60k-GPU NVIDIA deal) could be a partner or a competitor, and the chaebol IT-services arms build NVIDIA- or Siemens-based
  twins in house. Korean robot makers (Boston Dynamics/HMG, Rainbow/Samsung, Doosan Robotics, HD Hyundai Robotics, LG/Bear, Holiday, Aidin, RLWRLD) need training data and simulation but have thin RL/sim teams. Tailwinds include about 260k NVIDIA GPUs allocated to Korea (Oct 2025), HMG's roughly USD
  3B physical-AI cluster, the K-Humanoid Alliance, the AI Basic Act (in force Jan 2026) and MASGA-driven shipyard automation. (6) Most defensible positions for AICHEMIST: (a) a sovereign, NVIDIA-compatible physical-AI data factory for Korean conglomerates; (b) a shipbuilding and heavy-industry
  vertical twin with robot-policy training; (c) air-gapped defense sensor synthetic data; (d) Real2Sim assets with measured physics and commercial licences, sold through the CEN marketplace; (e) a neutral policy-evaluation and benchmark service for Korean humanoids. Pricing would be hybrid:
  subscription, GPU-hour metering, data packs, on-prem licence and NRE.
## Recommendations
- Adopt and extend; do not build an engine. Standardize on OpenUSD plus Isaac Lab 3.x multi-backend (PhysX + Newton/MuJoCo-Warp), with URDF/MJCF/USD round-trip (Lightwheel's mjcf2usd/usd2mjcf show the need). Keep Genesis as an optional backend for deformables and fluids. Newton 1.x (Apache-2.0,
  Linux Foundation) and MuJoCo 3.15 already provide the physics, and NVIDIA is shipping Kit-less ovphysx/ovrtx libraries that can be embedded. Put engineering into the parts AICHEMIST can own: LLM-driven scene and task authoring, data-generation pipelines, Real2Sim assets, vertical scenario
  libraries, evaluation, and sovereign/on-prem packaging.
- Sell outcomes, not simulator seats. Productize a 'Physical-AI Data Factory'. Input: CAD/BIM/photos plus 10-100 teleop demos. Output: a validated SimReady twin, synthetic multimodal datasets (RGB-D, segmentation, LiDAR, tactile), fine-tuned policies (GR00T N1.7 / pi0.5 bases) and an evaluation
  report. The synthetic-data tools market (~USD 0.3-0.6B) is too small to win on tooling alone.
- Lead with one or two verticals where Korea has unique demand and data. First, shipbuilding and heavy industry (HD Hyundai/HD Hyundai Robotics, Hanwha Ocean, Samsung Heavy): welding, painting, block logistics, crane and humanoid tasks, boosted by MASGA. Second, factory and logistics manipulation
  for Korean robot makers (Doosan Robotics, already on Isaac/cuRobo; Rainbow/Samsung; LG/Bear) and for CJ Logistics and Coupang. Deprioritize generic AV simulation (Applied Intuition, MORAI, NVIDIA blueprints and world models already cover it) and partner with MORAI instead.
- Add a separate air-gapped defense SKU: EO/IR/SAR/radar synthetic data and drone/UGV training twins for ADD, Hanwha Aerospace, LIG Nex1 and KAI. Use Bifrost and Duality as the reference business model. Expect long cycles, so run it as a second-wave line with security certification planned early.
- Build a Real2Sim asset moat on CEN's NeRF/3DGS pipeline. Add physical-parameter identification (mass, friction, articulation and joint limits from video plus a small in-house measurement rig), publish USD+MJCF+URDF with validation certificates, and license commercially. That contrasts with
  ManiSkill's CC BY-NC assets and Lightwheel's non-commercial free set. Benchmark against and integrate NVIDIA usd-content-agents rather than rebuilding generic auto-annotation. Differentiate on measured physics and Korean/Asian industrial and household SKUs.
- Become the neutral measurement layer. Launch a 'K-Physical AI Arena' that pairs a simulation benchmark with real test cells, standardized for K-Humanoid Alliance members, ideally with KIRIA/KTL. Evaluation is sticky, regulator-friendly under the AI Basic Act, and hard for a single OEM or NVIDIA to
  own.
- Ride the sovereign-GPU wave. Deploy CEN's workspace on Korean sovereign clouds that received Blackwell allocations (NAVER Cloud, KT, NHN, Samsung SDS) and offer an on-prem appliance for chaebol fabs, shipyards and defense. Join NVIDIA Inception and the Omniverse/Isaac partner programme and co-sell
  with NVIDIA Korea into the HMG, Samsung, SK and Naver physical-AI programmes.
- Partner with incumbents rather than fight them. Ship connectors from Siemens Process Simulate/Teamcenter, Dassault CATIA/DELMIA, AVEVA Marine and Autodesk Revit/BIM to USD training environments, and market the result as 'the AI training layer for your existing PLM twin'. Use group IT-services arms
  (Samsung SDS, LG CNS, Hyundai AutoEver, HD Hyundai IT) as resellers to get through procurement.
- Integrate world-model augmentation (Cosmos Transfer2.5-class) for photoreal variation on top of physics ground truth, and report downstream task metrics (sim-to-real success-rate delta, mAP delta) to prove fidelity. This answers the main customer pain point: there is no proof that synthetic data
  is good enough.
- Pricing (hybrid, anchored to public comps): (a) workspace subscription per seat, referencing the ~USD 1,850/seat/yr Unreal enterprise price point; (b) GPU-hour metering on RT-core GPUs (L40S / RTX PRO 6000) at a 30-60% margin over cloud cost; (c) data and scenario packs, plus per-task policy-
  training packages; (d) on-prem enterprise licence (indicatively KRW 0.3-1.5B per year), referencing NVIDIA's ~USD 4,500/GPU/yr enterprise list price; (e) NRE for co-development. Target 2-3 paid PoCs of KRW 200-500M each in 2026-27 with HD Hyundai, Doosan or Rainbow, and one defense prime, and use
  MSIT/MOTIE physical-AI and K-Humanoid programmes for non-dilutive funding.
- Watch-list triggers that should prompt a strategy review: NVIDIA productizing SimReady/content agents or a managed Isaac cloud in Korea; Lightwheel or Applied Intuition opening Korean sales; Chinese data factories (AgiBot, Manycore) pricing assets near zero; HMG/Samsung announcing in-house data
  factories; world models reaching controllable physics.
## Risks
- Platform commoditization by NVIDIA: Isaac Sim/Lab, Newton, Cosmos, GR00T and even SimReady asset agents are free or open. Any generic platform or asset feature can be matched by NVIDIA within months, and the proprietary Isaac Sim runtime licence (PyPI) also limits how freely AICHEMIST can
  redistribute on-prem.
- Market-size illusion: digital-twin forecasts vary 3-10x by scope, and the synthetic-data tools market is only ~USD 0.3-0.6B. Investors and the CEO should not size the opportunity from top-line digital-twin numbers.
- Customer in-housing: leading autonomy and robotics firms (Waabi, Wayve, Figure, Skild, Tesla, HMG/42dot) build simulation internally. Chaebol IT-services arms may capture projects after AICHEMIST's PoC.
- Long enterprise and defense sales cycles (12-24+ months) and procurement bias toward global brands (Siemens, Dassault, NVIDIA) strain a startup's runway.
- World-model disruption: generative simulators may reduce the value of hand-authored assets and scenes. Mitigate by owning physics ground truth, evaluation and data rights.
- GPU economics: Isaac rendering needs RT-core GPUs (L40S / RTX PRO), not H100, and GPU-hour margins compress as cloud prices fall.
- Fast-moving APIs: Isaac Lab 3.0's breaking changes and monthly Newton/MuJoCo releases create a heavy maintenance burden for a small team.
- Competition for scarce Korean talent in USD, RL and sim-to-real against Samsung, HMG, Naver and global labs.
- Fidelity liability: if synthetic data or sim-validated policies fail in the field (shipyard or defense), reputational and contractual exposure is high without validated metrics.
- Geopolitics and compliance: export controls, US connected-vehicle rules and defense security requirements. Chinese low-cost competitors put pressure on generic asset and data pricing.
- Verification gap in this report: most market and funding figures could not be re-checked this session (search budget exhausted, domains blocked), so decisions should not rest on them until they are verified.
## Open questions
- What exactly did NVIDIA announce at GTC 2026 (Mar 16-19), Computex 2026 and SIGGRAPH 2026 for Isaac, Newton, Cosmos and Omniverse (e.g., managed cloud offerings, SimReady marketplace, pricing changes)? Only the GitHub release dates were verified.
- Current (2026) funding and valuation for Skild AI, Wayve, Waabi, 1X, Physical Intelligence, Lightwheel, Hillbot, Duality, Bifrost, Rendered.ai and Foretellix.
- Is AWS IoT TwinMaker still open to new customers, and has Microsoft announced any Azure Digital Twins retirement or a migration path to Fabric?
- Updated analyst figures (2025/2026 editions) for robotics simulation, AV simulation and synthetic data, so the dispersion can be quantified properly.
- MORAI's latest funding round, revenue, IPO plans and physical-AI/robotics roadmap; whether it would partner or compete.
- Financials (2025 DART filings) for E8 (NDX PRO) and VIRNECT; identity and relevance of 'Danusys' and '에이딕', which could not be checked.
- Which simulation stacks HMG/Boston Dynamics, Samsung/Rainbow, LG, HD Hyundai and Hanwha use internally, and their budgets for synthetic and robot-training data in 2026-27.
- Korean government 2026-2027 budget lines for physical AI, the K-Humanoid Alliance and defense synthetic data, and the procurement routes AICHEMIST can use.
- Willingness of Korean shipbuilders and defense primes to share CAD, process and sensor data, or to require fully on-prem deployment.
- Public pricing points for Applied Intuition, Lightwheel assets, Duality Falcon and NVIDIA's latest Omniverse/AI Enterprise licences in 2026.


# TOPIC: korea_policy
## Executive summary
VERIFICATION LIMIT: I could not check anything on the web in this run. The first WebSearch call came back with 'web search budget is used up (200 calls per turn, shared by every agent)'. WebFetch to primary sources (nvidianews.nvidia.com, korea.kr, msit.go.kr) was blocked by the egress proxy.
  Everything below therefore comes from model knowledge, which is solid through 2025 and patchy for H1 2026. Nothing from after mid-2026 is covered, including the 2027 budget proposal published around late Aug/Sep 2026. Every item carries a confidence level, and decision-critical numbers must be re-
  checked on IRIS, K-Startup, NIPA and the MSIT/MOTIE press pages before any proposal is written.

The policy direction is very favorable. In the 2026 budget, the AI line roughly tripled to about KRW 10.1T (from about 3.3T in 2025). National R&D went to a record of about KRW 35.3T in the proposal, and the total budget of about KRW 727.9T passed on 2 Dec 2025. The AI Basic Act took effect on 22
  Jan 2026. The 'AI highway / sovereign AI' agenda and the Aug 2025 growth strategy name physical AI (robots/humanoids, autonomous vehicles, shipbuilding, drones, AI factories) as the main way to apply AI across industry.

The Oct 31, 2025 NVIDIA–Korea deal covers 260k+ Blackwell GPUs: about 50k for government, 50k each for Samsung, SK and Hyundai Motor Group, and 60k for Naver Cloud. Most of the commercial share is earmarked for physical AI and digital twins: Samsung's Omniverse 'AI Megafactory', Hyundai's roughly
  USD 3B physical-AI cluster, and SK's manufacturing AI cloud. So AICHEMIST's buyers are building Omniverse/Isaac-based twins right now. Those chaebol may also build in-house, which makes them both the best reference customers and the main substitution risk.

The best-fit role for AICHEMIST is not prime contractor on trillion-won national programs. It should be the 'simulation + synthetic-data + robot-learning infrastructure' supplier inside chaebol- or institute-led consortia:
- K-Humanoid Alliance / KEIT robot R&D
- the MOTIE M.AX alliance and AI-factory projects
- IITP physical-AI and digital-twin R&D
- the autonomous-driving R&D program
- NIA data-construction projects

Startup-only instruments should fund the core platform itself: Deep-tech TIPS (up to about KRW 1.5B of R&D over 3 years), Super-Gap Startup 1000+ (up to about KRW 0.6B over 3 years), and SME R&D. Vouchers (NIPA AI Voucher and the K-DATA Data Voucher) are the fastest route to subsidized revenue and
  paying references, because the government pays AICHEMIST to serve SMEs and mid-caps.

Compute: government GPU allocations so far are training GPUs (B200/H200 from the about 13k-GPU pool run by NHN, Naver and Kakao). These have no RT cores, so they cannot run Omniverse/Isaac RTX sensor rendering. The plan should therefore use public B200/H200 for VLA, perception and RL training, and
  get RTX-class capacity (RTX PRO 6000 Blackwell / L40S) through domestic cloud providers or Hyundai/SK/Naver physical-AI clouds.

Realistic non-dilutive intake over Q4 2026–2027, if 4–6 applications succeed, is about KRW 3–6B (my estimate, not a sourced figure), plus in-kind GPUs. Most of the 2026 calls have closed. The decisive window is Dec 2026–Apr 2027, when the yearly unified announcements come out.

Overseas sequence:
1. Lock in 2–3 named Korean references: one automotive or robot OEM, one AI-factory, one shipyard or defense customer.
2. Get certified and enter the NVIDIA ecosystem: GS certification, a TTA test report, Inception and Omniverse partner listing.
3. Japan first: labor-shortage automation, AIRoA robot-data consortium, and Japanese plants of Korean suppliers.
4. The US, by following Korean OEMs' US plants (HMGMA Georgia, Samsung Taylor, Hanwha Philly Shipyard under the USD 150B MASGA shipbuilding package), plus a self-serve SaaS for US robotics startups.
5. The Middle East through G2G smart-city and defense deals, following the precedent of Naver's Saudi 5-city digital-twin contract.

The key risks are:
- NVIDIA commoditizing the stack: Isaac Sim/Lab are open source, and Cosmos and the Omniverse Blueprints are free.
- Domestic competitors: MORAI in AV simulation, CyLab and E8 in synthetic data and digital twins.
- Dependence on the policy cycle and the burden of matching funds.
- Consortium IP and royalty terms, and the cap on how many concurrent projects one researcher may hold.

If the CEO funds one action now, it should be a single 'Korean physical-AI sim/data infrastructure' proposal kit with common KPIs (TRL 4→7, sim-to-real gap, synthetic-to-real mAP ratio, throughput), reused across TIPS, the vouchers and the consortia.
## Recommendations
- TOP TARGET 1 – Deep-tech TIPS. Size: up to about KRW 1.5B of R&D over 3 years, plus at least about KRW 0.3B of operator equity. Timing: recommendation is rolling; aim to secure an operator (a deep-tech AC/VC, ideally one that also has robotics or automotive LPs) in Q4 2026 and submit in Q1 2027.
  Scope: 'physics- and sensor-fidelity sim + synthetic-data engine + robot-learning pipeline'. This funds the core platform.
- TOP TARGET 2 – Super-Gap Startup 1000+. Size: up to about KRW 0.6B over 3 years. Timing: expected call around Feb–Mar 2027. Apply under the big data/AI field (or robotics if the humanoid/robot-learning angle is stronger). Use its global track for the Japan/US launch.
- TOP TARGET 3 – NIPA AI Voucher, as supplier. Size: about KRW 0.2–0.3B per voucher; target 3–5 vouchers, worth about KRW 0.6–1.5B. Timing: register as a supplier and line up demand companies (SME factories, AMR/logistics robot makers, inspection users) in Dec 2026; the call runs around Jan–Mar
  2027. Every voucher should end with a named reference and a measured synthetic-to-real result.
- TOP TARGET 4 – K-DATA Data Voucher, as synthetic-data supplier. Size: up to about KRW 70M per task; target 5–10 tasks, worth about KRW 0.35–0.7B. Timing: supplier registration around Dec 2026–Jan 2027. These are low-effort recurring wins that also seed the CEN marketplace.
- TOP TARGET 5 – Government GPU allocations (MSIT/NIPA advanced-GPU program; plus AICA Gwangju and KISTI). These are in kind. Ask for B200/H200 time for VLA, perception and RL training. Do not plan RTX sensor rendering on these GPUs, because they lack RT cores. Get RTX PRO 6000 / L40S capacity
  separately: domestic cloud providers, NVIDIA Inception preferred pricing, and Hyundai/SK/Naver physical-AI clouds.
- TOP TARGET 6 – K-Humanoid Alliance plus MOTIE/KEIT robot R&D. Join as a member now. Pitch a 'simulation and synthetic-demonstration data factory' work package for the robot-foundation-model effort, serving Rainbow Robotics/Samsung, Doosan, LG and others. Expected sub-award: about KRW 0.3–1B per
  year (estimate). Calls come around Q1–Q2 2027.
- TOP TARGET 7 – MOTIE M.AX Alliance / AI-factory lighthouse projects, as the digital-twin and synthetic-vision supplier to one lead manufacturer (automotive tier-1, battery, or electronics). Expected size: about KRW 0.3–3B per project (estimate). Timing: rolling through 2026–2027. Partner with an
  integrator (LG CNS, SK AX, Samsung SDS, Doosan Digital Innovation) rather than competing with it.
- TOP TARGET 8 – MSIT/IITP physical-AI, digital-twin and synthetic-data R&D as co-performer with ETRI, KAIST or SNU. Expected share: about KRW 0.2–1B per year over 3–5 years. Timing: new tasks Jan–Apr 2027 on IRIS. Use it for frontier pieces (sensor physics, world models / Cosmos-style augmentation,
  LLM-to-scene generation) without paying for them alone.
- TOP TARGET 9 – NIA AI training-data construction, as lead or member of a physical-AI / robot-manipulation synthetic dataset consortium. Size: about KRW 1–5B per consortium per year. Timing: around Q1–Q2 2027. Accept the open-data condition in exchange for scale and visibility; keep the generators
  proprietary.
- TOP TARGET 10 – Defense synthetic data and M&S: DAPA innovative-SME program, rapid prototyping, defense AI data projects. Size: tens of KRW billions at program level. Timing: plan for 2027 H2. Prerequisites: an on-prem or air-gapped CEN edition, and avoiding non-exportable components.
- TOP TARGET 11 – Mobility follow-on. Supply synthetic sensor data and scenario validation to remaining 2021–2027 AV program tasks, and position for the post-2027 successor program and for K-City digital-twin upgrades. Do not fight MORAI head-on; partner with it or specialize in perception data and
  sensor realism.
- TOP TARGET 12 – Global programs. Join NVIDIA Inception immediately (free) and apply for the Omniverse/Isaac ecosystem listing. Use KIAT international joint R&D (about a few hundred million KRW per year) with one Japanese partner and one US partner. Use the Export Voucher (up to about KRW 100M per
  year) for GTC, iREX Tokyo, Automatica and CES, and NIPA KIC Silicon Valley / KISED KSC for US landing.
- Eligibility and paperwork, Q4 2026: establish a KOITA-recognized corporate R&D lab, venture certification, and IRIS and SMTECH accounts. Plan around the 3책5공 limit on concurrent projects per researcher, and draft a module-by-module duplication map so one platform is not double-funded. Start GS
  certification (TTA) for a frozen CEN release. Start ISO 27001, and CSAP if public SaaS sales are planned.
- Proposal kit and KPI template, reusable across programs: TRL from 4 to 7. Sim-to-real policy success gap of at most 10 percentage points on 3 robot tasks. A synthetic-only-trained detector reaching at least 90–95% of real-data mAP, and synthetic plus 10% real data at least matching 100% real.
  Sensor-model error, e.g. LiDAR range error of at most 2 cm and camera ISP/noise matched on a calibration chart. Throughput of at least N thousand labeled frames per GPU-hour, and parallel RL environments of at least 4,096 per GPU. Real-time factor of at least 1.0 for a multi-robot factory scene.
  Third-party test reports (TTA/KTL/KOLAS) for 3+ indicators. Commercial KPIs: paying customers, revenue, export contracts, patents (filed and registered), papers (CoRL/ICRA/RSS), hires.
- Typical Korean R&D scoring to design for (approximate; varies by agency): technical merit and novelty about 40–60, commercialization plan and market about 20–40, team capability and infrastructure about 20. Bonuses exist for job creation, standards contribution, international collaboration, and
  prior TIPS/venture status. Written review is followed by a presentation; a score of about 70+ is commonly the cutoff. Show demand-side letters of intent (LOIs) from Hyundai, Samsung, SK, HD Hyundai or a robot OEM, plus measurable, third-party-verifiable KPIs.
- Sequencing domestic wins into overseas sales. Phase 1 (2026 Q4 – 2027 H1): vouchers plus one chaebol or robot-OEM PoC, published as quantified case studies. Phase 2 (2027 H2): GS certification, NVIDIA ecosystem listing, a public benchmark (sim-to-real or synthetic-to-real), and a Japan PoC via
  KIAT/KOTRA or a Korean supplier's Japanese customer. Phase 3 (2028): a US entity, following Korean OEMs into HMGMA Georgia, Samsung Taylor and Hanwha Philly (MASGA), plus a self-serve CEN tier for US robotics startups. Middle East via G2G smart-city and defense packages with a Korean prime.
- Architectural implication of the policy environment: build CEN on the open NVIDIA stack (Isaac Sim/Lab, Newton or MuJoCo-Warp, Cosmos, OpenUSD) rather than a proprietary engine. Government and chaebol buyers are standardizing on it, so compatibility is a scored and procurement advantage.
  Differentiate on Korean-domain assets and data (factories, shipyards, Korean roads and signage), sensor-fidelity calibration, LLM-driven scene control and the marketplace, which NVIDIA does not provide.
- Immediate verification to-dos (blocked in this run): the 2027 budget proposal (published around late Aug 2026) lines for physical AI, AI factory, humanoid and GPU programs; 2026–2027 GPU allocation rules and whether RTX PRO GPUs are included; the existence, scope and membership of any 'Physical AI
  Global Alliance'; IITP/KEIT 2026 physical-AI new-task lists on IRIS; 2026 caps for the Data Voucher and AI Voucher; 2026 TIPS and Super-Gap reforms; the National AI Computing Center schedule; GTC 2026 Korea announcements.
## Risks
- Verification risk: every number here is from model knowledge with no 2026 web confirmation (search budget exhausted, fetch egress blocked). Program caps, call dates and the 2027 budget must be re-checked before committing proposal effort.
- Policy-cycle risk: Korean R&D budgets swing sharply (2024's about 15% cut, then the 2026 surge). Physical-AI programs announced in 2025–2026 could be reorganized, delayed or merged after the 2027 budget review.
- Chaebol in-house substitution: Samsung, SK, Hyundai and Naver are building their own Omniverse-based twins directly with NVIDIA (260k-GPU deal). AICHEMIST could be confined to low-margin data-contractor work unless it owns a differentiated layer (sensor fidelity, Korean-domain assets, LLM scene
  control, marketplace).
- NVIDIA commoditization: open-source Isaac Sim/Lab, free Omniverse Blueprints (factory, AV), Cosmos WFMs and NVIDIA's own synthetic-data workflows lower barriers for every competitor and for customers' in-house teams.
- Domestic competition: MORAI (AV sim), CyLab/씨이랩 (synthetic data), E8 (digital-twin platform), plus large SIs (Samsung SDS, LG CNS, SK AX) that win prime roles.
- Compute mismatch: public GPU allocations are mostly B200/H200 with no RT cores, so they are unusable for RTX sensor rendering. Self-funded RTX capacity can dominate burn.
- Matching-fund and cash-flow burden: a 25%+ private share, cash contributions, delayed grant disbursement, and post-project royalty (기술료) obligations can strain a startup's runway.
- IP and consortium terms: results of national R&D generally belong to the performing organization, but consortium agreements, open-data conditions (NIA) and defense rules can restrict reuse in CEN commercial products.
- Researcher concurrency (3책5공) and duplication review: the same platform modules cannot be funded twice, and key engineers are capped on concurrent projects.
- Regulatory: AI Basic Act obligations (effective Jan 2026) for high-impact AI, transparency and labeling of generated content; privacy rules for real-data marketplace items (PIPC); defense security; US export controls on advanced GPUs or software when serving the Middle East or China-adjacent
  customers.
- Overseas execution: long Japanese enterprise sales cycles, US competition (Applied Intuition, Duality, Parallel Domain, Bifrost and others), local-partner requirements in the Middle East, and FX exposure.
- Over-dependence on vouchers: voucher revenue is subsidized, small-ticket and annual. Investors may discount it unless it converts into recurring subscriptions.
## Open questions
- What does the 2027 government budget proposal (published around late Aug–Sep 2026) allocate to physical AI, AI factory/M.AX, humanoids, the GPU 'AI highway' and data vouchers? This could not be retrieved in this run.
- Does a 'Physical AI Global Alliance' (피지컬AI 글로벌 얼라이언스) exist under that name, who leads it (MSIT or MOTIE), and can startups join?
- What are the 2026–2027 rules for public GPU allocation: application windows, per-startup caps, cost share, and whether RTX PRO 6000 / L40S rendering-capable GPUs are included in the government's ~50k Blackwell share?
- What is the National AI Computing Center's current timeline and startup access model (pricing, quotas)?
- Which 2026–2027 IITP/KEIT new tasks explicitly cover simulation, synthetic data, world models or robot-data factories (task titles and budgets on IRIS)?
- Has the K-Humanoid Alliance already chosen its robot-foundation-model prime and data/sim partners, and are work packages still open?
- What are the 2026 caps and tracks for the AI Voucher and Data Voucher? Is there a physical-AI or synthetic-data track?
- Were TIPS, Deep-tech TIPS or Super-Gap 1000+ restructured in 2026 (for example scale-up TIPS caps or new global tracks)?
- What did GTC 2026, SIGGRAPH 2026 and NVIDIA AI Day Seoul announce for Korea-specific startup or physical-AI programs (for example an Inception Korea expansion or Omniverse partner programs)?
- AICHEMIST's eligibility facts: founding date (under 7 or under 10 years), headcount, existing R&D lab and venture certification, prior national R&D record, and current investors. Is there a TIPS operator relationship?
- What is the status of the Hyundai, SK and Naver physical-AI clouds? Will they host third-party ISV platforms like CEN, and on what revenue-share terms?


# TOPIC: build_vs_buy
## Executive summary
Recommendation: choose Strategy D, a hybrid. Use an open, vendor-neutral physics and training core: Newton 1.6.1 (Apache-2.0, Linux Foundation, PyPI status "Production/Stable"), MuJoCo 3.15 and MuJoCo-Warp (Apache-2.0), and Isaac Lab 3.0 (BSD-3) in its new kit-less mode. Add NVIDIA's RTX sensor
  rendering (Isaac Sim 6.1 / Omniverse Kit / ovrtx) only where photoreal or physically based camera, lidar and radar output earns its cost. Put AICHEMIST's own differentiation in the platform layer: CEN orchestration, multi-tenancy, LLM scene control, NeRF/3DGS-to-SimReady asset pipeline,
  marketplace, and data/training services. Weighted decision-matrix scores (1-5): D 4.23, B (Isaac/Omniverse-centric) 3.70, C (open multi-engine + UE5/web) 3.20, A (build our own engine) 2.40. Strategy A should be ruled out. History shows how long an engine takes even for well-funded groups. MuJoCo
  was developed by Roboti LLC for about a decade before DeepMind acquired it in Oct 2021 and open-sourced it in May 2022. Newton needed NVIDIA, Google DeepMind and Disney Research plus a decade of Warp/MuJoCo code to go from its March 2025 announcement to 1.0 on PyPI on 2026-03-10. Genesis went from
  academic project to company-backed 1.0 in May 2026. Chrono (20k commits) and Drake (35k commits) are multi-decade efforts. A competitive in-house physics engine plus renderer would realistically need 40-80 scarce specialists for 3-5 years (about ₩400-600억). It would then compete with free, fast-
  moving engines. The main licensing trap: Isaac Sim's 'Apache-2.0' covers only the repository source. The Kit SDK, RTX renderer and 3D assets come under a separate NVIDIA 'Isaac Sim Additional Software and Materials License', and the isaacsim PyPI package is classified 'Other/Proprietary'. The kit-
  less RTX renderer ovrtx 0.5.1 is 'LicenseRef-NvidiaProprietary' and alpha; ovphysx 0.6.3 is 'LicenseRef-NVIDIA-Omniverse' and alpha. Kit apps fall under the NVIDIA Software License Agreement plus Omniverse product-specific terms, and Kit collects anonymous telemetry. Hosting these components for
  paying third parties in a multi-tenant cloud, shipping them on-prem, and reselling NVIDIA assets in the CEN marketplace each need written confirmation from NVIDIA before launch. Isaac Sim streaming has no authentication or encryption and needs host networking, so AICHEMIST must build its own
  secure streaming gateway. Hardware: RTX rendering needs RT-core GPUs. Isaac Sim lists A40 as the datacenter minimum, L40S/L20 as recommended and RTX PRO 6000 Blackwell Server as best; H100/H200/B200 lack RT cores and belong in the physics-only RL and VLA/foundation-model training pool. Live GPU
  prices (SkyPilot catalog, 2026-10-05/06): H100 $6.88/GPU-h on AWS p5 vs $2.89-4.29 on RunPod/Lambda. L40S $1.86 on AWS g6e.xlarge vs $1.09 on RunPod. RTX PRO 6000 $3.36 on AWS g7e.2xlarge and about $4.50 on GCP G4 (spot about $1.71). B200 $11.28 on GCP and $14.24 on AWS vs $6.69 on Lambda. AWS/GCP
  Seoul regions cost 23-38% more than US regions. Unit costs: GPU-parallel RL physics is cheap at about $1-10 per 1B env-steps without cameras and $8-30 with one camera in the loop (from Isaac Lab's own benchmarks). Synthetic images cost about $5-60 per 1M rasterized 1080p frames, $20-250 with RTX
  real-time ray tracing, and $300-5,000 path-traced. Storage and egress (about $126/month and about $495 egress per 1M multimodal frames) can exceed raster compute, so pricing tokens per image needs a storage/egress component. Full AV sensor-rig simulation runs about $3-15 per sim-hour. People
  dominate cost. Mid-case 24-month totals including compute: lean 12 ≈ ₩50억 ($3.5M), standard 25 ≈ ₩103억 ($7.4M), aggressive 45 ≈ ₩208억 ($14.9M). Ramped hiring cuts these by about 20%; Strategy D with ramped hiring (12→25) is about ₩80억. Time-to-MVP: B 3-5 months, D 4-6 months (Phase 0 rides on
  Isaac Sim), C 9-15 months, A 30-48+ months. Caveat: the shared web-search budget was exhausted before this agent's first query, and most vendor sites (nvidia.com, unrealengine.com, unity.com, Korean clouds, salary sites) were blocked by the egress proxy. Facts were therefore verified through
  GitHub, PyPI and the SkyPilot price catalog. UE/Unity/Omniverse Enterprise prices, Korean cloud prices and KRW salaries are marked low/medium confidence and must be confirmed with vendors and recruiters.
## Recommendations
- Adopt Strategy D (hybrid), which scores 4.23 vs 3.70 (B), 3.20 (C) and 2.40 (A). Do not build a physics engine or path tracer in-house. The evidence: MuJoCo took a decade-plus under Roboti and then DeepMind; Newton needed three large organizations plus prior code to reach 1.0 in March 2026;
  Genesis needed a VC-backed company to reach 1.0 in May 2026. A Korean startup cannot out-iterate engines that ship every 2-3 weeks for free.
- Architecture: (1) Physics core: Newton 1.6.x with MuJoCo-Warp as the primary solver, plus VBD/MPM for deformables and cloth. Keep MuJoCo C and MJX as the CPU/JAX reference, PhysX 5 (BSD-3) for vehicle parity, and Chrono (BSD-3) for off-road/terramechanics and ships. (2) Training: Isaac Lab 3.x in
  kit-less mode, plus LeRobot-style imitation-learning pipelines and VLA fine-tuning on H100/B200 pools. (3) Rendering behind a single 'Renderer API': tier 1 Newton GL / web viewer (WebGPU/3DGS, Rerun/Viser) for editing and RL debugging; tier 2 UE5 or rasterized Kit for bulk synthetic data; tier 3
  Isaac Sim 6.1 / ovrtx RTX for physically based camera/lidar/radar (premium); plus Cosmos 3 (OpenMDW-1.1) for appearance transfer. (4) Platform layer owned by AICHEMIST: OpenUSD scene graph, LLM scene compiler, NeRF/3DGS-to-SimReady asset physics estimation, domain-randomization engine, dataset
  versioning, CEN token billing and marketplace, multi-tenant K8s scheduler with separate RT-core and compute GPU pools.
- Phase 0 (months 0-6, lean 12): ship one vertical MVP, either robot-arm pick-and-place or AMR in a warehouse, because they reuse CEN's indoor SDG strengths. Use Isaac Sim 6.1 directly for photoreal SDG and Isaac Lab/Newton for RL. Exit criteria: 2-3 paid PoCs with Korean manufacturers or logistics
  firms, a sim-to-real transfer demo, and a per-image/per-step cost dashboard.
- Phase 1 (months 6-15, ramp to about 20-25): build the renderer abstraction and web viewer, a second vertical (AV/ADAS sensor simulation with CARLA content on UE5 or ovrtx, or mobile manipulators/humanoids), and the LLM scene control GA. Add an on-prem package for chaebol and sovereign customers.
  Phase 2 (months 15-24): multi-domain GA (vehicles, drones, ships via Chrono FSI), a marketplace of SimReady assets with physics parameters, and managed VLA fine-tuning.
- Budget: plan about ₩80-85억 ($5.8-6.0M) for 24 months on the ramped D plan (12 → 25 people). This covers people at a mid-case ₩1,495만 per head-month fully loaded, plus ₩8-12억 for compute. The aggressive 45-person plan (about ₩208억) is justified only if a large anchor customer or a Series B is
  secured. The lean 12-person plan (about ₩50억) cannot cover more than one or two verticals.
- Hiring priorities, in order: (1) a simulation architect or CTO with Isaac/MuJoCo/OpenUSD experience (consider Korean-American or remote hires); (2) two GPU physics engineers who can contribute upstream to Newton/MJWarp and earn credibility through Linux Foundation contributions; (3) two
  rendering/sensor engineers, recruitable from Korean game studios (Nexon, NCSoft, Krafton, Pearl Abyss) for real-time graphics; (4) two RL/VLA engineers; (5) a K8s GPU infra engineer; (6) two web-3D/platform engineers. Retain them with stock options because senior specialist salaries are
  ₩1.2-1.8억+.
- Licensing actions before any paid hosted launch: get NVIDIA's written confirmation (via NVIDIA Korea / Inception) that the Isaac Sim Additional Software license, the Omniverse product-specific terms and the ovrtx 'AI Products' terms allow (a) multi-tenant hosted SaaS for third parties, (b)
  container redistribution for on-prem, (c) resale or bundling of NVIDIA assets in the CEN marketplace, and (d) disabling or controlling telemetry. Budget about $4,500/GPU/yr for Omniverse Enterprise only if NVIDIA requires it. Keep the training path free of proprietary dependencies so a licensing
  change can only affect the premium rendering tier.
- Avoid asset-licensing contamination in the marketplace: build an asset provenance registry. Track CARLA assets as CC-BY with attribution in derived datasets, NVIDIA/Isaac assets as proprietary, UE Fab/Megascans as engine- and AI-use restricted (verify), and MuJoCo Menagerie and vendor robot models
  with per-model licenses. Sell only assets with clear rights, and attach a license manifest to every synthetic dataset.
- GPU procurement: split pools. Use RT-core GPUs for rendering: RTX PRO 6000 Blackwell (AWS g7e $3.36/h, GCP G4 $4.50/h, spot $1.71) or L40S (RunPod $1.09, AWS $1.86). Use H100/H200/B200 for training (Lambda $3.99/GPU-h for 8×H100; RunPod $2.89-3.49) and use spot for batch SDG (50-65% cheaper).
  Avoid Seoul hyperscaler regions for non-sensitive batch work (+23-38%). Use Korean CSAP-certified clouds (NHN/KT/Naver) for public-sector twins. Apply for Korean government GPU support programs (unverified). Once utilization exceeds about 60%, buy a few on-prem 8× RTX PRO 6000 servers.
- Pricing guardrails for CEN tokens derived from unit costs. Physics RL at about $1-10 per 1B steps means RL compute can be bundled cheaply. Price rasterized images at ≥ $0.0001 each, RTX ray-traced at ≥ $0.0005 and path-traced at ≥ $0.005, and meter storage/egress separately, since storage and
  egress (about $126/month and about $495 egress per 1M multimodal frames) exceed raster compute. Price AV sensor simulation per sim-hour at ≥ $20-30 to cover $3-15 COGS.
- Hedge NVIDIA lock-in cheaply: keep OpenUSD as the canonical format, keep a MuJoCo C/MJX CPU/TPU path and a Genesis backend (AMD/Apple/Vulkan) for portability tests, and put every renderer and physics backend behind internal interfaces with sim-to-sim regression tests.
- Differentiate where NVIDIA will not: Korean-language LLM scene control, vertical templates (shipbuilding yards, semiconductor fabs, logistics centers, defense and K-humanoids), photo-to-SimReady asset conversion with physical-parameter estimation, a sim-to-real validation service (real data in the
  marketplace for calibration), and turnkey managed training for non-expert customers.
## Risks
- NVIDIA license risk: the proprietary Kit/RTX/ovrtx/ovphysx terms (NVIDIA SLA + Omniverse / AI Products product-specific terms) may restrict hosted multi-tenant use, redistribution or asset resale, or may later require Omniverse Enterprise subscriptions. Mitigation: proprietary-free training path,
  renderer abstraction, written confirmation from NVIDIA.
- GPU vendor lock-in: Newton, MuJoCo-Warp, Warp and Isaac are all NVIDIA-CUDA-only. A pricing or supply shock on RT-core GPUs (L40S/RTX PRO 6000 supply is thinner than H100) directly hits COGS.
- Wrong GPU class: provisioning H100/H200/B200 for RTX rendering fails because they have no RT cores. Mixing pools without a scheduler causes idle expensive GPUs.
- Alpha-quality dependencies: MuJoCo-Warp is alpha on PyPI, ovrtx 0.5 and ovphysx 0.6 are alpha, Isaac Lab 3.0 is Early Access, and Genesis Nyx is alpha with an undeclared license. API churn could consume 20-30% of engineering capacity.
- Security: Isaac Sim WebRTC streaming has no authentication or encryption and needs host networking. A naive SaaS deployment exposes customer IP; a hardened gateway and per-tenant isolation are mandatory.
- Asset and data licensing contamination: CC-BY attribution (CARLA), Fab/Megascans usage limits (unverified), proprietary NVIDIA assets, and per-model Menagerie/vendor licenses could make sold datasets legally defective.
- Platform commoditization: NVIDIA (Isaac Lab Arena, Omniverse blueprints, Cosmos) and well-funded players (Genesis AI, Applied Intuition, Lightwheel and others) may ship similar hosted features. AICHEMIST must win on verticals, data, UX and Korean enterprise access.
- Talent scarcity in Korea for GPU contact-physics and sensor-physics engineers. Salaries could exceed the planning bands, and hiring could slip by 3-6 months.
- Fidelity gap: the sim-to-real gap for contact-rich manipulation and radar/lidar remains. Customers may churn if policies do not transfer, so calibration and validation services are needed.
- Cost-model uncertainty: rendering throughput, AV-rig GPU counts, KRW salaries, the FX rate (1,400 assumed) and vendor list prices (UE, Unity, Omniverse Enterprise, Korean clouds) could not be verified in this session.
- Unit-economics trap: storage and egress for multimodal synthetic data can exceed render compute. Underpricing tokens per image would create negative gross margin at scale.
- Strategic over-reach: trying to cover robots, AVs, drones, ships and factories at once with a lean team dilutes quality. Sequence verticals.
## Open questions
- Do the NVIDIA Isaac Sim Additional Software and Materials License, the Product-Specific Terms for Omniverse and the AI Products terms (ovrtx) allow commercial multi-tenant hosted SaaS, on-prem container redistribution and marketplace resale of NVIDIA assets? Is an Omniverse Enterprise subscription
  required, and at what 2026 price per GPU?
- What are the 2026 Unreal Engine seat price and EULA terms for non-game simulation SaaS with Pixel Streaming, and do Fab/Megascans licenses allow use outside UE or for generating AI training data for sale?
- What are the current 2026 GPU prices and availability (H100/H200/B200/L40S/RTX PRO 6000) at NHN Cloud, KT Cloud, Naver Cloud and Kakao Cloud, including government-subsidized GPU programs and startup eligibility?
- What are the verified 2026 KRW salary benchmarks for senior graphics, physics, RL/VLA and infra engineers (Wanted, Remember, headhunter data)?
- What renderer and engine does CEN currently use (Unity, UE, Omniverse, custom)? That determines whether tier-2 rendering should be UE5 or Kit rasterization, and how much existing code carries over.
- Which first vertical and anchor customers (e.g., Hyundai/Kia, Samsung, HD Hyundai, CJ Logistics, Doosan Robotics, Rainbow Robotics) are reachable, and do they mandate NVIDIA Omniverse compatibility or on-prem deployment?
- What is the measured throughput of RTX real-time vs path-traced SDG and of ovrtx sensor simulation on RTX PRO 6000 vs L40S for CEN's actual scenes? This is needed to replace the modeled image-cost assumptions.
- Genesis AI's Nyx renderer license and long-term openness, and Genesis AI's funding and team size (unverified here).
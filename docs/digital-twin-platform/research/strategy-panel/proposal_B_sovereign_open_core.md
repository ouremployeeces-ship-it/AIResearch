# CEN Twin: Sovereign Open Core
### Strategy proposal for AICHEMIST's general-purpose digital-twin platform (as of 2026-10-06)

**Legend.** **[A]** marks a planning assumption that has not been verified. **[V]** marks a claim that a named verification gate (Section 6, Phase 0) must clear before we commit money to it. Facts without a tag come from GitHub, PyPI or the SkyPilot price catalog and were verified in the research digest. Where the fact-check corrected a claim, this document uses the corrected version.

---

## 1. Thesis

In 2026 NVIDIA, Google DeepMind and Disney open-sourced the physics engines: Newton 1.6.1, MuJoCo/MJWarp 3.15, the PhysX SDK 5.11 source and Isaac Lab 3.0 source. The pieces NVIDIA charges for are still proprietary: Kit, ovrtx, the ovphysx binaries and the isaacsim/isaaclab wheels. They also collect telemetry, and nobody has confirmed whether they may be redistributed on-prem. Korea's biggest physical-AI buyers are shipbuilders, chaebol factories and defense, and they need twins that run inside their own walls, often air-gapped, with auditable licenses and reproducible data. AICHEMIST should build **CEN Twin**:
- a physics and training core that is 100% permissively licensed;
- three AICHEMIST-owned layers on top of it: the **Sim Kernel API**, the **Renderer/Sensor API** and the **Real2Sim Forge**;
- a **Fidelity Lab** that issues a measured sim-to-real certificate for every asset and policy;
- NVIDIA RTX as an optional premium tier.

We do not compete with the engines. We own the layer that makes them deployable, certifiable and Korean.

**Investor sentence:** *"AICHEMIST builds the physical-AI twin a Korean shipyard or defense lab can install behind an air gap with no proprietary code in the physics-and-training path, and every asset it ships carries a measured sim-to-real certificate."*

### 1.1 Why this angle, and where it is weak

**For:**
- Every on-prem or air-gapped delivery counts as *distribution*. That triggers unverified Kit/ovrtx/Isaac Sim redistribution terms plus GPL and Epic EULA duties. A permissive core removes that exposure for the deployments that pay the most.
- A clean license stack holds up at M&A, in enterprise security reviews and in defense accreditation.
- The physics is already permissive (Newton is a Linux Foundation project; the PhysX SDK core is Apache-2.0), so the "sovereignty premium" is integration work, not invention.

**Against (stated plainly):**
1. **Sovereignty stops at the software layer.** Newton, MJWarp and Warp are fast only on NVIDIA CUDA GPUs (Warp 1.18 needs Turing+ and R580+ drivers).
2. **Sensor fidelity without RTX is lower.** Our open lidar/radar/camera models will trail RTX OmniLidar/OmniRadar for 12–18 months, especially on radar multipath.
3. **It costs about 15% more** than an Isaac-first hybrid: about ₩19억 over 24 months (Section 8).
4. **The photoreal MVP arrives 1–2 months later** than an Isaac Sim start (3–5 months).
5. **Some buyers score Omniverse compatibility** in procurement. OpenUSD and the premium tier answer most of this, not all.
6. **Anyone can assemble the same permissive core.** The moat must come from data, certificates, accreditation and installed base (Section 10).

---

## 2. Engine and stack decision per layer

Versions are as of 2026-10. The **Sovereign core** column marks components that ship in the on-prem and air-gapped editions.

| Layer | Choice (version) | License | Why | Fallback |
|---|---|---|---|---|
| **Robot physics** | **Newton 1.6.1** (pin 1.6.x, upgrade quarterly) with **MJWarp 3.15** as the default solver; Kamino for closed loops (experimental); Featherstone for small differentiable tasks. **MuJoCo 3.15 CPU** (float64, deterministic) as the reference and interactive backend. **Drake v1.57** (BSD-3, CPU) as the offline contact gold standard. Sovereign core: yes. | Apache-2.0 | One Warp/USD API over many solvers. Deterministic paths since v1.4. Linux Foundation governance, so no single vendor can relicense it. Sim2real record: Unitree G1, Skild rack assembly, Samsung cable insertion. | MuJoCo CPU/MJX. **Genesis 1.4.3** (Apache-2.0; CUDA, ROCm, Metal) as the non-NVIDIA hedge, excluding Nyx, which is a closed binary. |
| **PhysX compatibility** | **PhysX SDK 5.11 built from source**, wrapped by **our own USD adapter** and *not* the ovphysx wheels. The ovphysx source is Apache, but the wheels and their ovstage dependency are proprietary. Sovereign core: yes. | Apache-2.0 core (repo root BSD-3) | This is the Isaac Gym/Isaac Lab lineage behind most published sim2real results. GPU SDF contact, FEM, tendons, Vehicle2. Customer assets are often authored for PhysX. | ovphysx 0.6.3 in the premium tier only. We will attempt an upstream "physx_sdk" backend for Isaac Lab. |
| **Vehicles, terrain, marine** | **Chrono 10.0.0**: Vehicle (Pac02/TMeasy tires), SCM and CRM/SPH terrain (29 km on one H100), FSI. **PhysX Vehicle2** for AMRs and light vehicles. An **in-house clean-room Fossen 6-DOF plus wave-spectrum module** for ships. **FMI 3.0 FMU bridge** for customer CarSim/CarMaker models. Sovereign core: yes. | BSD-3 / Apache / own | Best open vehicle and terramechanics stack. The open marine simulators are GPL (Stonefish), tied to UE (HoloOcean) or low fidelity (VRX). | Gazebo Jetty LTS + VRX (Apache-2.0, supported to May 2031) for USV SITL. Chrono's ROCm path is dev-branch only. |
| **Deformables and fluids** | Newton **VBD/Style3D** (cloth, cables, hoses), **ImplicitMPM** (granular), MuJoCo 3.14–3.15 flex (IPC, Neo-Hookean; experimental), Chrono FSI-SPH. Sovereign core: yes. | Apache / BSD-3 | Covers shipyard hoses and cables, sealant and bulk material. Samsung and Lightwheel already use Newton cables. | Genesis IPC/SPH adapter; PhysX FEM. No determinism guarantee for deformables on any engine. |
| **Rendering tiers** | **T0 browser**: three.js r186 + Spark 2.x, PlayCanvas 2.23, Babylon.js 9.29 (OpenUSD WASM loader). **T1 training**: Newton Warp tiled renderer + Isaac Lab physically-plausible ISP. **T2 sovereign photoreal**: gsplat/3DGUT for captured scenes, plus **Blender 5.1 Cycles run as a separate, unmodified process** for path-traced SDG on CUDA. **T3 premium**: Isaac Sim 6.1 / ovrtx 0.5.1 RTX. T0–T2 are in the sovereign core; T3 is not. | MIT/Apache. Blender is GPL, but its outputs are unrestricted. T3 is NVIDIA proprietary. | **T0–T2 need no RT cores**, so they run on government B200/H200 and customer H100 fleets. T3 is used only where RTX lidar/radar is worth the cost. | UE 5.8/CARLA as an optional connector, never in the core. Unity HDRP is frozen, so skip it. |
| **Neural realism** | **gsplat 1.6.0** and **3DGRUT 2.0** (3DGUT on any GPU; 3DGRT on RT-core GPUs only). **fVDB Reality Capture 0.4** for site-scale capture. Feed-forward geometry: **DA3 Small/Base/Metric** and **MapAnything-apache**; **VGGT-1B-Commercial** in non-defense editions only. **TRELLIS.2** for generative completion, with nvdiffrast replaced. **Cosmos 3 Nano 16B** for label-preserving augmentation. Sovereign core: yes, except where noted. | Apache / MIT / OpenMDW-1.1 **[V]** | Commercially safe replacements for the non-commercial Inria/NVIDIA research code. Standardized on OpenUSD ParticleField and KHR_gaussian_splatting (ratified). | Cosmos Transfer 2.5 (maintenance only). No world model ever runs inside the physics loop. |
| **Sensor simulation** | **AICHEMIST Sensor Model Library**, written as Warp kernels: camera ISP (PPISP-style), lidar ray-cast with per-band material reflectance, simplified FMCW radar, IMU/GNSS noise, event cameras (v2e), and tactile (MuJoCo touch_grid + Newton hydroelastic pressure). Sovereign core: yes. | Own code (Apache dependencies) | Sovereign fidelity is won or lost here, and RTX is proprietary. Calibrated per-device profiles also become marketplace products. | RTX OmniLidar/OmniRadar via ovrtx (premium); Chrono::Sensor. TacSL is excluded because it works only on the PhysX path inside Isaac Sim. |
| **Scene format** | **OpenUSD 26.08**, pinned per release. UsdPhysics plus namespaced schemas (newton-usd-schemas v0.x, mjc, physx). OpenPBR/MaterialX 1.39. UsdVolParticleField for splats. MCAP, **LeRobotDataset v3**, FMI 3.0/SSP and ASAM OpenDRIVE/OpenSCENARIO/OSI at the edges. Sovereign core: yes. | TOST (Apache-derived) / Apache / MIT | The industry standard. Layer composition gives live overlays, branching and audit. WASM builds open the browser path. | glTF/GLB + SPZ for the web. Note that AOUSD Core 1.0 excludes UsdPhysics. |
| **Training stack** | **Isaac Lab 3.0 built from GitHub source** (pin the GA release, expected around Nov 2026) on the Kit-less Newton backend, plus **mjlab 1.6.0**. Libraries: rsl_rl 5.5, skrl 2.1, **LeRobot 0.6.1**, Isaac Lab Mimic, RLinf 0.3 (phase 2), RF-DETR N–L. VLA zoo: **SmolVLA** (default and defense); GR00T N1.7 **[V]**; pi0.5 gated until its weight terms are confirmed. Sovereign core: yes. | BSD-3 / Apache | One task API across backends. The isaaclab PyPI wheel is labeled proprietary, so we build from source. | MuJoCo Playground / Brax training. |
| **Web and streaming UX** | Browser-first client. **Our own WebRTC gateway** (NVENC + auth/TLS + session manager). Selkies (MPL-2.0) for the CEN virtual desktop. Viser/Rerun for rollouts. Sovereign core: yes. | MIT / Apache / MPL | Zero server-GPU cost by default. Isaac Sim streaming has no authentication or encryption. | Kit livestream behind our gateway, premium tier only. |
| **Orchestration and infra** | K8s + **GPU Operator v26.7.1** + **KAI Scheduler v0.18.2**, Ray 2.59, Argo Workflows, MLflow 3, Harbor, Kafka, Postgres/TimescaleDB core, SeaweedFS or Ceph RGW **[V]** (not MinIO, which is AGPL **[A]**). SkyPilot for SaaS burst only. Sovereign core: yes. | Apache etc. | The same Helm bundle runs SaaS, sovereign cloud and air-gapped installs. No BSL or AGPL in the shipped bundle, so lakeFS 1.87+ is excluded. | OSMO 6.3 (Apache) as an optional DAG engine. |
| **LLM agent** | First-party **MCP server** (spec 2026-07-28) plus a sandboxed USD-code agent. Model-agnostic: a frontier API in SaaS; an on-prem open-weight model in sovereign editions; a Korean sovereign model preferred for public and defense customers **[V]**. Sovereign core: yes. | Model licenses vary | Korean-language scene control is a differentiator. | NVIDIA kit-usd-agents for API grounding (dev time only). |

**GPU classes.** We run three pools:
- **R (RT-core):** L40S and RTX PRO 6000 Blackwell, for T3, 3DGRT and streaming.
- **C (compute):** H100, H200 and B200, for RL, VLA, Cosmos and Cycles-on-CUDA batch work.
- **L (light):** L4, CPU and dev workstations.

Because the sovereign T0–T2 path needs no RT cores, we can use government B200/H200 allocations **[V]**.

---

## 3. Build vs buy map

| Category | Components |
|---|---|
| **OWN (core IP)** | **Sim Kernel API**: load/step/get_state/set_state/apply_actions/render/contacts/snapshot/restore/set_seed/capabilities, plus a cross-backend conformance suite. **PhysX-SDK USD adapter.** **Renderer API + Sensor Model Library.** **Real2Sim Forge**: pipeline, articulation and physical-parameter models fine-tuned on our own data. **Fidelity Lab** and its certificate schema. Run Manifest and scene-commit service. Twin runtime (live, simulation and shadow modes). MCP server + authoring agent with validation gates. Korean LLM scene compiler. Control plane: tenancy and metering into CEN tokens. **License/provenance registry** (SPDX gate). **Sovereign packaging**: air-gap installer, signed SBOM, offline updates. Clean-room marine dynamics. Vertical content packs (shipyard, factory, logistics). |
| **INTEGRATE (open source)** | Newton, MJWarp, MuJoCo, Drake, PhysX SDK, Chrono, Gazebo/PX4 (BSD-3), Isaac Lab (source), mjlab, rsl_rl, skrl, LeRobot, RLinf, gsplat, 3DGRUT, fVDB, TRELLIS.2 (without nvdiffrast), DA3/MapAnything, CoACD/CuACD, Articulate-Anything (MIT baseline), Cosmos 3, OpenUSD, MaterialX, three.js/Spark/PlayCanvas/Babylon, K8s/KAI/Ray/Argo, open62541, Blender Cycles (process-isolated). |
| **LICENSE (commercial)** | NVIDIA Isaac Sim/Kit/ovrtx, premium tier only. NVAIE is about $4,500/GPU/yr at list or $1,125 with the Inception discount **[A][V]**. Customers bring their own CarSim/CarMaker/MF-Tyre/FTire via FMI. Optional Remcom WaveFarer for high-end radar. |
| **PARTNER** | **NVIDIA** (Inception, co-sell). **Linux Foundation Newton** (upstream contributions in vehicle hooks, tactile and Korean industrial assets). **MORAI** (it keeps AV/UAM scenarios; we supply sensor data and robot learning). **Korean CSPs** NHN, Naver and KT, for sovereign cloud and RT-core capacity **[V]**. **Group SI arms** (HD Hyundai IT, Samsung SDS, LG CNS) as resellers. **KRISO/KR** for maritime credibility and **KATRI** for AV correlation **[V]**. KAIST/SNU labs. Doosan Robotics and Rainbow for hardware. |

**Do we build our own physics engine or renderer? No.** The evidence:
1. **Cost and time.** A competitive engine plus renderer would take about 150–300 engineer-years (40–80 specialists for 3–5 years), roughly ₩400–600억, with a 30–48+ month time-to-MVP. Our hybrid path reaches MVP in 4–6 months.
2. **Track record.** MuJoCo took about a decade at Roboti before DeepMind. Newton needed three large organizations plus prior Warp/MuJoCo code to reach 1.0 on 2026-03-10. Chrono has about 20k commits and Drake about 35k.
3. **We cannot keep up with release cadence.** Newton shipped six minor releases in seven months, and MuJoCo ships a minor release every 2–3 weeks.
4. **Fidelity is not the bottleneck.** Independent 2026 benchmarks (GAUGE, GPUSimBench; numeric results unverified) find no engine uniformly faithful to reality. The gap is calibration and measurement, which we *do* own.

What we *do* build are the abstraction layers, two narrow physics modules (sensor physics and marine hydrodynamics), and upstream contributions that earn us roadmap influence.

---

## 4. Beachhead verticals and sequencing

Scores run 1–5, where 5 is best. For Competition, 5 means the field is open.

| Vertical | KR demand | Competition | Korean anchors | CEN fit | Sovereign pull | Time to revenue | Total | Wave |
|---|---|---|---|---|---|---|---|---|
| Robot-arm manipulation (heavy-industry cells) | 4 | 3 | 5 | 5 | 4 | 5 | **26** | **1** |
| Factory cell / in-plant logistics | 4 | 2 | 4 | 4 | 5 | 4 | 23 | 1 (context) |
| Ship / port / shipyard autonomy | 5 | 4 | 4 | 3 | 5 | 3 | **24** | **2** |
| Off-road / defense UGV | 4 | 4 | 3 | 3 | 5 | 2 | 21 | 2 |
| Drone (perception, counter-UAS) | 3 | 3 | 3 | 3 | 4 | 3 | 19 | 2 (inside the defense edition) |
| Humanoid | 4 | 2 | 4 | 3 | 3 | 3 | 19 | **3** |
| AMR / logistics (standalone) | 3 | 2 | 3 | 4 | 2 | 4 | 18 | add-on |
| Quadruped | 2 | 2 | 3 | 2 | 3 | 3 | 15 | template only |
| AV/ADAS | 4 | 1 | 3 | 3 | 3 | 2 | 16 | partner (MORAI) |

**Wave 1 (M3–15): heavy-industry manipulation cells.** Targets are welding, grinding, painting-prep and part handling, plus in-cell AMR and crane logistics, in shipyard workshops and chaebol plants.
- *Demand:* MASGA-driven shipyard automation and HD Hyundai's target of 30% shorter production time by 2030.
- *Competition:* no sim-and-learning vendor owns this space. Siemens, Dassault and the SI arms build PLM twins that cannot train policies.
- *Anchors:* one shipbuilder robotics unit (HD Hyundai Robotics/FOS, Samsung Heavy or Hanwha Ocean) plus Doosan Robotics, which already uses Isaac/cuRobo, or Rainbow.
- *CEN fit:* revenue from day one through perception SDG (weld seams, defects, PPE), BIM-to-USD conversion and the existing NeRF capture work.
- *Physics maturity:* rigid manipulation is the most mature regime on MJWarp and PhysX.
- *Time to revenue:* a paid PoC of ₩2–5억 within 4–6 months.

**Wave 2 (M12–27): maritime and defense editions.**
- *Maritime:* ship and port perception (EO/IR, marine radar, sea state, night), COLREG scenario libraries and port-crane twins.
- *Demand:* the Autonomous Ship Act (in force since 2025-01-03) requires performance verification. Avikus runs on about 350 vessels, and SHI's SAS made an autonomous Pacific crossing.
- *Competition:* marine open-source simulators are fragmented and no commercial leader exists. This is the strongest white space in the research.
- *Defense:* the air-gapped edition adds off-road UGV (Chrono CRM terrain) and drone perception (PX4 SITL, Gazebo Jetty). It follows the Duality/Bifrost business model, and its anchor is one defense prime.
- *Timing:* this wave comes second because it needs the Chrono/marine modules, sensor calibration and accreditation, and sales cycles run 12–24 months.

**Wave 3 (M20–36): humanoids, an evaluation arena, and AV data.**
- *Humanoids:* a "K-Physical AI Arena" for K-Humanoid Alliance members, offering neutral sim-plus-real-cell evaluation **[V]** and a VLA data factory.
- *Timing:* humanoid locomotion training is commoditized by free tools (mjlab, GR00T), so we enter where neutrality and data, not tooling, are scarce.
- *AV:* perception-only data through MORAI. We do not compete in OEM HIL against Applied Intuition (about $830M ARR **[A]**), dSPACE or IPG.

---

## 5. Architecture sketch

```
┌─ L7 EXPERIENCE ─ CEN browser workspace (WebGPU viewer · Jupyter/VS Code · Selkies desktop)
│                 Korean/English command bar (MCP client) · Fidelity dashboards · Marketplace
├─ L6 AGENT & APIs ─ First-party MCP server · REST/gRPC · Python SDK
│                 Authoring agent (gVisor/Kata sandbox) → validation gates → scene branch → human merge
├─ L5 LEARNING ────────────────────────┬─ L4 TWIN RUNTIME ──────────────────────────
│  Isaac Lab (src) / mjlab · LeRobot   │  LIVE   : OPC UA/MQTT/ROS 2 → Kafka → twin-state
│  RL · IL/Mimic · VLA · SDG · Eval    │           → USD live layer (10–60 Hz) + TSDB
│  Sim2Real kit (sysid, actuator nets) │  SIM    : fork-from-live → calibrate → batch what-if/RL
│                                      │  SHADOW : real controller ↔ sim, lockstep clock (HIL)
├─ L3 SIM KERNEL API (OWN) ────────────┴───────────────────────────────────────────
│  Physics adapters: Newton/MJWarp · MuJoCo CPU · PhysX-SDK · Chrono · FMU · Genesis(exp)
│  Renderer API: T0 web · T1 Warp tiled · T2 3DGUT/Cycles · T3 RTX*  │ Sensor Model Library
│  Conformance suite · Run Manifest (scene hash, image digest, driver, GPU SKU, seeds, MCAP)
├─ L2 SCENE & ASSETS ─ OpenUSD stage service · scene commits/branches · Real2Sim Forge
│                     Fidelity certificates · license/provenance registry (SPDX gate)
├─ L1 DATA ─ Object store · Postgres · Kafka · TSDB · MCAP · LeRobot v3 · MLflow registry
└─ L0 INFRA ─ K8s + GPU Operator + KAI │ pools R / C / L │ Harbor · signed SBOM
     EDITIONS: Global SaaS │ Sovereign Cloud (KR CSP) │ On-prem │ Air-gapped (no T3, no telemetry)
  * T3 = NVIDIA proprietary premium tier, absent from Sovereign and Air-gapped builds by default
```

**Live twin vs simulation twin.**
- A **live twin** mirrors state. Edge gateways (open62541, MQTT, ROS 2 Humble/Jazzy/Lyrical over Zenoh) feed Kafka, then a twin-state service. That service writes a per-twin USD session layer, which overrides only transforms, joint states and signals and is pushed to browsers.
- A **simulation twin** forks a live snapshot and calibrates it, using MuJoCo's sysid toolbox and actuator nets. It then runs faster than real time on Pool C or R and scores itself against later live data. That score is the *twin-fidelity KPI*.
- **Shadow mode** runs real controllers against the simulator in lockstep.
- Our ROS 2 bridge is our own code, not the Isaac Sim workspace (which supports only Humble and Jazzy), so we support Lyrical LTS on day one.

**LLM/MCP agent.**
- *Typed, permissioned tools:* `scene.query/diff/apply_ops`, `asset.search`, `sim.run/sweep`, `job.submit`, `twin.query/forecast`, `dataset.export`, `policy.evaluate`.
- *Code generation:* USD-Python generation happens only in a sandbox.
- *Gates before commit:* UsdValidation, physics sanity checks (mass/inertia, interpenetration, joint limits) and a two-backend smoke test.
- *Execution limits:* no community MCP with arbitrary exec reaches tenants.
- *Scenario output:* constrained to OpenSCENARIO DSL, so scenarios stay reproducible.

**Marketplace and asset pipeline (Real2Sim Forge).** CEN's NeRF pipeline becomes a 3DGUT-based Forge:
1. Capture from phone or robot video, lidar, or CAD/BIM.
2. Estimate poses and metric depth (DA3-Metric, MapAnything).
3. Train a gsplat/3DGUT splat for the visual layer.
4. Extract a mesh (fVDB, plus our own PGSR-style re-implementation).
5. Complete unseen parts with TRELLIS.2.
6. Infer articulation (Articulate-Anything baseline, later our own model).
7. Build collision geometry with CuACD.
8. Set mass and friction from VLM priors, refined by sysid on short interaction videos.
9. Run physics QA on three backends.
10. Export SimReady USD + MJCF/URDF + glTF (KHR_gaussian_splatting), with a **Fidelity certificate** and a **license manifest**.

Every upload goes through the provenance gate. Assets derived from Hunyuan3D, Inria 3DGS, Instant-NGP, nvdiffrast, ManiSkill or PhysX-Anything are rejected.

---

## 6. Phased roadmap (M0 = Nov 2026)

| Phase | Deliverables | Exit criteria | Demo milestone |
|---|---|---|---|
| **P0 Ground Truth** M0–3 | **Verification gates V1–V8** (below). License audit of CEN's NeRF stack (Instant-NGP is non-commercial). SPDX gate in CI. **Bake-off** on 1× RTX PRO 6000 + 1× H100 across Newton/MJWarp, MuJoCo CPU, PhysX-SDK (src) and Isaac Lab (src): G1 velocity, a BeyondMimic clip, Franka lift, LEAP in-hand, cable insertion, cloth fold, a Kamino gripper. Sim Kernel API v0 spec and conformance suite v0 (5 scenes). Order the Sovereign Lab cluster. | Decision memo with *our own* steps/s/$ and sim2sim deltas. 0 non-commercial, AGPL or proprietary components in the core SBOM. ≥2 LOIs (one shipbuilder, one robot OEM). TIPS operator signed **[V]**. | One USD welding cell runs on three backends side by side in the browser, with a live divergence plot. A Korean text command edits and randomizes the scene. |
| **P1 Sovereign Core MVP** M3–10 | Sim Kernel v1 (Newton, MuJoCo, PhysX-SDK adapter). Renderer T0–T2. Sensor library v1 (RGB-ISP, depth, segmentation, lidar, IMU). Isaac Lab-src and mjlab templates: arm reach/pick/place, cell AMR, quadruped/humanoid locomotion. Teleop → Mimic → IL/VLA (SmolVLA; GR00T gated). Forge v1 for rigid objects. MCP v1 (read/run). Single-tenant on-prem beta Helm chart. | Arm sim2real gap ≤15 pp on 3 anchor tasks. Synthetic-only detector ≥85% of real-data mAP on the anchor's inspection task. One on-prem beta installed. ₩10억 contracted. | **"Photo to policy in a day"**: phone video of a shipyard workpiece → certified asset → Mimic data → policy running on a real Doosan/HD Hyundai arm. |
| **P2 Twin Runtime and On-prem GA** M10–18 | Live/Sim/Shadow modes. Scene commits. Fork-from-live calibration. Chrono vehicle/terrain adapter. Marine Fossen module v1 with EO/IR and simplified marine-radar models. Multi-tenant SaaS (KAI queues; MIG where available **[V]**). **Sovereign Edition GA** (on-prem and Korean-CSP sovereign cloud). Premium RTX tier, only after V1 clears. Fidelity Lab v1 certificates. GS certification and ISMS-P. | 3 sovereign-edition contracts. On-prem install ≤3 days. Sim2real ≤10 pp on 3 tasks. Synthetic-only ≥90% of real mAP, and synthetic + 10% real ≥100%. Marine PoC with Avikus or SHI. ARR ≥₩15억. | A live shipyard-cell twin mirrored at 30 Hz. A what-if fork validates a new crane schedule and a retrained policy. A COLREG encounter with synthetic EO/IR/radar. |
| **P3 Air-gapped and Certified Content** M18–27 | **Defense/Air-gapped Edition**: offline signed update bundles, no telemetry, a defense license profile that excludes the SAM License, VGGT-Commercial and any **[V]** models. UGV (Chrono CRM) and drone (PX4) packs. Marketplace with 500+ certified assets and 5 Korean site twins. K-Physical AI Arena v1. Cosmos 3 Nano augmentation with label QA. RLinf post-training. Field flywheel (MCAP → failure mining → re-simulation). | 1 accredited defense pilot. 2 shipyards live. ≥5 robot makers in the Arena. NRR ≥110%. ARR ≥₩50억. | An air-gapped rack runs end to end (capture → train → evaluate) with the network physically disconnected. |
| **P4 Scale and Export** M27–36 | Japan entry (Korean suppliers' Japanese plants, AIRoA **[V]**). US entry following Korean OEM plants (HMGMA, Hanwha Philly). Global SaaS. Partner program for SIs. Humanoid VLA data factory. Newton core-contributor status. | ARR ≥₩90억. ≥20% of revenue from outside Korea. Blended gross margin ≥65%. ≥2 engineers with Newton commit rights. | The same certified asset pack sells in Seoul, Nagoya and Georgia, with certificates reproduced on the customers' own hardware. |

**Phase 0 verification gates:**
- **V1** NVIDIA's written terms for multi-tenant SaaS, on-prem redistribution and dataset-only sales.
- **V2** Legal opinion on Blender as a separate process in an on-prem bundle, on ArduPilot/GPL, and on whether ovstage can be replaced in an ovphysx source build.
- **V3** In-house benchmarks.
- **V4** RT-core GPU availability and MIG support on Korean CSPs.
- **V5** Salary benchmarks.
- **V6** Korean program calls and caps.
- **V7** Terms for OpenMDW-1.1, the GR00T Open Model License and the openpi weights, including military-use clauses.
- **V8** On-prem LLM license and origin acceptability for defense customers.

---

## 7. Team and effort split

End-of-phase headcount (FTE). Phase 0 starts with about 8 engineers reassigned from CEN **[A]**.

| Workstream (owns) | P0 | P1 | P2 | P3 | P4 |
|---|---|---|---|---|---|
| **WS1 Sim Kernel and Physics**: Kernel API, adapters, conformance, Chrono/marine, upstream Newton work | 4 | 5 | 6 | 7 | 7 |
| **WS2 Rendering, Sensors and Streaming**: Renderer API, sensor library, WebRTC gateway, T3 integration | 2 | 3 | 4 | 5 | 6 |
| **WS3 Real2Sim Forge and Fidelity Lab**: reconstruction, sim-ready conversion, sysid, capture operations, certificates | 2 | 4 | 5 | 6 | 7 |
| **WS4 Learning**: RL, IL/VLA, SDG/perception, evaluation, Arena | 2 | 4 | 5 | 6 | 7 |
| **WS5 Platform and Sovereign Ops**: K8s/KAI, control plane, metering, security, air-gap packaging, SBOM | 2 | 3 | 4 | 5 | 6 |
| **WS6 Twin Runtime, Agent and Web UX**: connectors, MCP/agent, browser client | 1 | 3 | 4 | 5 | 6 |
| **WS7 Verticals and GTM**: PM, solution engineers, technical artists, 0.5 FTE licensing counsel | 1 | 2 | 4 | 6 | 9 |
| **Total** | **14** | **24** | **32** | **40** | **48** |

**Hiring order:**
1. A simulation architect/CTO-track hire with Newton/MuJoCo/OpenUSD depth (Korean-American or remote is acceptable).
2. Two Warp/CUDA physics engineers who can earn Newton upstream credibility.
3. A USD/asset-pipeline engineer.
4. A sysid/sim2real engineer with access to a real arm and a quadruped.
5. Two sensor/rendering engineers, recruited from Korean game studios (Nexon, NCSoft, Krafton, Pearl Abyss).
6. A K8s GPU and security engineer, plus an air-gap packaging engineer.
7. Two RL/VLA engineers.
8. An OPC UA/industrial-IoT engineer.
9. A maritime dynamics engineer (Fossen, COLREG).
10. Solution engineers, one per vertical.

Retention: options plus a publish-and-upstream culture. Senior specialist salaries run ₩1.2–1.8억+ **[A]**.

---

## 8. 24-month budget (M0–M24, KRW)

**Assumptions:**
- FX is ₩1,400/USD **[A]**.
- The fully loaded cost is **₩1,500만 per head-month**. That figure blends a base salary of about ₩1.32억 with a 1.18× statutory load (4대보험 plus severance) and ₩25M per head per year for overhead and recruiting **[A][V5]**. The base-salary blend is 55% senior at ₩1.5억, 30% mid-level at ₩0.8억, 10% leads at ₩2.2억 and 5% technical artists at ₩0.75억.
- Average headcount is 12, 19, 28 and 34 across M0–3, M3–10, M10–18 and M18–24, which gives **597 head-months**.

| Line | Basis | ₩억 |
|---|---|---|
| **People** | 597 HM × ₩1,500만 | **89.6** |
| Pool R: RT-core | 2× 8-GPU RTX PRO 6000 Blackwell servers for the "Sovereign Lab", also the air-gapped reference (≈₩1.6억 each **[A]**) = 3.2; cloud RT burst of ~25k GPU-h at ~$2.5 = 0.9 | 4.1 |
| Pool C: H100/H200/B200 | ~60k GPU-h at ~$3.5 on Lambda/RunPod-class providers, before any government in-kind GPUs **[V]** | 2.9 |
| Pool L: dev and CI | 30 RTX 5090-class workstations (≈₩800만 **[A]**) plus L4/CPU CI | 3.0 |
| Pilot serving (Seoul) | Premium sessions and customer pilots. AWS Seoul RTX PRO 6000 costs $4.135/h; partly recovered through tokens | 2.0 |
| Storage and egress | Synthetic data at about 5.5 TB per 1M multimodal frames | 1.5 |
| **Compute subtotal** | | **13.5** |
| Licenses | NVIDIA premium-tier dev/test on 16 GPUs × 2 years at $1,125–4,500/GPU/yr **[A][V1]** = 1.5; dev, CI, security and SBOM tooling = 1.5; LLM APIs = 0.5 | **3.5** |
| Fidelity Lab hardware | 2 industrial cobots, 1 research arm, 1 quadruped, 1 G1-class humanoid, a dexterous hand, F/T sensors, mocap, capture rigs **[A]** | 6.0 |
| Legal and IP | OSS counsel, NVIDIA negotiation, about 10 patent filings | 2.5 |
| Certification and security | ISMS-P, ISO 27001, GS certification, penetration tests, CSAP readiness | 2.0 |
| GTM | GTC, iREX, Kormarine, PoC travel | 3.0 |
| **Subtotal** | | **120.1** |
| Contingency (8%) | | 9.6 |
| **Gross 24-month total** | ≈ **$9.3M** | **≈129.7** |

**Comparison and offsets:**
- The research's Isaac-first hybrid with 12→25 people costs about ₩80억. Our plan is larger (14→36 people at M24). It also carries the **sovereignty premium** of about ₩19억 (about 15%): the PhysX adapter at 24 HM, the sensor library at 36 HM, air-gap packaging at 36 HM, marine at 12 HM, and the lab cluster.
- *Offsets:* non-dilutive funding of about ₩30–60억 (Deep-tech TIPS up to ₩15억, Super-Gap up to ₩6억, consortium work packages) **[A][V6]**, plus about ₩35억 of contribution margin on PY1–PY2 revenue.
- **Net equity need: about ₩45–65억.**
- *Lean fallback:* if the Series B has not closed by M9, freeze headcount at 28 and defer Wave 3. The 24-month total then drops to about ₩105억.

---

## 9. Business model and pricing

CEN Twin plugs into CEN's existing **subscription + token + marketplace** model. It adds new token sinks (GPU pools), new subscription editions and new marketplace SKUs (certified assets, site twins, sensor profiles, policies). All prices below are **[A]** and are re-priced quarterly against actual pool cost, with a floor of ≥30% gross margin.

| Offer | Price point | Notes |
|---|---|---|
| Explorer (free/education) | ₩0 | Browser viewer, MuJoCo CPU, 20 L-pool hours per month |
| Studio seat | ₩49만/seat/month | Includes 100 L-hours and 20 R-hours. Compare UE at about $1,850/seat/yr **[A]**. |
| Team / Lab | ₩3,900만/yr | 5 seats, 2,000 R-hours, private marketplace |
| Tokens per GPU-hour | L ₩1,000 · R ₩6,500 · C ₩9,000; premium RTX session +₩3,000/h | Cost bases: RunPod RTX PRO 6000 $2.09, AWS Seoul $4.135, Lambda H100 $3.99/GPU-h |
| Per-output floors | Raster ≥₩0.15/image · RTX ≥₩0.7 · path-traced ≥₩7 · AV sensor rig ≥₩35,000/sim-hour | Storage and egress metered separately |
| **Sovereign Edition** (on-prem or KR sovereign cloud) | ₩2.5억/yr platform fee (≤16 GPUs, 20 seats) + ₩1,200만/GPU/yr beyond that | Typical deal ₩4–8억/yr, with support SLA |
| **Defense / Air-gapped Edition** | ₩8–15억/yr | Offline update channel, accreditation support, on-site engineer |
| Premium RTX tier | NVIDIA license at cost + 15%, or bring your own license | Only after V1 clears |
| Physical-AI Data Factory PoC | ₩2–5억 per 3–4 months | Fixed scope, ends with a measured sim2real result |
| Marketplace | Certified asset ₩3–30만; Korean site-twin pack ₩0.5–3억; 25% take rate on third-party assets | Every SKU ships with a license manifest |
| Certification | ₩500만 per asset class; ₩3,000만–1억 per robot-task sim2real certificate | Issued by the Fidelity Lab |

**Revenue targets [A]:**

| | PY1 (M1–12) | PY2 (M13–24) | PY3 (M25–36) |
|---|---|---|---|
| PoC / NRE | 9 (3 × ₩3억) | 15 | 25 |
| Sovereign Editions | 0 | 15 (3 × ₩5억) | 54 (9 × ₩6억, incl. renewals) |
| Defense Edition | 0 | 6 (pilot) | 20 (2 × ₩10억) |
| Data, marketplace, certificates (incl. voucher-funded) | 6 | 10 | 24 |
| SaaS seats and tokens | 1 | 6 | 12 (KR + JP/US) |
| **Total (₩억)** | **16** | **52** | **135** |
| Exit ARR | ₩5억 | ₩30억 | ₩90억 |

---

## 10. Moat

| Rival | Their play | Why we win (or where we do not) |
|---|---|---|
| **NVIDIA commoditization** | Gives away engines, Cosmos and GR00T; monetizes Kit/ovrtx/NVAIE and GPUs | We are built *on* what NVIDIA gives away, so each free release improves us. NVIDIA's monetized layers are exactly what air-gapped buyers struggle to deploy (proprietary, telemetry, unverified redistribution terms). NVIDIA does not provide Korean on-site integration, accreditation or certified vertical content, and it wants partners for that. **Weak spot:** a managed Isaac cloud in Korea would hit our SaaS tier, though not our on-prem tier. |
| **Chaebol in-housing / SI arms** | Omniverse + Siemens twins built by Samsung SDS, HD Hyundai IT and others | Their teams are thin on RL and sim2real. We sell *through* the SI arms as the sovereign learning kit, and our certificates and asset library span many customers. **Weak spot:** after a PoC an SI can absorb the work, so we put Forge, Kernel and certificates under license terms that survive that. |
| **MORAI** | AV/UAM/maritime scenarios; government ties | It has limited manipulation and RL depth and is reportedly Unity-based **[A]**. We partner on AV and compete only where marine and defense sensor realism matter. |
| **Applied Intuition** | AV and defense toolchain, about $15B valuation **[A]** | Premium-priced, AV-centric and a foreign vendor for Korean sovereign programs. We avoid HIL homologation entirely. |
| **Lightwheel** | SimReady assets and benchmarks, NVIDIA-aligned | The closest analog. Its free assets are non-commercial, and its US/China footprint is a trust issue in Korean defense and chaebol accounts **[A]**. We win on commercially licensed assets with *measured* physics plus on-prem delivery. |
| **Genesis AI** | Open multi-physics simulator; pivoting to its own models (GENE-26.5) | Its renderer (Nyx) is closed, and it competes with its own data customers. We integrate Genesis as a backend and stay neutral. |
| **Chinese data factories** (AgiBot, Manycore, 51WORLD) | Near-zero-price assets and data | Trust and geopolitics barriers with Korean defense and chaebol buyers. We position as the trusted non-China, license-clean vendor. |
| **E8, CyLab** | City twins; synthetic data | No robot-learning loop. We differentiate on training plus certificates. |

**What compounds:**
1. Accreditation and installed base: security certifications, GS certification and defense approvals each take 12–24 months to replicate.
2. Fidelity Lab data: measured mass, friction and actuator parameters for Korean industrial SKUs, which improve the Forge models with every customer capture under data-rights terms.
3. Certificates as a de facto standard through the K-Physical AI Arena.
4. Korean-language agent plus vertical templates.
5. Upstream influence in Newton under Linux Foundation governance.

**Honest note:** in the first 18 months, until (1) and (2) accumulate, the moat is thin.

---

## 11. Top risks and mitigations

| # | Risk | P/I | Mitigation |
|---|---|---|---|
| 1 | **NVIDIA Kit/ovrtx/Isaac Sim terms** forbid or tax hosted, on-prem or redistributed use **[V1]** | M/M | T3 sits behind the Renderer API, is absent from sovereign builds and launches only after written terms. Kit telemetry is disabled or excluded. Outputs-only selling remains possible but is **unverified**. |
| 2 | **ovphysx/ovstage dependence** makes the "PhysX from source" path impure | M/M | We own the PhysX-SDK USD adapter. ovphysx is premium-only, and we upstream our backend. |
| 3 | **Model and asset contamination**: Hunyuan3D excludes Korea including its outputs; Inria 3DGS/2DGS/MILo, Instant-NGP, nvdiffrast, MimicGen code, PhysX-Anything and ManiSkill assets are non-commercial; GO-1 and RLDX-1 are non-commercial | H/H | SPDX gate in CI plus a marketplace provenance gate, with automatic blocking. The CEN NeRF audit happens in P0. We re-implement methods (PGSR-style meshing) from papers, not code. |
| 4 | **Defense clauses**: the SAM License forbids ITAR/military use, VGGT-Commercial bars military use, and Cosmos and GR00T terms are unverified | H/M | The defense profile excludes them and uses DA3 Apache, MapAnything-apache and SmolVLA **[V7]**. |
| 5 | **Copyleft via distribution**: Blender (GPL), ArduPilot (GPL), Stonefish (GPL), Ultralytics (AGPL), MinIO (AGPL **[A]**), lakeFS (BSL) | M/H | Blender runs as an unmodified separate process with source offered **[V2]**. PX4 (BSD-3) replaces ArduPilot. The marine module is clean-room. RF-DETR replaces Ultralytics. No BSL or AGPL in bundles. |
| 6 | **GPU class**: H100/H200/B200 have no RT cores; RTX PRO 6000/L40S supply in Korea is thin **[V4]** | M/H | T0–T2 need no RT cores, so government B200/H200 capacity is usable. We own 16 RTX PRO 6000s. Workloads are routed by steps/s/$. |
| 7 | **Driver floor**: Warp 1.18 needs Turing+ GPUs and R580+ drivers; customer on-prem fleets may lag | M/M | Installer preflight check. We ship a validated driver/firmware matrix and keep MuJoCo CPU as a fallback. |
| 8 | **API churn**: Newton releases monthly, Isaac Lab 3.0 breaks APIs (quaternion order, ProxyArray), MJWarp is alpha, mjlab lags MJWarp | H/M | Sim Kernel API plus a conformance suite on every upgrade. Quarterly pins. 20% of WS1 capacity reserved for maintenance. |
| 9 | **Fidelity and determinism**: no engine is uniformly faithful; MJWarp is non-deterministic in float32 | H/H | The Fidelity Lab measures rather than claims. Run Manifest, MuJoCo CPU bit-exact replay and Newton's deterministic mode. Datasets are labeled "statistically reproducible" when run on GPU. |
| 10 | **Sensor fidelity gap** without RTX (radar and lidar intensity) | H/M | Per-device calibration profiles and published error bars. T3 sold where it is needed. |
| 11 | **Chaebol in-housing and long sales cycles** (12–24 months) | H/H | SI-reseller channel, voucher- and TIPS-funded PoCs, and license terms that cover Forge and Kernel after the PoC. |
| 12 | **Talent scarcity** (GPU contact physics, sensor physics) | H/M | Remote and Korean-American hires, game-studio recruiting, and upstream visibility as a hiring magnet. |
| 13 | **Policy-cycle and verification risk**: program caps, GPU allocations and market sizes are unverified | M/M | Plan on equity. Count grants only once awarded. |
| 14 | **Export control and LLM origin**: EAR rules on GPUs and weights for Middle East deals; Chinese-origin open weights may be unacceptable in defense | M/M | Export screening per deal. On-prem LLM chosen per edition **[V8]**. |

---

## 12. KPIs per phase

| Phase | Technical KPIs | Business KPIs |
|---|---|---|
| **P0** (M0–3) | 7 bake-off tasks × 3 backends measured. Conformance v0 passing on 5 scenes. Core SBOM has 0 non-commercial, AGPL, BSL or proprietary components. | ≥2 LOIs. TIPS operator signed. NVIDIA terms requested in writing. 2 voucher supplier registrations. |
| **P1** (M3–10) | Arm sim2real gap ≤15 pp on 3 tasks. Forge v1: rigid asset in ≤30 min, mass error ≤15%, friction error ≤20% vs measured. Synthetic-only detector ≥85% of real mAP. Quadruped zero-shot transfer. ≥4,096 envs/GPU. | 2–3 paid PoCs. ₩10억 contracted. 1 on-prem beta. 300 monthly active Studio users. |
| **P2** (M10–18) | Sim2real ≤10 pp. Synthetic-only ≥90% of real mAP; synthetic + 10% real ≥100%. Lidar range error ≤2 cm on a calibration target. Live-twin RTF ≥1.0 for a multi-robot cell. Cross-backend conformance within tolerance. Bit-exact CPU replay. | 3 Sovereign Edition contracts. ARR ≥₩15억. GS certification and ISMS-P. Install ≤3 days. |
| **P3** (M18–27) | Air-gapped end-to-end with 0 outbound calls. 500 certified assets. Marine radar/EO-IR profile errors published. Arena correlation (sim vs real success) Pearson r ≥0.8 on ≥5 policies. | 1 accredited defense pilot. ARR ≥₩50억. NRR ≥110%. ≥5 Arena members. |
| **P4** (M27–36) | Certificates reproduced on customer hardware within tolerance. ≥2 Newton core contributors. Forge throughput ≥200 certified assets/week. | ARR ≥₩90억. ≥20% non-Korean revenue. Gross margin ≥65%. CAC payback ≤18 months. |

**Bottom line:** adopt the engines, own the kernel, sensors, Forge and certificates, and ship the only license-clean, air-gap-ready physical-AI twin in Korea. RTX remains a premium option, never a dependency.

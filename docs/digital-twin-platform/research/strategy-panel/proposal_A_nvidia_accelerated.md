# CEN Twin: An NVIDIA-Accelerated Digital Twin Platform for AICHEMIST
**Strategic angle: "NVIDIA-Accelerated Speed" · Status date: 2026-10-06 · Month 0 (M0) = October 2026**

Tags used throughout: **(A)** is our planning assumption. **(U)** is a research claim that could not be checked against a primary source. No (U) item drives a go/no-go decision without the verification step listed in §11. FX is 1 USD = 1,400 KRW (A).

---

## 1. Thesis

The physics-engine and renderer race is over, and NVIDIA and its open-source partners won it. Isaac Sim 6.1, Isaac Lab 3.0, Newton 1.6, Cosmos 3, GR00T N1.7 and NuRec are free or cheap, release every month, and are the stack Korean conglomerates are standardising on. What Korean industry lacks is not an engine. It lacks a fast, accountable way to turn that stack into robots that work: trained policies, validated synthetic data, Korean-domain scenes, and a Korean-speaking team that delivers on site. AICHEMIST should become the fastest and most trusted NVIDIA physical-AI delivery platform in Korea. The product is **CEN Twin**: it runs on the NVIDIA runtime under formal licences, is sold first as 12-week paid PoCs in robot-arm manipulation, and each PoC converts into CEN subscriptions, tokens and marketplace spend. We give up some independence to gain 6–12 months of speed. We keep a way out by running the training path on Newton (Linux Foundation, Apache-2.0) and storing every scene as OpenUSD.

**The investor sentence:** *"Korea bought 260,000 NVIDIA GPUs; AICHEMIST is how they become working robots in 12 weeks."* The 260k figure was reported in October 2025 and is (U).

**Honest scoring.** The research team's decision matrix scores a hybrid open-core plan ("D") at 4.23 and an NVIDIA-centric plan ("B") at 3.70. This proposal is "B+": B's runtime with D's internal seams and NVIDIA licences we pay for. Rescored on the same weights, B+ comes to about 4.1. Licensing safety rises from 2 to 4 once the terms are in writing, physics rises from 4 to 4.5 because Newton runs inside Isaac Lab, and cost falls from 3 to 2.5. B+ still trails D slightly on paper. We accept that gap because B+ reaches an MVP in 3–5 months against D's 4–6, and because NVIDIA co-selling into chaebol accounts is worth more than the matrix can price.

**Weaknesses of this angle that we accept with open eyes:**
1. Licences become a cost and a dependency. NVIDIA AI Enterprise (NVAIE) lists at about $4,500 per GPU per year (U), and the hosting terms are not yet in writing.
2. We are locked into NVIDIA hardware. Rendering needs CUDA and RT-core GPUs; the only non-NVIDIA hedge (Genesis/Quadrants) is experimental.
3. NVIDIA gives away blueprints, usd-content-agents and Cosmos, which erodes our features, and partner status is not exclusive.
4. APIs churn. Kit shipped about 3 major versions in 12 months, Isaac Lab 3.0 breaks APIs, and upgrades can eat 20–30% of engineering capacity.
5. Key pieces are immature. ovrtx and ovphysx are alpha, Isaac Lab 3.0 is Early Access, there is no ROS 2 Lyrical support, and the Pegasus drone simulator is still on Isaac Sim 5.1.
6. Streaming is expensive. A dedicated RT-core GPU costs $1.9–2.3 per session-hour.

---

## 2. Engine and stack decision per layer

| Layer | Choice and version (Oct 2026) | Licence | Why | Fallback |
|---|---|---|---|---|
| **Physics: robots** | **Isaac Lab 3.0** (EA 2026-09-16, GA targeted for end of Oct 2026) on **Isaac Sim 6.1.0** (2026-09-10). PhysX (SDK 5.11) is the default for contact-rich manipulation. **Newton 1.6.1** (MJWarp solver) runs Kit-less for locomotion and humanoids, Kamino (beta) handles closed kinematic loops, and SDF/hydroelastic contact handles insertion. | Isaac Lab BSD-3. PhysX SDK core Apache-2.0. Newton Apache-2.0 (Linux Foundation). Isaac Sim runtime and Kit are NVIDIA proprietary. | One task API over several backends. It is the best-documented manipulation stack (Mimic, Teleop, TacSL, Arena). Newton is co-built by NVIDIA, so we stay "all-NVIDIA" while keeping an open path. | mjlab 1.6.0 plus MuJoCo 3.15 on CPU (float64, deterministic reference) |
| **Physics: vehicles, terrain, marine** | PhysX vehicles inside Isaac Sim for yard and road vehicles. **Project Chrono 10.0** co-simulation for off-road tyres (Pac02/TMeasy), SCM/CRM terramechanics and SPH fluid-structure interaction. In-house **Fossen 6-DOF plus wave-spectrum Warp kernels** for vessels. **FMI 3.0.2** adapter so customers can bring CarSim or CarMaker models. | PhysX and Chrono BSD-3; our own code; FMI open | Vehicles should not be forced into the robot RL engine. Chrono is the best open terramechanics engine. Marine has no dominant vendor. | BeamNG.tech partnership (priced by quote); customer-supplied FMUs |
| **Deformables and fluids** | Newton VBD/Style3D for cloth and cables, ImplicitMPM for granular media; Isaac Sim 6.1 experimental VBD/XPBD; Chrono SPH for water | Apache-2.0 / BSD-3 | Cable and hose insertion is already used in production (Samsung and Lightwheel, medium confidence) | Genesis World 1.4.3 (Apache-2.0) adapter for IPC/SPH; MuJoCo 3.15 flex (experimental) |
| **Rendering tiers** | **T0** browser WebGPU (three.js r186, Babylon.js 9.29, PlayCanvas 2.23, Spark for splats) for editing and previews, at zero server GPU cost. **T1** Isaac Sim 6.1 RTX real-time on L40S / RTX PRO 6000 Blackwell for interactive premium sessions and synthetic-data generation (SDG). **T2** RTX path tracing for hero shots and ground truth. **T3** (from M10) ovrtx (0.5.1, alpha) as a Kit-less sensor service once it reaches GA. | Web libraries MIT/Apache; Kit, RTX and ovrtx NVIDIA proprietary | Best-in-class physically based camera, lidar and radar in one USD scene, and customers ask for "Omniverse-compatible" | Newton GL/Warp renderer for RL debugging; Blender Cycles offline on non-RT GPUs |
| **Neural realism** | Reconstruction with **NuRec** (GA at GTC 2026 via NGC; terms (U)) plus **3DGRUT 2.0 / gsplat 1.6.0** inside our Forge, rendered as Isaac Sim ParticleField 3DGS. Augmentation with **Cosmos Transfer 2.5** now (limited maintenance), moving to a **Cosmos 3 Nano 16B** fine-tune from M8. **Cosmos 3 Super 64B** for world-model policy evaluation in Phase 3. | 3DGRUT and gsplat Apache-2.0; Cosmos 3 OpenMDW-1.1; Transfer 2.5 weights NVIDIA Open Model License | Real-to-sim reconstruction removes the gap at the target site; world models add appearance diversity under label-preserving controls | gsplat-only reconstruction; Cosmos Transfer 2.5 only |
| **Sensor simulation** | Isaac Sim RTX camera (with PPISP), RTX lidar, radar and ultrasonic, IMU; TacSL tactile (PhysX path); OSI 3.7 export for vehicles; event cameras via EVIS (research) | NVIDIA runtime; TacSL inside Isaac Lab | Same scene, same labels. RTX lidar and radar are the hardest pieces to rebuild ourselves. | ovrtx; Newton ray-casters |
| **Scene format** | **OpenUSD** is canonical: the USD build bundled with Isaac Sim 6.1 at runtime, OpenUSD 26.08 for tooling. Physics via UsdPhysics plus PhysxSchema, Newton and MJC schemas, labels via UsdSemantics, following SimReady conventions. Edge formats: URDF/MJCF (Apache converters), glTF with KHR_gaussian_splatting (ratified), OpenDRIVE 1.8 / OpenSCENARIO, MCAP, LeRobotDataset v3. | AOUSD Core 1.0.1 (CC-BY-ND spec); converters Apache-2.0 | It is the format NVIDIA, Siemens and chaebol twins use | USD is itself the hedge |
| **Training** | RL: Isaac Lab 3.0 plus rsl_rl 5.5.1 (default) and skrl 2.1.0. Imitation: Isaac Teleop, Isaac Lab Mimic (Apache) and LeRobot 0.6.1. VLA: **GR00T N1.7** for humanoid and bimanual, SmolVLA for low cost, pi0.5 blocked until its weight terms are confirmed. VLA RL: RLinf 0.3 (Phase 2). Evaluation: Isaac Lab Arena v0.3. Perception: Replicator SDG plus RF-DETR N–L. Deployment: ONNX to TensorRT on Jetson AGX Thor. | BSD/Apache/MIT; GR00T weights under NVIDIA Open Model License | One `isaaclab` command covers every RL library, and the GR00T-to-Jetson path gives the strongest demos | mjlab plus LeRobot (fully open) |
| **Web and streaming UX** | The existing CEN browser workspace plus a React "Twin Studio" modelled on the NVIDIA DSX blueprint. A Kit 110.x USD Viewer app runs on **Kit App Streaming** (K8s/Helm) behind **our own authentication and TLS WebRTC gateway**, with 10-minute idle auto-suspend. | Kit proprietary; gateway is ours | The fastest route to photoreal rendering in the browser. Isaac Sim's own streaming has no authentication or encryption. | NVCF managed streaming (availability in Korea (U)); Selkies-style desktop streaming |
| **Agent layer** | A first-party MCP server (spec 2026-07-28) using Isaac Sim MCP and **kit-usd-agents** (Apache-2.0) for API grounding, plus Isaac Lab 3.0 agent skills; USD code generation runs in a sandbox | Ours plus Apache | CEN already has an LLM text-command interface; this makes it physically grounded | Our own tool set without NVIDIA MCPs |
| **Orchestration and infrastructure** | K8s 1.32+, GPU Operator v26.7, **KAI Scheduler** v0.18, **NVIDIA OSMO** for SDG/training/HIL pipelines, Ray 2.59 and SkyPilot burst. Two GPU pools: **RT** (L40S / RTX PRO 6000, driver R580+) and **Train** (H100/H200/B200). | Apache-2.0 | Open-source and NVIDIA-native; OSMO already models Isaac workflows | Kueue/KubeRay; Slurm via Slinky |

**Version discipline.** We ship one release train per half-year. Train 1 runs Nov 2026–Jun 2027 on Isaac Sim 6.1.x, Isaac Lab 3.0 GA, Newton 1.6.x and Kit 110.x. Isaac Sim 7.0 (alpha since 2026-09-18) lives only on a side branch and is adopted on Train 2 or 3, after its GA and one patch release.

---

## 3. Build-vs-buy map

**Do we build our own physics engine or renderer? No.** The evidence:
- Building our own (Strategy A) is estimated at 150–300 engineer-years (₩400–600억) and 30–48+ months to an MVP. An NVIDIA-centric build reaches an MVP in 3–5 months.
- Engines take years and large teams. MuJoCo spent about a decade at Roboti before DeepMind. Newton needed NVIDIA, DeepMind, Disney and earlier code to reach 1.0 on 2026-03-10, then shipped six minor releases in seven months. MuJoCo releases every 2–3 weeks. A Korean startup cannot out-iterate free engines.
- Owning the solver does not close the realism gap. GAUGE (U) found no engine uniformly faithful to reality. The gap closes through calibration and measurement, so that is where we invest.
- We touch engines only through Warp kernels (custom sensors, actuators, marine dynamics) and upstream Newton contributions (tactile sensors, Korean industrial assets).

| OWN (core IP, ~70% of engineering) | INTEGRATE (open source) | LICENSE (commercial) | PARTNER |
|---|---|---|---|
| CEN Twin control plane: tenancy, RBAC, GPU-second metering into CEN tokens, data-residency tags | Isaac Lab, Newton, MuJoCo/mjlab, PhysX SDK, Chrono | **NVAIE / Omniverse Enterprise** for every GPU that serves Kit or Isaac Sim to third parties | **NVIDIA**: Inception, then an NPN partner tier; co-selling into HMG, Samsung, SK and Naver; early access to 7.x |
| Secure streaming gateway and session broker | OpenUSD plus URDF/MJCF converters, MCAP, LeRobot v3 | **Isaac Sim/Kit OEM or redistribution rights** for the on-prem appliance | **Korean cloud providers** (Naver Cloud, NHN, KT) for RT-core capacity (U) |
| Scene repository: content-hashed USD layer commits, branches, run manifests (lakeFS is now BSL 1.1, so we build this) | gsplat, 3DGRUT, Cosmos 3, GR00T code, TRELLIS.2 (with nvdiffrast replaced), VGGT-1B-Commercial, DA3 Small/Base/Metric, MapAnything-apache, CoACD/CuACD | **NuRec container terms**, if priced separately (U) | **SI arms as resellers**: Samsung SDS, LG CNS, SK AX, Hyundai AutoEver, HD Hyundai |
| Sim-kernel adapters and conformance suite (thin, following the Isaac Lab factory pattern) | rsl_rl, skrl, Isaac Lab Mimic, Isaac Lab Arena, RLinf, RF-DETR N–L | **ovrtx production terms** when it reaches GA | **Robot OEMs**: Doosan Robotics (already on Isaac/cuRobo), Rainbow Robotics, HD Hyundai Robotics |
| **Alchemist Agent**: a Korean/English LLM driving MCP tools that produce validated USD operations and training jobs | KAI, OSMO, Ray, Kafka, open62541 (MPL-2.0) | Customer-licensed CarSim/CarMaker connected through FMI | **MORAI** (AV scenarios); KATRI, KTL and KIRIA (third-party validation); KAIST, SNU and ETRI (IITP co-research) |
| **Real2Sim Forge** (the evolution of CEN's NeRF pipeline) plus fidelity certificates | three.js, Babylon.js, PlayCanvas, Spark | — | **Lightwheel** as a possible asset-reseller or benchmark partner |
| **Sim2Real Gap Scorecard**, calibration lab, vertical packs, licence and provenance registry, fork-from-live service | | | |

**Deny list (enforced in CI):**
- 3D generation and reconstruction: Hunyuan3D 2.x (its licence excludes Korea, including use of outputs); Inria 3DGS and its derivatives 2DGS, MILo and PGSR; Instant-NGP; nvdiffrast; PhysX-Anything (S-Lab licence).
- NVIDIA research code: MimicGen and DexMimicGen code.
- Non-commercial assets, data and weights: ManiSkill assets, AgiBot GO-1, RLDX-1 weights, Waymax and the Waymo Open Dataset, the original VGGT-1B, DA3 Large/Giant.
- Copyleft: Ultralytics (AGPL) anywhere in the SaaS; GPL BlenderProc and Stonefish in anything shipped on-prem.
- Conditional: cuRobo only at a pinned Apache-2.0 tag after NVIDIA confirms the terms (Isaac Lab ships it under a restrictive licence), and SkillGen stays off until then.

---

## 4. Beachhead verticals and sequencing

| Rank | Vertical | Demand (Korea) | Competition | Anchor customers | CEN fit | Time to revenue |
|---|---|---|---|---|---|---|
| **1** | **Robot-arm manipulation in factory cells** (pick-place, bin-picking, assembly, inspection) | High: Samsung AI Megafactory, HMG and LG lines, and SME automation under M.AX (U) | Lightwheel globally, CyLab for data, chaebol SIs | Doosan Robotics, Rainbow Robotics (about 35% Samsung-owned), HD Hyundai Robotics, auto tier-1s | Highest: indoor SDG, asset marketplace, NeRF capture | **3–4 months** |
| **2** | **Factory mobility: AMR fleets plus humanoids** (from M8) | AMR: CJ Logistics, Coupang, Hyundai Glovis (A). Humanoid: K-Humanoid Alliance (Apr 2025), HMG/Boston Dynamics, Samsung/Rainbow, LG | NVIDIA blueprints, robot makers' in-house teams | Alliance work packages; HMG physical-AI cluster | High: GR00T N1.7 and Newton locomotion templates; strongest demos | 8–12 months |
| **3** | **Shipyard and port** (welding, painting and block-logistics robots; vessel and port perception) (from M14) | HD Hyundai (Avikus on about 350 vessels), Samsung Heavy (SAS), Hanwha Ocean; MASGA US-yard modernisation (U); Autonomous Ship Act in force since 3 Jan 2025 | No dominant vendor; MORAI is entering maritime; shipbuilders may build with Siemens/Palantir | HD Hyundai, SHI, Hanwha Ocean | Medium: the robot cells reuse vertical 1; marine needs Fossen dynamics, radar and EO/IR | 12–18 months |
| 4 | Defence UGV and drones, air-gapped SKU (from M20) | ADD, Hanwha Aerospace, LIG Nex1, KAI | MORAI, Duality-style vendors | Defence primes | Medium: Chrono terrain; Pegasus needs porting from Isaac Sim 5.1 | 18–24+ months |
| — | AV/ADAS | Real but crowded | Applied Intuition, dSPACE, IPG, MORAI; NVIDIA AlpaSim is free | — | Perception data only, through MORAI or tier-1s | Opportunistic |
| — | Quadrupeds | Demo value only | — | — | Free Isaac Lab template | Not a revenue line |

**Why manipulation first.** It is where NVIDIA's stack is deepest: Isaac Lab Mimic turns 10 demos into 1,000 in 18–40 minutes, and GR00T N1.7, TacSL and Replicator all target it. It is also where CEN's SDG and asset strengths transfer directly. Every chaebol factory twin begins with a robot cell. Doosan Robotics already integrates Isaac and cuRobo, which is verified on GitHub. Most importantly, a 12-week PoC can be delivered as **outputs only**: datasets, policies and reports produced on our own GPUs. Per the research summary this is outside NVAIE (U), so revenue can start before NVIDIA's hosting terms are signed.

**Why AMR and humanoid second.** They reuse the factory scene and add fleet-level and whole-body value. Humanoids bring the K-Humanoid Alliance, the strongest investor narrative and GTC-grade demos, but revenue is lumpy and depends on consortium funding, so they follow vertical 1 instead of leading.

**Why shipyard third.** It is the largest Korean-unique prize, with no incumbent and ITAR-free demand. It needs marine dynamics, radar and EO/IR work that we can afford only after verticals 1 and 2 pay for the platform. Shipyard robot cells, however, are vertical 1 with new assets, which gives us an early entry point.

---

## 5. Architecture sketch

```
L8 AGENT      Alchemist Agent (KR/EN) -> first-party MCP -> sandbox (gVisor/Kata) -> validation gates -> human merge
L7 UX         CEN browser workspace | Twin Studio (React + WebGPU T0) | Jupyter/VS Code | "High-fidelity" WebRTC (T1/T2)
L6 APIs       REST/gRPC | Python SDK | MCP tools | Marketplace API | Token metering (DCGM + KAI -> CEN tokens)
L5 LEARNING   Isaac Lab 3.0 RL/IL/VLA | Replicator SDG + Cosmos augmentation | Arena eval | ONNX/TensorRT -> Jetson Thor
L4 TWIN       LIVE mirror | SIMULATION (batched, faster than real time) | SHADOW/HIL (lockstep) | fork-from-live
   FORGE      capture -> poses/depth -> 3DGUT -> mesh -> articulation -> collision -> physics ID -> SimReady + certificate
L3 RUNTIME    Isaac Sim 6.1 (Kit 110, RTX sensors, PhysX) | Newton 1.6 Kit-less | MuJoCo CPU reference | Chrono co-sim | FMU
L2 SCENE      OpenUSD layer-stack repo (content-hash commits/branches) | SimReady validation | Run manifests
L1 DATA       S3 | Postgres | Kafka | TSDB | MCAP | LeRobot v3 | model registry | licence/provenance registry
L0 INFRA      K8s + GPU Operator + KAI + OSMO | RT pool (L40S/RTX PRO 6000) | Train pool (H100/H200/B200) | Seoul + on-prem
```

**Main data flows:**
1. **Live twin (a mirror, with no physics in the loop).**
   - Ingest: PLCs, robots and AMRs send data over OPC UA (open62541), MQTT or ROS 2 (Humble/Jazzy native; Lyrical via a Zenoh/DDS bridge) to the edge gateway, then into Kafka.
   - State: a twin-state service maps W3C WoT descriptions to USD prim paths and writes a USD *live session layer* that overrides only transforms, joint states and signals at 10–60 Hz. Browsers receive it over WebSocket, and history goes to the TSDB.
2. **Simulation twin.** We snapshot the live layer into a scene branch, then calibrate it with the MuJoCo sysid toolbox and actuator networks. What-if, RL and SDG jobs then run headless on the RT or Train pool. Predictions are scored against later live data to produce a *twin-fidelity score*. In Shadow/HIL mode, the customer's controller runs against the simulator on a lockstep clock.
3. **Agent.** A Korean prompt goes to the planner, which calls typed MCP tools: `scene.search`, `scene.apply_ops`, `asset.search`, `sim.run`, `job.submit`, `dataset.export` and `policy.evaluate`. Generated USD code runs in a sandbox and must pass UsdValidation, a physics sanity check (mass, inertia, interpenetration) and a backend smoke test before it is committed to a branch; a human approves the merge. NVIDIA MCPs are used only for API grounding, and tenants never get raw-exec tools.
4. **Marketplace and asset pipeline (Forge).**
   - Input: phone or robot video, or CAD/BIM.
   - Reconstruction: VGGT-1B-Commercial / MapAnything poses, a 3DGUT splat, a mesh, TRELLIS.2 to complete unseen parts, articulation, then CoACD/CuACD collision shapes.
   - Physics: VLM estimates of mass and friction are refined by system identification, then checked by physics QA on PhysX and Newton.
   - Output: SimReady USD, URDF/MJCF, glTF/KHR_gaussian_splatting, a licence manifest and a fidelity score. The asset is listed on the marketplace and used in scenes. The datasets it produces carry run manifests and become marketplace dataset packs. Customers opt in before their data improves our models.
5. **Learning loop.** A scene becomes an Isaac Lab environment and then a policy. The policy passes Arena evaluation and a sim-to-sim gate (PhysX vs Newton), is exported through ONNX/TensorRT to Jetson Thor, and runs in the field. Field MCAP logs feed failure mining, which feeds the next simulation round.

Each run carries a **run manifest**: USD commit hash, container digest, backend and version, GPU SKU and driver, seeds, timestep and substeps, and the MCAP input log. GPU runs are statistically reproducible, not bitwise; a CPU MuJoCo or deterministic Newton replay is the audit path. This is how CEN keeps its "reproducible" promise.

---

## 6. Phased roadmap (36 months)

**Phase 0 "Ignite": M0–4 (Oct 2026–Jan 2027)**
- *Deliverables, licensing and audit:* in weeks 1–6, engage NVIDIA Korea and Inception and request written terms covering (a) multi-tenant streaming SaaS, (b) on-prem/OEM redistribution, (c) dataset-only sales, (d) bundling NVIDIA assets in the marketplace and (e) telemetry control; request an NVAIE quote; audit CEN's code and NeRF pipeline with SPDX tags.
- *Deliverables, product:* the **CEN Twin α** runs Isaac Sim 6.1 headless and Isaac Lab 3.0 GA on one owned 8× RTX PRO 6000 node. It ships three templates (cobot pick-place, bin-picking SDG, G1/quadruped velocity), an authenticated WebRTC gateway and Agent v0 with 10 MCP tools. NuRec/3DGRUT import of customer cells works, and the move from NeRF to 3DGUT begins.
- *Deliverables, sales:* 15 qualified accounts and a fixed-price **12-week "Cell-to-Policy" PoC** offer.
- *Exit criteria:* at least 1 paid PoC signed and invoiced by M4; NVIDIA's written guidance requested (received is the target); licence audit closed.
- *Demos:* **M2 "Korean text-to-cell":** a Korean command builds a cobot cell, generates 50k labelled images, trains a policy and streams the result to the browser. **M4:** a policy trained only in simulation runs on a real cobot.

**Phase 1 "Cell-to-Policy": M4–10 (Feb–Jul 2027)**
- *Deliverables:*
  - Product: **CEN Twin β**, hosted for PoC customers or bring-your-own-licence (BYOL) until NVIDIA's terms are signed. Forge v1 for rigid objects, Scorecard v1, the Teleop-to-Mimic-to-VLA pipeline (SmolVLA, GR00T N1.7), and KAI multi-tenant queues.
  - Marketplace: 100 certified SimReady assets and 5 Korean factory-cell environments.
  - Partnerships and funding: an NPN partner listing; a TIPS submission; registration as an AI-voucher and data-voucher supplier.
- *Exit criteria (the **M10 gate**):* at least 3 paid PoCs, 2 of them converted to annual contracts; NVIDIA hosting and OEM terms in writing; PoC gross margin of at least 40%. If the gate fails, headcount freezes at 27 and the SaaS core moves to the Kit-less Newton/mjlab path (plan D).
- *Demos:* "Phone-to-policy in 24 hours" (scan, SimReady asset, Mimic, VLA, real robot), staged as an NVIDIA partner showcase (A: GTC 2027 slot).

**Phase 2 "Factory Twin": M10–18 (Aug 2027–Mar 2028)**
- *Deliverables:*
  - Hosted product: **CEN Twin GA**, a hosted SaaS on a Seoul RT pool licensed under NVAIE.
  - Twin features: live-twin connectors and fork-from-live; AMR fleet simulation (50+ robots); humanoid loco-manipulation templates; Cosmos 3 Nano augmentation with label QA.
  - On-prem and compliance: **Twin Sovereign** on-prem appliance v1 (Helm, air-gap capable, OEM rights); ISMS-P / ISO 27001.
  - Engineering: Isaac Sim 7.x on release Train 3.
- *Exit criteria:* ARR of ₩30억; 2 chaebol-group logos through their SI arms; 1 on-prem install; one K-Humanoid or IITP work package won.
- *Demos:* a live factory twin with AMRs and a humanoid; a what-if re-layout requested in Korean, with predicted vs actual throughput.

**Phase 3 "Yard & Sovereign": M18–27 (Apr–Dec 2028)**
- *Deliverables:*
  - Shipyard and port: a shipyard pack (welding and painting cells, block logistics, crane); a port and vessel perception module (EO/IR, marine radar, sea state, Fossen dynamics, 500 COLREG scenarios).
  - Off-road, defence and drones: Chrono off-road co-simulation; a defence air-gapped SKU (no SAM- or VGGT-licensed components); a drone module (Pegasus ported to Isaac Sim 6.x/7.x, or our own PX4 SITL bridge).
  - International: a Japan PoC.
- *Exit criteria:* ARR of ₩60억; one shipbuilder production programme; one defence contract; one Japanese customer.
- *Demos:* a welding policy trained in simulation runs on a real block mock-up; a vessel detector trained on at least 90% synthetic data is benchmarked at sea.

**Phase 4 "Scale & Export": M27–36 (Jan–Sep 2029)**
- *Deliverables:* world-model closed-loop evaluation (Cosmos 3); a **K-Physical AI Arena** with KTL/KIRIA; a US entity that follows Korean OEM plants (HMGMA, Hanwha Philly); a self-serve global tier; the fleet data flywheel.
- *Exit criteria:* ARR of ₩130억; at least 55% recurring revenue; a path to break-even in 2030.
- *Demos:* a public Arena leaderboard; a field failure replayed and fixed in under 48 hours.

---

## 7. Team and effort split

FTE at the end of each phase. 8 of Phase 0's 16 are existing CEN staff reassigned from the web workspace, NeRF, SDG and marketplace teams (A). The CEO is not counted.

| Workstream | Owns | P0 | P1 | P2 | P3 | P4 |
|---|---|---|---|---|---|---|
| WS1 Sim Runtime & Physics | Isaac Lab/Newton/PhysX/Chrono integration, conformance suite, system ID, Warp kernels, Newton upstream contributions | 3 | 4 | 5 | 6 | 6 |
| WS2 Realism & Sensors | RTX sensors, NuRec/3DGUT, Forge, Cosmos augmentation, Scorecard, calibration lab | 3 | 5 | 7 | 8 | 9 |
| WS3 Learning Factory | RL/IL/VLA templates, Teleop/Mimic, Arena evaluation, perception, Jetson deployment | 2 | 4 | 6 | 7 | 8 |
| WS4 Platform & Infra | K8s/KAI/OSMO, streaming gateway, tenancy and metering, on-prem appliance, security and compliance | 3 | 5 | 6 | 7 | 8 |
| WS5 UX, Agent & Marketplace | Twin Studio, WebGPU, Alchemist Agent/MCP, marketplace, licence registry | 2 | 3 | 5 | 6 | 7 |
| WS6 Solutions & Vertical Content | Forward-deployed engineers (FDEs), technical artists, vertical packs, PoC delivery | 2 | 4 | 6 | 7 | 9 |
| WS7 Alliances, GTM & PM | NVIDIA alliance, licensing and legal (0.5 FTE), grants, PM, sales | 1 | 2 | 3 | 4 | 5 |
| **Total** | | **16** | **27** | **38** | **45** | **52** |

Effort mix: about 30% engine integration (WS1 + WS2 runtime work), 40% our own IP (Forge, Scorecard, Agent, platform), and 30% customer delivery (WS6 plus FDE time). We reserve 20% of WS1 and WS4 capacity for NVIDIA upgrades.

**Hiring order:**
- *Months 0–3:*
  1. Simulation architect with Isaac, Kit and OpenUSD experience (M0)
  2. NVIDIA alliance and licensing lead (M0)
  3. Isaac Lab RL / sim-to-real engineer (M1)
  4. RTX sensor and rendering engineer from a game studio (Nexon, NCSoft, Krafton, Pearl Abyss) (M1)
  5. Streaming-security platform engineer (M1)
  6. Two FDEs with cobot-integrator backgrounds (M2)
  7. Neural-reconstruction engineer (M3)
  8. USD pipeline engineer / technical artist (M3)
- *Months 5–6:*
  9. VLA engineer (M5)
  10. System-ID engineer with lab experience (M5)
  11. Kubernetes GPU SRE (M6)
  12. Agent/MCP engineer (M6)
- *Later:* humanoid whole-body control (M9), AMR fleet (M10), marine and vehicle dynamics (M14), defence security officer (M16), Japan business development (M20).

Senior specialists cost ₩1.2–1.8억+ a year, so we retain them with stock options.

---

## 8. 24-month budget (M0–M24, Oct 2026–Sep 2028)

**Assumptions (A):**
- Fully loaded cost of ₩1,495만 per head-month (mid case). This covers the 1.18× statutory load and severance, ₩25M per head per year of overhead, and recruiting.
- Salary bands (low confidence; to be confirmed with Wanted, Remember and headhunters): CTO/architect ₩1.8–2.6억; senior physics, RL or rendering ₩1.1–1.8억; infra ₩1.0–1.5억; web-3D ₩0.9–1.3억; mid-level ₩0.65–0.95억; technical artist ₩0.6–0.9억.
- Head-months: 52 (P0) + 132 (P1) + 264 (P2) + 240 (M18–24) = 688.

| Line | Basis | ₩억 |
|---|---|---|
| **People** | 688 head-months × ₩1,495만 | **103.0** |
| RT pool, owned | 3 × 8-GPU RTX PRO 6000 Blackwell servers bought at M1, M7 and M13, about ₩1.6억 each (A); colocation and power ₩1.0억 | 5.8 |
| RT pool, cloud burst | Average 12 GPUs × 24 months × 730 h × $2.3/h blended (Korean cloud, neocloud, AWS Seoul at $4.1 for latency-critical work) | 6.8 |
| Train pool (H100/H200/B200) | Average 6 GPUs × 24 months × 730 h × $3.5/h on neoclouds. Government B200/H200 allocations (U) are upside and not budgeted. | 5.2 |
| Storage, egress, CPU, network, observability | Synthetic data storage and egress can exceed raster render cost | 3.0 |
| **Compute subtotal** | | **20.8** |
| NVAIE / Omniverse Enterprise | Average 30 hosted GPUs × 2 years × $4,500 list (U); about ₩1.0억 if the 75% Inception discount (U) applies | 3.8 |
| Other software and connectors | CAD/PLM connector SDKs, security tooling, developer tools | 2.0 |
| Legal | NVIDIA terms, open-source audit, export control, contracts | 1.5 |
| Certifications | ISO 27001 / ISMS-P, GS (TTA), CSAP readiness, KOLAS test reports | 1.5 |
| **Licences and legal subtotal** | | **8.8** |
| Sim-to-real lab | 2 cobots, 1 G1-class humanoid, 1 quadruped, 1 AMR, 4 Jetson AGX Thor, lidar/cameras/force-torque/tactile sensors, capture rigs, 2 XR headsets for Isaac Teleop (A) | 6.0 |
| Go-to-market and events | GTC, AI Day Seoul, iREX, Automatica, demo builds | 3.5 |
| PoC travel and on-site support | | 1.5 |
| **Subtotal** | | **143.6** |
| Contingency (10%) | | 14.4 |
| **Total (24 months)** | about **$11.3M** | **≈158** |

**Funding logic.**
- Target revenue in the window is about ₩80억 and gross, with collections lagging.
- Non-dilutive funding (TIPS, Super-Gap, vouchers, consortia) is estimated at ₩30–60억 (U).
- Both are upside to runway, not the plan of record. **Raise ₩100억+ of equity by M9–12**, using NVIDIA partner status and at least 4 PoCs as proof points. NVentures participation is a stretch goal (A).
- **Gate-fail budget:** if the M10 gate fails and headcount freezes at 27, the 24-month spend is about ₩120억.
- For comparison: a lean 12-person plan (₩50억) cannot cover more than one vertical, and the research team's ramped plan D costs ₩80–85억.

---

## 9. Business model and pricing (all inside CEN's subscription, token and marketplace model)

| SKU | Price point | Notes |
|---|---|---|
| Twin Explorer | Free | WebGPU only, 10 RT-GPU-hour trial, education and lead generation |
| Twin Pro | **₩390,000 per seat per month** (about $3,340 a year; Unity Industry is about $4,950 (U)) | Includes 30 RT-GPU-hours; Isaac Lab templates |
| Twin Team | ₩2.9M per month | 5 seats, 200 RT-GPU-hours, private projects |
| Twin Enterprise (hosted VPC) | From **₩2억 per year** | 20 seats, 4 reserved RT GPUs, SSO, SLA; NVAIE passed through, or BYO-NVAIE (chaebol likely already hold licences (A)) |
| Twin Sovereign (on-prem) | **₩5–15억 per year** plus ₩1–2억 installation | NVIDIA OEM licence passed through; hardware supplied by the SI partner |
| Tokens: RT-GPU-hour | ₩6,000 (cost $1.1–2.3, so about 50–75% gross margin) | No cross-tenant time-slicing |
| Tokens: Train-GPU-hour (H100-class) | ₩8,500 (cost $2.9–3.5) | |
| Tokens: synthetic images | ₩0.3 raster, ₩1.5 RTX real-time, ₩15 path-traced per image (about 2× the research cost floors) | Storage ₩40,000 per TB-month and egress ₩150 per GB, metered separately |
| Cell-to-Policy PoC | **₩1.5–2.5억** over 12 weeks, 30% upfront | Delivered as outputs only: twin, dataset, policy and sim-to-real report |
| Production programme | ₩4–10억 per year | Continuous SDG, retraining and evaluation |
| Policy pack / Arena certification | ₩1–3억 per task / ₩3,000만–1억 per model | |
| Marketplace | Certified asset ₩5만–50만; environment twin ₩3,000만–1.5억; dataset pack ₩2,000만–3억; 30% take rate on third-party sellers | Every item carries a licence manifest and fidelity score |

**Revenue targets (A; targets, not forecasts):**

| | FY2026 (Q4) | FY2027 | FY2028 | FY2029 |
|---|---|---|---|---|
| Revenue | ₩0.5억 | **₩25억** (7 PoCs at ₩12.6억, 2 production programmes at ₩6억, vouchers ₩3억, SaaS/tokens ₩2억, marketplace ₩1.4억) | **₩80억** (8 enterprise accounts at ₩40억, 2 on-prem at ₩14억, PoCs ₩16억, SaaS ₩6억, marketplace ₩4억) | **₩190억** (16 enterprise accounts at ₩96억, 5 sovereign/defence at ₩40억, NRE ₩20억, SaaS ₩18억, marketplace ₩16억) |
| Recurring share | — | 20% | 45% | 60% |
| Year-end ARR | — | ₩15억 | ₩60억 | ₩150억 |

---

## 10. Moat: why AICHEMIST wins

| Rival | Their play | Why we win | Where we could lose |
|---|---|---|---|
| **NVIDIA** | Free tools, blueprints and models; sells GPUs | NVIDIA needs local partners who turn GPUs into deployed workloads. We are the last mile: Korean FDEs, vertical content, procurement and on-site support. | NVIDIA launches a managed Isaac cloud with Naver or KT plus its own SI partners. Mitigation: move our value into data, content and services. |
| **Chaebol in-housing** (Samsung SDS, Hyundai AutoEver, SK AX, HD Hyundai) | 50k GPUs each (U); group-internal twins | We sell *to* their SIs as a component; their supplier networks cannot build in-house; our asset library is neutral across groups. | A group mandates internal-only tools. We then target tier-1 and tier-2 suppliers through vouchers. |
| **MORAI** | AV, UAM, maritime; strong government ties | We do manipulation, humanoids and factories, where MORAI has limited robot RL. We partner on AV data. | Maritime overlaps; we differentiate with neural reconstruction plus robot learning. |
| **Applied Intuition** | AV and defence toolchain ($15B valuation, medium confidence) | We avoid AV HIL, and they have no Korean factory presence | Their defence expansion into Korea |
| **Lightwheel** | SimReady assets (free only for non-commercial use), aligned with Isaac Arena | Commercially licensed assets, Korean industrial SKUs, sovereign on-prem delivery and Korean trust | A Korean office or capital advantage. Option: make them a reseller partner. |
| **Genesis AI** | Open engine and its own foundation model (GENE-26.5); Nyx renderer is closed | Enterprise delivery and RTX sensor fidelity; we use Genesis as our hedge adapter | Its ROCm/Metal portability if NVIDIA supply tightens |
| **CyLab, E8, VIRNECT** | Domestic synthetic data and twins (CyLab is an NVIDIA partner) | Physics, RL and VLA training, not just images | Price competition on simple SDG |
| **Chinese data factories** | Near-zero-price assets and data | Trust barrier for defence, chaebol and US-linked buyers | Generic asset prices |

**The moat, most durable first:**
1. A compounding library of **Korean physical data**: Real2Sim assets and environments with measured fidelity, plus paired real/sim datasets with gap scores. Each PoC adds rights-cleared content.
2. **Workflow embedding**: customer USD repositories, lineage, run manifests and a Korean-language agent.
3. **Distribution**: NVIDIA co-selling, SI resale, and government consortia and vouchers.
4. **Sovereign compliance**: ISMS-P, CSAP, OEM on-prem rights and a defence SKU.
5. **Speed**: a 12–18-month lead in Korean reference deployments.

None of these is a technology moat. Speed is what this angle sells, and it decays if we are slow.

---

## 11. Top risks and mitigations

| # | Risk | Likelihood / impact | Mitigation |
|---|---|---|---|
| 1 | **NVIDIA terms for hosted SaaS, on-prem redistribution, asset resale and telemetry are unverified.** The "outputs-only" exemption is itself (U). | High / High | Deliver outputs only, from our own GPUs, in P0–P1. Request written terms in week 1. Budget NVAIE at list price. Offer BYO-NVAIE. No hosted GA before written terms (M10 gate). Keep a Kit-less Newton/mjlab SaaS fallback. |
| 2 | **ovrtx is proprietary and alpha; the ovphysx pip binary is proprietary and alpha** (its source is Apache-2.0) | Medium / Medium | Neither is on the GA critical path; Isaac Sim 6.1 headless is the runtime. Adopt them only after production release and written terms. |
| 3 | **Hunyuan3D 2.1 excludes Korea, including use of its outputs** | High if used / High | CI blocks the dependency and known weight hashes. Use TRELLIS.2 with nvdiffrast replaced, SAM 3D (non-defence only) and VGGT-1B-Commercial. |
| 4 | **Non-commercial research code** (Inria 3DGS family, Instant-NGP, nvdiffrast, MimicGen, ManiSkill assets, GO-1, RLDX-1; openpi weight terms unstated) | High / High | SPDX scanning and the deny list from §3. Audit CEN's NeRF code in month 1 for Instant-NGP. Clean-room in-house meshing. Pin cuRobo to its Apache tag. |
| 5 | **Wrong GPU class:** H100/H200/B200 have no RT cores, and government allocations are B200/H200 | High / High | Separate pools in the scheduler. Buy 24 RTX PRO 6000 early. Verify Korean cloud RTX supply by M2. Price sessions on whole GPUs, because RTX PRO 6000 MIG is (U). Use R580+ driver images. |
| 6 | **API churn** (Isaac Lab 3.0 quaternion and ProxyArray changes, Kit major versions, Isaac Sim 7.0) | High / Medium | Release trains, an adapter layer with a cross-backend conformance suite in CI, 20% capacity reserve, NVIDIA early access |
| 7 | **Streaming has no authentication or encryption** | High / High | Our own gateway, no host-network exposure, no cross-tenant GPU sharing, penetration test before GA |
| 8 | **NVIDIA channel conflict and commoditisation** (usd-content-agents, free blueprints) | Medium / High | Position as the partner that grows GPU usage; shift value to data and services; review strategy if NVIDIA launches a managed Isaac cloud in Korea |
| 9 | **Chaebol in-housing** | High / Medium | SI resale, BYOL, supplier-network focus |
| 10 | **Fidelity liability** (GAUGE: no engine uniformly faithful (U)) | Medium / High | Contract acceptance tied to Scorecard metrics, a real calibration lab, per-asset fidelity scores |
| 11 | **Defence and export controls:** the SAM License bars ITAR uses; VGGT-Commercial bars military use; air-gapped delivery counts as distribution (GPL, Kit terms); US EAR applies | Medium / High | A separate defence SKU bill of materials, legal screening, no GPL components on-prem |
| 12 | **ROS 2 Lyrical is unsupported by Isaac Sim; Pegasus is still on Isaac Sim 5.1** | Medium / Low | Zenoh/DDS bridges; drones deferred to P3 |
| 13 | **Funding and policy cycle** (R&D budgets swing; matching funds required) | Medium / High | M10 gate, raise by M9–12, treat grants as upside |

**Items to verify within 60 days:**
- NVIDIA licensing: hosting, OEM and NuRec terms; the NVAIE price and Inception discount.
- GPU supply: Korean cloud RTX PRO 6000/L40S availability and price; eligibility for government GPU programmes.
- Market and funding context: the 260k-GPU deal and chaebol cluster details; 2027 TIPS and voucher calls.
- Costs and technical claims: KRW salary bands; RTX PRO 6000 MIG profiles.
- Pending component terms: openpi and OceanSim licences; Isaac Lab 3.0 GA date.

---

## 12. KPIs per phase

| Phase | Technical KPIs | Business KPIs |
|---|---|---|
| **P0 (M0–4)** | 3 templates run end-to-end in CEN; RTX session start ≤90 s and RTT ≤80 ms from Seoul; SDG ≥10 RTX 1080p images/s/GPU (A, to be measured); Agent completes ≥85% of 20 scripted Korean commands; 100% of dependencies SPDX-tagged, 0 deny-list hits | ≥1 paid PoC (≥₩1.5억) signed and invoiced; 3 LOIs; 15 qualified accounts; NVIDIA terms requested in week 1; TIPS operator secured |
| **P1 (M4–10)** | Sim-to-real gap ≤10 pp on 3 manipulation tasks; synthetic-only detector ≥90% of real-data mAP, and synthetic plus 10% real ≥100%; Forge turns phone video into a SimReady asset in ≤30 min with ≥90% physics-QA pass; measured RL cost ≤$10 per 1B steps; conformance suite green across PhysX, Newton and MuJoCo | ≥3 PoCs (target 5), 2 annual conversions; ₩15억 bookings; ARR ₩8억; 100 certified assets; 30 paid Pro seats; NPN listing; written NVIDIA terms; PoC gross margin ≥40% |
| **P2 (M10–18)** | Live twin ≥30 Hz across 200 assets; fork-from-live throughput prediction error ≤10%; 50-robot AMR fleet at real-time factor ≥1.0; humanoid real-world success ≥70% on 3 tasks; on-prem install ≤5 days; 99.5% uptime | ARR ₩30억; 10 enterprise logos (2 chaebol groups); 1 on-prem; marketplace GMV ₩3억; token gross margin ≥50%; net revenue retention ≥120% |
| **P3 (M18–27)** | Marine perception synthetic-to-real mAP ratio ≥0.9; 500 COLREG scenarios; off-road co-simulation real-time factor ≥1.0; air-gapped SKU passes a customer security audit; world-model evaluation rank correlation ≥0.8 with real outcomes | ARR ₩60억; 1 shipbuilder production programme; 1 defence contract; 1 Japanese customer; 1,000+ certified assets |
| **P4 (M27–36)** | Arena hosts ≥5 humanoid models; field failure to fix ≤48 h; ≥2,000 assets with fidelity scores | ARR ₩130–150억; FY2029 revenue ₩190억; ≥55% recurring; US entity live; break-even path in 2030 |

**Bottom line:** adopt NVIDIA's runtime now, pay for the licences formally, own the Korean data, delivery and agent layers, and land the first paid PoC by February 2027. Hold a hard M10 gate (written NVIDIA terms plus at least 3 paid PoCs) before scaling past 27 people.

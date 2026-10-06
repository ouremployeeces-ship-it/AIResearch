# CEN Forge & Proof: An Outcome-Led Physical-AI Data and Evaluation Factory
**Strategic angle C: "Outcome-led Physical-AI Data & Evaluation Factory" · Status date 2026-10-06 · M1 = November 2026 · FX 1 USD = ₩1,400 [A]**

Tags: **[A]** is a planning assumption made by this proposal. **[U]** is a research claim that could not be checked against a primary source; it must be re-verified before money is committed. Untagged facts were verified on GitHub, PyPI or the SkyPilot price catalog in the research digest. Where the fact-check corrected a claim, this document uses the corrected version.

---

## 1. Thesis

In 2026 the simulator became free: Newton 1.6.1, MuJoCo 3.15, the PhysX 5.11 SDK, Isaac Lab 3.0 and Cosmos 3 are open and release often, and NVIDIA even open-sources SimReady authoring agents. What nobody gives away is **evidence that a robot will work**: twins with physics measured against the real object, data with measured transfer to real cameras, and policies with measured success in a real cell. AICHEMIST should therefore sell no simulator seats and instead run a **Physical-AI Data & Evaluation Factory** that sells four outcomes, each with a measured fidelity score: certified SimReady twins, synthetic multimodal datasets, trained policies, and sim-to-real evaluation and certification. The platform is built inside-out: it first runs AICHEMIST's own factory, and each production line becomes a self-serve CEN product only once it is automated and profitable. The moat is the **Real2Sim Forge** (CEN's NeRF pipeline rebuilt on Apache-licensed Gaussian splatting) plus a growing corpus of paired real/sim measurements, which the CEN marketplace turns into a network effect.

**Investor sentence:** *"NVIDIA gives the simulator away. AICHEMIST sells what comes out of it (twins, data and robot skills, each with a measured sim-to-real score) and runs the arena where Korea's robots get graded."*

**How the four hard requirements are met:**

| Requirement | How this plan meets it |
|---|---|
| (1) Powerful physics | Newton/MJWarp, PhysX 5.11 and MuJoCo 3.15 behind one adapter; quality comes from **calibration against our own measurements**, not engine authorship. |
| (2) Real-world similarity | Real2Sim splats remove the site gap; mass, friction and sensor profiles are lab-measured; every delivery ships a Sim2Real Gap Scorecard. |
| (3) Ease of use | Customers order outcomes in Korean via the Outcome Console and LLM/MCP layer; self-serve lines open only once they run untouched by our engineers. |
| (4) Built-in training | Isaac Lab 3.0, LeRobot 0.6.1 and GR00T N1.7/SmolVLA run as factory lines (RL, IL, VLA, perception), proven in closed-loop sim plus real cells. |

### Why this angle, and where it is weak
**For:**
1. **It sidesteps the biggest open question.** NVIDIA's terms for hosting Kit/Isaac Sim as multi-tenant SaaS are not in writing, but selling outputs reportedly needs no NVIDIA AI Enterprise (NVAIE) licence [U]. Our Phase 0–1 revenue is outputs-only, and even the worst case (NVAIE on 16–32 internal RT GPUs at the ~$4,500/GPU/yr list [U]) costs about ₩1–2억 a year.
2. **Customers buy results.** Korean robot makers have thin simulation and RL teams and churn from seats they cannot use; a dataset sold with an mAP acceptance test does not have that problem.
3. **Commoditization becomes a tailwind:** every free NVIDIA or DeepMind release lowers our cost per outcome.
4. **Evaluation is the stickiest position**, and regulation is starting to require simulation credibility (UN ADS regulation, ISO 34505, the AI Basic Act [U]).

**Against (stated plainly):**
1. **Services gravity.** Outcome contracts look like SI work; gross margin starts near 45% [A], and without the productization gate (§6) we become a body shop.
2. **Outcome liability.** Success depends on customer hardware and lighting we do not control, so acceptance must be defined in a certified cell or a written protocol.
3. **It costs more than a pure platform plan:** about ₩121억 over 24 months against ₩80–85억 for the research team's ramped hybrid, because of test cells, capture operations and forward-deployed engineers.
4. **Conflict of interest.** We both sell policies and grade them; without a governance firewall and a third-party co-signer the Arena has no credibility.
5. **Self-serve arrives late (M13+)**, possibly after NVIDIA or Lightwheel ship hosted SimReady tooling.
6. **Paired real data is hard to get.** The moat compounds only if customers let us measure, so data rights become a gating sales item.

---

## 2. Engine and stack decision per layer

Selection rule: pick what makes the **factory** fast, measurable and reproducible today, and keep every path that will face tenants licence-clean so it can be productized later.

| Layer | Choice (version, Oct 2026) | Licence | Why (factory lens) | Fallback |
|---|---|---|---|---|
| **Physics: robots** | **Newton 1.6.1** (2026-10-05): MJWarp solver by default, Kamino for closed loops, SDF plus hydroelastic contact for insertion. **PhysX 5.11 via Isaac Lab 3.0** for parity with customers' Isaac setups. **MuJoCo 3.15 CPU** (float64, deterministic) as the *certification replay* backend. | Apache-2.0 (Newton, MuJoCo, MJWarp, PhysX SDK core) | RL/IL throughput. Deterministic replay (MuJoCo CPU; Newton deterministic paths since v1.4) makes certificates auditable; MJWarp is float32 and GPU-non-deterministic, so no certificate depends on it. | mjlab 1.6.0; Genesis World 1.4.3 as the only non-CUDA hedge |
| **Physics: vehicles, terrain, marine** | PhysX vehicles for yard tugs and AMRs. **Chrono 10.0** for tyres, SCM/CRM terramechanics and SPH fluid-structure interaction (Phase 3). In-house Fossen 6-DOF and wave-spectrum Warp kernel (Phase 3). FMI 3.0 adapter for customers' CarSim/CarMaker. | BSD-3; own; open standard | We sell vehicle *perception data and evaluation*, not dynamics validation. Chrono is the best open terramechanics; marine has no incumbent. | BeamNG.tech (by quote); customer FMUs. Avoid GPL-3 Stonefish. |
| **Deformables and fluids** | Newton VBD (polybags, cables, cloth), Style3D, ImplicitMPM (granular); MuJoCo 3.15 Stable Neo-Hookean flex; Chrono SPH for water | Apache-2.0 / BSD-3 | Logistics is full of polybags and cartons, and deformables show the largest gaps (GAUGE [U]), so we measure before guaranteeing. | Genesis IPC; in-house PhysTwin-style spring-mass fit |
| **Rendering tiers** | **R0** browser WebGPU (three.js r186 + Spark 2.0, PlayCanvas 2.23) for review. **R1** Isaac Sim 6.1 RTX real-time *inside the factory* for SDG. **R2** RTX path tracing for gold validation sets. **R3** Newton GL for RL debugging. ovrtx (alpha) evaluated once GA and licensed. | Web MIT/Apache; Kit, RTX, ovrtx NVIDIA proprietary | Top camera/lidar/radar fidelity where it pays, on outputs; reviewers use no server GPU. | Blender Cycles offline (internal tool); raster SDG |
| **Neural realism** | **gsplat 1.6.0, 3DGRUT 2.0** (3DGUT) for the Forge; **fVDB Reality Capture** for sites; NuRec USDZ import/export. **Cosmos Transfer 2.5** now, **Cosmos 3 Nano 16B** fine-tune from M9 for label-preserving augmentation; Cosmos 3 policy pre-screening in Phase 3. | Apache-2.0; Cosmos 3 OpenMDW-1.1; Transfer 2.5 weights NVIDIA Open Model License; NuRec terms [U] | Splats remove the site gap. World models add appearance diversity but not trustworthy physics or labels, so every augmented frame passes an automatic label-consistency check. | Domain randomization only |
| **Sensor simulation** | Isaac Sim RTX camera with PPISP, RTX lidar/radar, IMU noise, TacSL tactile, plus **our measured sensor profiles** (camera chart, lidar range/intensity, noise PSD) per sensor SKU; OSI 3.7 export for vehicles | NVIDIA runtime (internal); profiles ours | Fidelity is measured, not asserted, and profiles are sellable marketplace items. | Warp ray-cast lidar, raster camera and our ISP model for self-serve |
| **Scene format** | **OpenUSD** (26.08 tooling; Isaac Sim 6.1's bundled USD at runtime); UsdPhysics with newton/mjc/physx schemas; UsdSemantics; glTF + KHR_gaussian_splatting (ratified) for web; URDF/MJCF via Apache converters; MCAP; LeRobotDataset v3; **own `aic:TwinCertificate` schema** + JSON sidecar | AOUSD Core 1.0.1 (CC-BY-ND spec); converters Apache-2.0 | One stage carries geometry, physics, splats, labels *and* the certificate. | USD is the hedge |
| **Training** | **Isaac Lab 3.0** (EA 2026-09-16, bundles Newton 1.5.2; pin GA, targeted end-Oct 2026) with rsl_rl 5.5.1 and skrl 2.1; Isaac Lab Mimic (10 demos to 1,000); **LeRobot 0.6.1**; VLAs GR00T N1.7 (humanoid, bimanual) and SmolVLA 450M, pi0.5 blocked until weight terms are confirmed; RF-DETR N–L; **Isaac Lab Arena v0.3** (alpha) as harness base; ONNX to TensorRT/Jetson | BSD-3/Apache/MIT; GR00T weights NVIDIA Open Model License | Mature, free, and what customers' engineers know. We differentiate on inputs (twins, data) and measured outputs. | mjlab + LeRobot (fully open) |
| **Web and streaming UX** | **Outcome Console** (order, review, accept) plus the CEN workspace; WebGPU by default; WebRTC streaming only for RTX review, behind our own auth/TLS gateway (Isaac Sim streaming has none); Selkies for the CEN desktop | Ours; Selkies MPL-2.0 | Customers review outcomes rather than author scenes; client-side rendering keeps COGS proportional. | Rendered videos of acceptance runs |
| **Orchestration and infrastructure** | K8s 1.32+, GPU Operator v26.7.1, **KAI Scheduler v0.18.2**, Ray 2.59, SkyPilot burst, MLflow 3.x, optional OSMO; a **Run Manifest** on every job. Pools: **RT** (L40S/RTX PRO 6000, driver R580+), **TRAIN** (H100/H200/B200 incl. government), **LIGHT** (L4/CPU). | Apache-2.0 | The factory is a batch pipeline; gang scheduling and spot burst drive cost per outcome. Multi-tenant hardening is deferred to Phase 2. | Kueue/KubeRay; Slurm via Slinky |

---

## 3. Build-vs-buy map

| Decision | Components |
|---|---|
| **OWN** (about 65% of engineering) | **Real2Sim Forge** (orchestration, in-house articulation and physical-parameter models, physics QA, certificate generator). **Fidelity Lab** (protocols, real test cells, paired real/sim corpus, Sim2Real Gap Scorecard). **K-Physical AI Arena** (task suites, real cells, leaderboard, governance). **Outcome Orchestrator** (order spec, job DAG, QA gates, Run Manifest, lineage). Thin **Sim Kernel / Renderer API** with conformance suite. **Licence & Provenance Registry** (SPDX for code; rights for assets, data, weights). Korean LLM/MCP agent; Korean content library and sensor profiles; token metering. Small Warp kernels (tactile, sensor noise, Fossen marine), upstreamed when generic. |
| **INTEGRATE** (open source, pinned) | Newton, MuJoCo/MJWarp, PhysX SDK 5.11, Isaac Lab 3.0, mjlab, Chrono 10, gsplat, 3DGRUT, fVDB, VGGT-1B-Commercial, MapAnything (Apache variant), Depth Anything 3 Small/Base/Metric, TRELLIS.2 (with nvdiffrast replaced), SAM 3D Objects (civil use only), Articulate-Anything, CoACD/CuACD, LeRobot, rsl_rl, skrl, RF-DETR N–L, Cosmos 3 / Transfer 2.5, OpenUSD, KAI, Ray, open62541, MCAP |
| **LICENSE** | Isaac Sim 6.1 / Kit RTX for internal factory use (NVAIE only if NVIDIA requires it for outputs); ovrtx and NuRec once terms permit; customer-owned CarSim/CarMaker/FTire via FMI; Ultralytics Enterprise only if a customer mandates YOLO. |
| **PARTNER** | NVIDIA (Inception, co-selling, written terms); robot OEMs (Doosan, Rainbow) for cell hardware and channel; a testing body (KTL, KIRIA or TTA [A]) as Arena co-signer; MORAI for AV; group IT arms (Samsung SDS, LG CNS, Hyundai AutoEver) as resellers; Korean clouds for Seoul RT capacity; KAIST/SNU/ETRI for IITP consortia. |
| **NEVER USE** (verified licence traps) | Hunyuan3D 2.1 (its licence excludes South Korea, including outputs). Inria 3DGS and its derivatives (2DGS, MILo), PGSR, Instant-NGP and nvdiffrast. MimicGen/DexMimicGen code. PhysX-Anything (S-Lab). ManiSkill assets, AgiBot World/GO-1, RLDX-1 weights, DA3 Large/Giant, the original VGGT-1B, Waymax/WOD. Ultralytics AGPL in SaaS. GPL-3 BlenderProc or Stonefish in anything shipped on-prem. lakeFS ≥1.87 (BSL) embedded. SAM 3D in the defense edition (the SAM License restricts military and ITAR uses). The cuRobo bundled with Isaac Lab (pin an Apache-tagged upstream release instead). |

**Do we build our own physics engine or renderer? No.**
- **History.** MuJoCo spent about a decade at Roboti before DeepMind bought it (2021). Newton needed NVIDIA, DeepMind and Disney plus years of Warp/MuJoCo code to reach 1.0 on 2026-03-10, and has shipped six minor versions since. Chrono and Drake are multi-decade codebases (about 20k and 35k commits).
- **Cost.** 150–300 engineer-years (₩400–600억) and 30–48+ months to an MVP; "build" scored 2.40 against 4.23 for the hybrid in the research decision matrix.
- **Decisive for this angle.** GAUGE [U] found no engine uniformly faithful to reality. Fidelity is a *calibration and measurement* problem, and measurement is what we own; a home-grown engine would be less faithful *and* unmeasured.
- **Renderer.** Isaac RTX already renders camera, lidar and radar in one USD stage, and 3DGUT is Apache-2.0. Our own path tracer would add nothing a customer pays for.

---

## 4. Beachhead verticals and sequencing

Scores run from 1 to 5 [A]. "Outcome measurability" asks how fast a delivered outcome can be scored against reality; it is the criterion this angle adds.

| Vertical | KR demand | Open field | Anchors | Forge/CEN fit | Time to revenue | Outcome measurability | Total /30 | Wave |
|---|---|---|---|---|---|---|---|---|
| **Object-rich manipulation:** logistics picking, depalletizing, kitting, inspection | 4 | 4 | 4 | 5 | 5 | 5 | **27** | **1** |
| **Humanoid and dual-arm evaluation + VLA data** | 4 | 4 | 4 | 4 | 3 | 5 | **24** | **2** |
| Factory-cell manipulation (assembly, welding) | 4 | 3 | 4 | 4 | 4 | 4 | 23 | Rides on wave 1 |
| **Shipyard, port and maritime perception** | 5 | 4 | 3 | 3 | 2 | 3 | **20** | **3** |
| Defense UGV/drone data (air-gapped) | 4 | 3 | 2 | 3 | 1 | 3 | 16 | Inside wave 3 |
| AV/ADAS | 4 | 1 | 3 | 3 | 2 | 3 | 16 | Data only, via MORAI |
| Quadrupeds | 2 | 1 | 2 | 2 | 3 | 3 | 13 | Template only |

**Wave 1 (M1–M15): "Pick Anything, Korea."**
- *Why it compounds:* the Forge's unit of work is the object, and logistics involves thousands of SKUs, so an asset scanned for one customer (a Korean ramen carton for a 3PL) is resold to the next (a robot OEM). Outcomes are scored in hours: real-image mAP, or pick success per 1,000 attempts.
- *Demand:* e-commerce/3PL automation (CJ Logistics, Coupang, Hyundai Glovis [A: not validated]); robot OEMs needing pick skills (Doosan Robotics already integrates Isaac and cuRobo; Rainbow Robotics ~35% Samsung-owned [U]); SME factories via AI and Data vouchers.
- *Competition:* Lightwheel's SimReady assets are free only for non-commercial use and its footprint is US/China; CyLab sells data without physics or policies; no Korean SKU library exists.
- *CEN fit and timing:* the highest fit, since NeRF photo-to-3D *is* object capture and CEN SDG already sells perception data. Datasets sell in M2–M4 (voucher-funded); policy PoCs in M6–M9.

**Wave 2 (M9–M24): K-Physical AI Arena plus humanoid and dual-arm VLA data.**
- *Demand:* Korean humanoid makers (K-Humanoid Alliance, April 2025 [U]; HMG/Boston Dynamics, Samsung/Rainbow, LG, RLWRLD) need neutral evaluation and long-tail demonstration data; evaluation is sticky and government-fundable. Wave-1 cells become the first Arena cells.
- *Competition:* Lightwheel's LW-BenchHub (268 tasks) is sim-only, and RoboArena is academic and DROID-only. No neutral Korean arena with real cells exists.
- *Time to revenue:* M12–M15, through KEIT/NIA consortia and Arena memberships.

**Wave 3 (M20–M36): shipyard, port and maritime perception, plus a defense air-gapped edition.**
- *Demand:* the largest Korea-unique white space. The Autonomous Ship Act took effect on 3 Jan 2025; Avikus runs on about 350 vessels, alongside SHI's SAS and Hanwha Ocean; marine simulation has no commercial leader. Offer: EO/IR, marine-radar, sea-state and COLREG datasets plus shipyard cell twins reusing wave 1.
- *Why third:* it needs Fossen dynamics, radar/EO-IR profiles and on-prem packaging (distribution, which triggers licensing duties), and sales cycles run 12–24 months.

**AV/ADAS:** we build no simulator. Korean road perception packs are sold only through the marketplace and MORAI.

---

## 5. Architecture sketch

```
SURFACES   Outcome Console | CEN Workspace (Jupyter / virtual OS) | Marketplace | Arena Leaderboard | SDK·REST·MCP
AGENTS     Korean LLM command layer -> first-party MCP server (typed tools) -> sandboxed USD code agent -> validation gates
ORCHESTR.  Outcome Orchestrator: order spec -> job DAG -> QA gates -> delivery + certificate | token metering | Run Manifest
FACTORY    [FORGE line]           [DATA line]              [SKILL line]             [PROOF line]
LINES      capture -> SimReady    SDG + augmentation       RL / IL / VLA            deterministic sim eval + real-cell
           asset + certificate    + label QA               + sim2sim gate           trials + scorecard + Arena
SIM KERNEL physics: Newton | MuJoCo-CPU | PhysX/Isaac Lab | Chrono | FMU     render: Isaac RTX | ovrtx* | Newton GL | web
           measured sensor profiles                                                                    (*after GA + terms)
TWIN/SCENE OpenUSD stage service | scene commits & branches | aic:TwinCertificate | live session layer
DATA       object store | Postgres | Kafka | TSDB | MCAP | LeRobot v3 | Iceberg | Licence & Provenance Registry
           PAIRED REAL/SIM MEASUREMENT CORPUS (the moat)
INFRA      K8s + KAI: RT pool (L40S / RTX PRO 6000) | TRAIN pool (H100/H200/B200 + gov) | LIGHT pool | LAB EDGE (test cells)
```

**Forge flow:** phone/robot video (optional lidar) → anonymization (faces, plates, customer IP) → poses and metric depth (VGGT-1B-Commercial, MapAnything, DA3-Metric) → 3DGUT splat (gsplat/3DGRUT) → surface mesh (gsplat 2DGS mode, fVDB, clean-room PGSR/MILo ideas) → generative completion (TRELLIS.2 without nvdiffrast; SAM 3D for clutter) → articulation (Articulate-Anything baseline plus our model) → CuACD hulls (~0.25 s/mesh) → VLM mass/friction priors → **measured refinement** (scale, inclined plane, push/drop video sysid with MuJoCo's toolbox) → physics QA on Newton and MuJoCo → SimReady USD + MJCF/URDF + glTF/splat with a certificate tier: **Bronze** (VLM-estimated), **Silver** (video-identified) or **Gold** (lab-measured).

**Outcome flow:** order → scene assembled from marketplace assets plus the customer's site twin → DATA and/or SKILL line → PROOF line (deterministic replay plus real cells) → delivery of dataset or policy with scorecard, Run Manifest and licence manifest.

**Proof loop (what compounds):** every real trial adds paired sim/real data, which recalibrates Forge priors, sensor profiles and the fidelity predictor that sets our prices and guarantees.

**Simulation twin vs live twin:**
- The **simulation twin** is the default product: headless, batched, faster than real time, branched from a scene commit, and replayed deterministically for certification.
- The **live twin** is a measurement instrument, not a general IIoT platform. Telemetry from customer cells (ROS 2 Humble/Jazzy/Lyrical bridges and Zenoh, OPC UA via open62541, MQTT) flows through Kafka and a twin-state service into a USD live session layer (10–60 Hz) and a time-series DB.
- It serves (a) acceptance monitoring of deployed skills, (b) failure mining (field failure → new scenario → retrain → gated redeploy) and (c) fidelity drift (fork from live, predict, compare with later live data).
- Siemens, AVEVA and Dassault PLM twins connect through OPC UA and USD; we do not replace them.

**Agent layer:**
- A Korean-language LLM drives a first-party MCP server (spec 2026-07-28) with typed tools: `asset.search/certify`, `scene.apply_ops`, `sdg.generate`, `skill.train`, `eval.run`, `cert.issue`, `order.quote`.
- A USD code-generating agent runs in a gVisor/Kata sandbox behind UsdValidation, physics sanity checks and a backend smoke test; a human approves every merge. Community MCPs that execute arbitrary code are never exposed to tenants.
- It is built **for our own delivery engineers first** (target: half the engineer-hours per outcome by M12), then exposed to customers.

**Marketplace and asset pipeline:**
- Every listing carries a licence manifest, provenance (capture source, consent, anonymization) and a certificate tier; datasets also carry Run Manifests. Third parties list Forge-certified assets on a 75/25 split, and non-commercial items are blocked automatically in commercial workspaces.

---

## 6. Phased roadmap (36 months)

**Productization gate.** A factory line opens to self-serve only when all three conditions hold:
1. at least 80% of its internal jobs finish with no engineer touching them;
2. internal gross margin on the line is at least 60%;
3. every component in the line has a written licence basis for tenant use.

| Phase | Deliverables | Exit criteria | Demo |
|---|---|---|---|
| **P0 Factory Zero** (M1–M4, Nov 2026–Feb 2027) | Licence audit of CEN's NeRF pipeline and migration to gsplat/3DGRUT; written-terms request to NVIDIA (outputs, hosting, on-prem); 6–8-week physics bake-off (Newton/MJWarp vs PhysX vs MuJoCo CPU) on bin pick, depalletize, polybag pick, drawer opening, peg insertion; Forge v0 (rigid); Test Cell 1 (cobot, bin, 3 cameras, F/T sensor) with measurement protocol; Run Manifest and licence registry v0; 3 dataset contracts; TIPS operator secured | 300 Korean SKUs at Silver/Gold; synthetic-only detector ≥85% of real-trained mAP on a held-out real set; 100% deterministic replay of certificate tests | M4: **"Phone video to robot pick in 48 hours"** |
| **P1 Outcome MVP** (M5–M12, Mar–Oct 2027) | Forge v1 (articulated objects, VBD polybags); DATA line with Cosmos augmentation and label QA; SKILL line (grasp RL, Mimic + SmolVLA/GR00T fine-tunes, Jetson export); Outcome Orchestrator v1; Test Cell 2; Arena v0 (25 sim tasks, 2 real cells, internal); marketplace "Certified" tier; internal MCP agent | 2,000 certified assets; 3 paying outcome customers, ≥1 on a production (non-PoC) contract; gap ≤15 pp on 3 pick tasks; engineer-hours per outcome −50% vs P0 | M12: public **"K-Pick Challenge"** scoring three robot OEMs' policies in sim and real cells |
| **P2 Productize & Arena** (M13–M24, Nov 2027–Oct 2028) | Self-serve FORGE and DATA lines (if gated in); self-serve training templates; **Arena v1** with humanoid/dual-arm track, co-signing testing body and governance charter; humanoid cell; VLA data packs (Mimic + teleop); live-twin flywheel; on-prem "Factory-in-a-box" (open stack, RTX only under customer licence); MIG tenancy and ISMS-P; Japan PoC; GS certification | 10,000 assets (≥30% third-party); gap ≤10 pp on 5 tasks; sim/real r ≥0.8 over ≥5 policies; ≥30% recurring revenue; 8 Arena members | M18: Arena v1 launch with three humanoid makers. M24: self-serve "video in, certified twin and pick skill out, same day" |
| **P3 Scale & new domains** (M25–M36, Nov 2028–Oct 2029) | Maritime/shipyard perception packs; air-gapped defense edition (no SAM, no GPL, no Kit unless customer-licensed); Chrono and Fossen modules; Cosmos 3 policy pre-screening; self-serve SKILL line; US landing via Korean OEM plants | ₩95억 run-rate, ≥50% recurring; ≥1 procurement programme citing the Arena certificate; 50,000 assets; 3 verticals live | M30: maritime pack validated on a real vessel log. M36: Arena certificate accepted in a chaebol or government procurement |

---

## 7. Team and effort split

Headcount at the end of each phase (FTE):

| Function | P0 | P1 | P2 | P3 | Owner |
|---|---|---|---|---|---|
| Leadership: CTO/sim architect, **Head of Fidelity & Evaluation**, product lead | 3 | 3 | 3 | 4 | CEO |
| Forge: neural reconstruction, geometry/SimReady, generative 3D and articulation ML | 3 | 5 | 6 | 7 | Forge lead |
| Capture and lab operations (capture technicians, robot technicians) | 1 | 2 | 4 | 5 | Head of Fidelity |
| Fidelity science and Arena (sim2real scientists, metrics, system ID) | 1 | 2 | 3 | 4 | Head of Fidelity |
| Sim kernel and physics integration (conformance, Warp kernels) | 1 | 2 | 3 | 3 | CTO |
| Sensors, rendering and SDG | 1 | 2 | 3 | 3 | CTO |
| SKILL line: RL, IL and VLA | 1 | 3 | 4 | 5 | Skill lead |
| Platform, MLOps, infrastructure and security | 1 | 2 | 3 | 4 | Platform lead |
| Web/UX, agent/MCP and marketplace | 0 | 1 | 2 | 3 | Product lead |
| Forward-deployed solutions engineers | 1 | 1 | 2 | 3 | CEO |
| BD, partnerships, grants and licensing/legal | 1 | 1 | 1 | 2 | CEO |
| Marine and vehicle (Chrono, Fossen, radar) | 0 | 0 | 0 | 2 | CTO |
| **Total** | **14** | **24** | **34** | **45** | |

**Effort split (engineering time, P1–P2):** about **40% on the moat** (Forge, Fidelity, Arena); 20% on the DATA and SKILL lines; 20% on orchestration, UX and the agent; 10–15% reserved as an "upgrade tax" for pinning, conformance and API churn (the research warns unmanaged churn eats 20–30%); about 10% on delivery.

Phase 0 deliberately has almost no web or multi-tenant engineering. The internal factory does not need it, and that is the main saving this angle buys.

**Hiring order:**
1. **Head of Fidelity & Evaluation**: a sim2real scientist who has run a real-robot lab. The angle stands or falls on this hire.
2. CTO/sim architect (OpenUSD, Isaac Lab, Newton).
3. Neural-reconstruction lead, who migrates the CEN NeRF pipeline.
4. Robot lab technician and capture technician.
5. RL/IL engineer for pick skills.
6. Forward-deployed engineer with a Korean manufacturing background.
7. MLOps/K8s engineer.
8. Generative-3D/articulation ML engineer.

A part-time licensing counsel is on contract from M1. Later hires: VLA and sensor engineers (M6), web and agent engineers (M8), an Arena programme manager (M10), marine engineers (M24).

---

## 8. 24-month budget (M1–M24, KRW)

**Assumptions [A]:**
- Average headcount is 12, 20 and 30 across P0 (4 months), P1 (8 months) and P2 (12 months), which gives **568 head-months**.
- The blended fully loaded cost is **₩1,400만 per head-month**. The research mid-case is ₩1,495만 for an all-engineer team; ours is lower because about 20% of the team are technicians and operations staff. Salary bands are low confidence.
- Blended GPU costs are $1.9 per RT GPU-hour and $3.5 per TRAIN GPU-hour. These sit between RunPod (L40S $1.09, RTX PRO 6000 $2.09, H100 $2.89–3.49) and AWS Seoul (L40S $2.288, RTX PRO 6000 $4.135), which is 23–38% above us-east-1.
- Government B200/H200 allocations have **no RT cores**, so they offset TRAIN only and are not budgeted.

| Line | Basis | ₩억 |
|---|---|---|
| **People** | 568 head-months × ₩1,400만 | **79.5** |
| Compute: RT pool | Average of 8, 16 and 32 GPUs (P0/P1/P2) at 70% utilization ≈ 278k GPU-h × $1.9 | 7.4 |
| Compute: TRAIN pool (paid) | 2, 8 and 16 GPUs at 50% utilization ≈ 96k GPU-h × $3.5 | 4.7 |
| Compute: LIGHT pool, review streaming, CI | L4/CPU | 0.9 |
| Storage and egress | About 20M multimodal frames produced (~5.5 TB per 1M frames), 30% kept hot | 1.2 |
| **Compute subtotal** | Option: buy 2 × 8-GPU RTX PRO 6000 servers at M9 if RT utilization exceeds 60% | **14.2** |
| Licences | NVAIE/Omniverse reserve for 16 RT GPUs for 12 months at the $4,500 list price [U] (about ₩0.25억 at the reported Inception price [U]): 1.0. Developer and SaaS tools: 1.2. | 2.2 |
| Legal and certification | Licence counsel, data-rights contracts, ISMS-P/ISO 27001, GS certification, TTA/KTL test reports | 2.5 |
| **Fidelity Lab** (capex and opex) | 2 cobot test cells at ₩1.2억 each; humanoid/dual-arm cell (lease or partner) ₩2.0억; capture and measurement kits ₩1.0억; lab space ₩1.8억; consumables ₩0.5억 | 7.7 |
| GTM and G&A | Events and Arena launch ₩2.0억; travel and Japan PoC ₩1.0억; recruiting fees ₩1.5억; G&A ₩1.5억 | 6.0 |
| **Subtotal** | | **112.1** |
| Contingency (8%) | | 9.0 |
| **Gross 24-month total** | ≈ **$8.6M** | **≈121** |

**Funding logic.**
- 24-month revenue target: ₩57억 (Y1 ₩15억 + Y2 ₩42억, §9).
- Non-dilutive funding: about ₩30억 [A]. The research estimates ₩30–60억 if 4–6 applications succeed.
- Net equity need: about ₩34억. **Raise ₩60억 by M9** to cover collection lag and a buffer.
- **Phase 0 alone costs about ₩10억**, which is the CEO's real decision this quarter.
- *Lean variant (≈₩105억):* hold the team at 24 through M24, partner for the humanoid cell, cap the RT pool at 16 GPUs and halve event spend. Arena v1 slips to M24 and self-serve to M30.

---

## 9. Business model and pricing

Principle: **compute is sold near cost to drive usage; value is captured on outcomes and certificates.** There is no per-seat simulator licence, and viewer and reviewer seats are free and unlimited.

| Outcome | Done-for-you (enterprise) [A] | Self-serve in CEN [A] | Acceptance metric |
|---|---|---|---|
| **Certified SimReady twin** | Object ₩0.3–1.5M (Bronze to Gold); cell or site twin ₩30–150M | Forge conversion: 300 tokens (Bronze rigid), 1,500 tokens (Silver articulated) | Certificate tier; trajectory and rest-pose error thresholds |
| **Synthetic multimodal dataset** | Pack ₩50–200M with an acceptance test | 1 token per 100 RTX frames; storage and egress metered separately | Synthetic-only ≥ 90% of real-trained mAP, or synthetic + 10% real ≥ 100% real |
| **Trained or fine-tuned policy (skill)** | ₩150–500M per skill + runtime ₩3M per robot per year + retraining subscription | Training templates billed in GPU tokens | Real-cell success; gap ≤ 10–15 points |
| **Evaluation and certification** | Arena membership ₩30M/yr (startup) or ₩100M/yr (enterprise); campaign ₩20–60M per policy version | Sim-only evaluation in tokens | Success-rate confidence intervals, sim/real Pearson r, signed report |

**How it plugs into CEN:**
- **Tokens** [A]: 1 token = ₩100. An RT GPU-hour is 45 tokens (₩4,500 ≈ $3.2, against ~$1.9 cost); a TRAIN GPU-hour is 70 tokens (₩7,000 ≈ $5.0, against ~$3.5). Image prices stay above the research floors (RTX ≥ $0.0005, path-traced ≥ $0.005 per image), and storage/egress are metered separately because they exceed raster compute.
- **Subscriptions** [A]:
  - **Explorer** (free): web viewer, three Bronze Forge conversions a month, and a MuJoCo CPU sandbox.
  - **Builder:** ₩99,000 per workspace per month, including 1,000 tokens.
  - **Team:** ₩1.9M per month, including 25,000 tokens and a private marketplace.
  - **Enterprise VPC:** from ₩300M a year.
  - **Factory-in-a-box (on-prem):** ₩0.5–1.5B a year, within the research's indicative on-prem band of ₩0.3–1.5B.
- **Outcome credit.** 30% of every outcome contract's value is issued as CEN tokens valid for 12 months, so every delivered outcome seeds a self-serve account: the inside-out conversion mechanism.
- **Marketplace.**
  - Third-party certified assets sell on a 75/25 split.
  - Capture contributors, such as SME factories, earn royalties when their anonymized captures are reused, under explicit data-rights terms.
  - Customers who grant measurement rights get a 10–20% discount [A], which feeds the corpus.
- **Vouchers.** AI and Data Voucher work is delivered as outcome SKUs, so subsidized revenue builds both references and marketplace content.

**Revenue targets [A] (targets, not forecasts):**

| ₩억 | Y1 (M1–12) | Y2 (M13–24) | Y3 (M25–36) |
|---|---|---|---|
| Datasets | 6.5 | 11 | 18 |
| Twins (objects, cells, sites) | 2.5 | 6 | 11 |
| Skills (policies + runtime) | 5 | 14 | 25 |
| Evaluation and certification | 0.5 | 5 | 14 |
| CEN subscriptions, tokens, marketplace take | 0.5 | 6 | 27 |
| **Total** | **15** | **42** | **95** |
| Recurring share | ~10% | ~30% | ~50% |
| Blended gross margin | ~45% | ~52% | ~62% |
| Voucher- or government-funded share | ~60% | ~30% | ~15% |

Y3 downside and upside cases are ₩50억 and ₩130억. Break-even comes around M34 in the base case.

---

## 10. Moat

**What compounds:**
1. **Paired real/sim measurement corpus.** Every job adds measured trajectories, sensor statistics and real-cell outcomes; labless competitors cannot reproduce it, and NVIDIA runs no customer cells (target: 50,000 trials by M24).
2. **Certified asset library with two-sided network effects:** orders create assets, assets cut the next order's cost, contributors add assets for royalties.
3. **The Arena as a Korean standard:** neutral grading is a role no OEM or chaebol can play for its rivals.
4. **Cost-per-outcome learning curve:** automation plus the agent target −50% a year.
5. **Trust:** Korean enterprise relationships, on-prem delivery, licence-clean provenance.

| Competitor | Their play | Our answer |
|---|---|---|
| **NVIDIA** | Free engines, Cosmos, NuRec, usd-content-agents, blueprints; sells GPUs | Their releases cut our COGS (adopted within 30 days). They sell no measured, rights-cleared Korean content or neutral certification; we co-sell via Inception. If they launch a measured SimReady marketplace, we answer with Gold lab-measured tiers and real-cell certification. |
| **Chaebol in-housing** (tens of thousands of Blackwell GPUs each [U]) | In-house Omniverse twins | They can build simulators but cannot certify themselves or rivals, and their supplier tiers cannot build in-house. We sell into supplier ecosystems, offer Factory-in-a-box, and resell through their IT arms. |
| **MORAI** | Korean AV/UAM/maritime simulator seats, government ties | Partner: we supply Forge assets and perception data and build no AV simulator; in maritime we sell data and evaluation, not a tool. |
| **Applied Intuition** (~$830M ARR est. [U]) | AV/defense autonomy toolchain | Avoid head-on; it has no Korean manipulation or humanoid presence. Feed data via OSI/OpenSCENARIO if asked. |
| **Lightwheel** | SimReady assets plus LW-BenchHub (268 sim tasks) | Closest analogue, but free assets are non-commercial and the benchmark is sim-only. We sell commercial rights, measured physics, Korean SKUs and real-cell evaluation; possible reseller abroad. |
| **Genesis AI** ($105M seed [U]) | Open Genesis World plus own model (GENE-26.5) | A model company: a potential data/evaluation customer. Genesis stays our non-CUDA backend. |
| **CyLab, other synthetic-data vendors** | Perception data | We add physics, policies and measured transfer. |
| **Human-data vendors** (Scale-type) | Teleop and annotation | Complementary: Mimic multiplies their demos 100×, and the Arena grades the policies. |

**Honest limit:** moats 1–3 are weak until about M18. Until then AICHEMIST competes on speed and Korean presence, like any services firm.

---

## 11. Top risks and mitigations

| # | Risk | Mitigation |
|---|---|---|
| 1 | **NVIDIA licensing.** The outputs-only exemption is unverified [U]. The Kit and ovrtx binaries, the ovphysx pip binaries and the isaacsim/isaaclab wheels are all proprietary. | Written terms by M3. If needed, NVAIE on internal RT GPUs (₩1–2억/yr worst case). Every tenant-facing line runs on the Apache/BSD stack. RTX for tenants is bring-your-own-licence until terms are signed. |
| 2 | **Model and asset licence contamination:** Hunyuan3D (excludes Korea), Inria code, nvdiffrast, SAM's military clause, GPL on-prem, AGPL, cuRobo inside Isaac Lab. | Licence & Provenance Registry as a CI gate; M1 audit of CEN's NeRF pipeline; a component whitelist for the defense edition. |
| 3 | **GPU class.** Isaac RTX and ovrtx need RT cores; H100/H200/B200 and the government allocations have none. Seoul costs 23–38% more. Warp 1.18 needs Turing+ GPUs and R580+ drivers. MIG on RTX PRO 6000 is unverified [U]. | Two-pool scheduling with capability labels. RT capacity contracted early from Korean cloud providers and neoclouds, with on-prem from M9. A driver check at node admission. Government GPUs used for TRAIN only. |
| 4 | **API churn.** Isaac Lab 3.0 EA breaks APIs (quaternion order, ProxyArray). Newton ships monthly minors, Kit about 3 majors a year. ovrtx and ovphysx are alpha. Cosmos 2.5 went into limited maintenance after about 8 months. | Sim Kernel adapter with a conformance suite (falling box, pendulum, Franka pick, polybag, vehicle). A quarterly "upgrade train" with 10–15% capacity reserved. Versions pinned per contract, and certificates tied to Run Manifests so old results stay valid. |
| 5 | **Services trap / margin dilution** | The productization gate. Forward-deployed engineers capped at 1 per ₩8억 of outcome revenue [A]. Outcome credit pushes customers to self-serve. Engineer-hours per outcome is a board KPI. |
| 6 | **Outcome liability** | Acceptance is defined in a certified cell or a written protocol. Liability is capped at contract value. The certificate states its operating envelope. |
| 7 | **Arena neutrality conflict** | A separate Arena programme with a governance charter, published protocols and a third-party co-signer. Recusal: any policy we trained is certified only with the co-signer's review. |
| 8 | **Fidelity unattainable for deformables and contact-rich tasks** | Measured gaps are reported honestly and prices follow the certificate tier. A real fine-tune is always included. No deformable guarantees before the M12 measurements. |
| 9 | **Determinism vs the "reproducible" promise.** MJWarp is non-deterministic; PhysX is deterministic only on the same hardware. | Certificates run on MuJoCo CPU or Newton's deterministic paths. GPU runs are statistically reproducible, with seeds, GPU SKU and driver stored. |
| 10 | **Chaebol in-housing; customers refuse to share data; talent and policy-cycle swings** | Supplier-tier focus; data-rights discount; Factory-in-a-box; grant duplication map; stock options and remote/Korean-American senior hires. |

---

## 12. KPIs per phase

**Technical:**

| KPI | P0 (M4) | P1 (M12) | P2 (M24) | P3 (M36) |
|---|---|---|---|---|
| Certified assets (cumulative) | 300 | 2,000 | 10,000 | 50,000 |
| Forge zero-touch rate | 30% | 60% | 80% | 90% |
| Gold-tier mass / friction error vs lab measurement | ≤15% / ≤25% | ≤10% / ≤20% | ≤8% / ≤15% | ≤5% / ≤10% |
| Synthetic-only mAP ÷ real-trained mAP | ≥0.85 | ≥0.90 | ≥0.95 | ≥0.95 in 3 verticals |
| Synthetic + 10% real vs 100% real mAP | — | ≥1.0 | ≥1.0 | ≥1.05 |
| Policy sim-to-real gap (success, percentage points) | ≤25 | ≤15 (3 tasks) | ≤10 (5 tasks) | ≤8 (10 tasks) |
| Sim/real success correlation (Pearson r, ≥5 policies) | — | ≥0.7 | ≥0.8 | ≥0.85 |
| Lidar range error vs measured profile | — | ≤3 cm | ≤2 cm | ≤2 cm, plus a radar profile |
| Deterministic replay of certificate tests | 100% | 100% | 100% | 100% |
| Video to trained pick skill | 48 h | 24 h | same day, self-serve | 4 h |
| Engineer-hours per outcome (index) | 100 | 50 | 25 | 15 |
| Lag to adopt pinned Newton/Isaac Lab releases | — | ≤45 days | ≤30 days | ≤30 days |

**Business:**

| KPI | P0 | P1 | P2 | P3 |
|---|---|---|---|---|
| Revenue | ₩2억 contracted | ₩15억 (Y1) | ₩42억 (Y2) | ₩95억 (Y3) |
| Paying outcome customers | 3 | 8 | 20 | 40 |
| Outcome-to-self-serve conversion | — | 25% | 50% | 60% |
| Recurring revenue share | — | 10% | 30% | 50% |
| Blended gross margin | — | 45% | 52% | 62% |
| Marketplace GMV / third-party share of assets | — | ₩0.5억 / 0% | ₩5억 / 30% | ₩20억 / 50% |
| Arena members | — | 3 (pilot) | 8 | 20, including 2 overseas |
| Non-dilutive funding (cumulative) | TIPS operator secured | ₩15억 | ₩30억 | ₩45억 |
| Paired real/sim trials in the corpus | 1k | 10k | 50k | 200k |

**Decisions requested this month:**
1. Approve Phase 0 (about ₩10억).
2. Open the Head of Fidelity & Evaluation search.
3. Send NVIDIA Korea the written-terms request (outputs, hosting, on-prem).
4. Name the wave-1 anchor pair: one logistics or 3PL operator and one robot OEM.

# 41013_IR_RobotFlorist

**Purpose**  
RoboFlorist demonstrates a safe, dual-arm flower arrangement station for creative retail:
- **Real arm (lab)**: Dobot Magician – arranges artificial flowers.
- **Custom arm**: **BloomArm-6** (6-DOF) – ties stems with ribbon and places bouquets into a vase.
- **Safety**: GUI e-stop + hardware e-stop, simulated barrier (light curtain), collision detection/avoidance.

**Team**  
- Anisha Uddin (24457222)  
- Nicola De Meio (14264663)  

**Safety Docs (submitted)**  
- Combined PDF: `docs/SWMS_and_RA.pdf` (RoboFlorist – SWMS + General Risk Assessment)

---

## System Overview
- Shared workspace: table, vase, tool tray, barrier zone.
- Dobot places stems; BloomArm-6 handles ribbon tying & vase placement.
- Safety triggers pause motion; resuming requires a separate “Resume” action (post e-stop).

## BloomArm-6 (New 6-DOF Arm)
- **Goal**: precise, slender wrist with good roll for ribbon-tying and bouquet rotation.
- **Planned spec**: 6 revolute joints, modest reach, light payload, soft joint limits near vase.
- **DH model (WIP)**: _TODO — add link lengths & alpha offsets here after validation_
- **Why not a standard arm?** It’s tuned for **dexterity over payload** in confined, delicate spaces.

## Planning & Collision (High Level)
- Joint-space trapezoidal trajectories for fast, safe moves between waypoints.
- **RMRC** for Cartesian jogs from the GUI teach panel.
- Collision objects: table, vase, other arm envelope.  
- **Rule**: every motion call runs `safety.precheck()` then `safety.guard()` (no blind moves).

## Safety Integration
- **E-Stop (GUI)**: latching stop; requires explicit resume.
- **E-Stop (Hardware)**: Arduino-button stub; mapped to the same latch.
- **Barrier/Light Curtain (Sim)**: entering the zone pauses trajectories.
- Indicators: status lights for `ESTOP`, `BARRIER`, `COLLISION`.

## GUI (Teach + XYZ Jog)
- Joint jog buttons (`J1± … J6±`), XYZ jog (`X± Y± Z± Rz±`), speed slider.
- Live status panel (e-stop, barrier, collision).
- Buttons: `Home`, `Plan`, `Execute`, `Pause`, `Resume`, `E-STOP`.

## Running (Plan)
- **Python (Swift/RTB)**: `python -m src.python.sim_app`  
(Initial scaffolding will be added after Week 9 feedback.)

---

## Evidence Log (Commits on main)
- `chore(repo): create README as main file` — initial submission overview.
- `docs(safety): add SWMS_and_RA.pdf and link from README`
- `feat(model): outline BloomArm-6 DH section`
- `feat(gui): add teach/XYZ jog plan`

## Milestones & Tags
- v0.1-proposal (Week 7)  
- v0.2-demo-controls (Week 11)  
- v1.0-week12-presentation (Week 12)

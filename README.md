# Project Specification: Autonomous Rover Factory

## 1. Environment Layout

The factory is represented as a **6×4 grid**, where:

- **Origin (1,1):** Bottom-left tile.
- **Max (6,4):** Top-right tile.

### Points of Interest (POIs)

| Element                   | Location (x, y) | Function                               |
| :------------------------ | :-------------- | :------------------------------------- |
| **Source**                | (1, 4)          | Infinite supply of workpieces ($w$).   |
| **Machine M1 / Depot D1** | (3, 3)          | Processing; D1 capacity = 2.           |
| **Machine M2 / Depot D2** | (5, 2)          | Processing; D2 capacity = 2.           |
| **Machine M3 / Depot D3** | (1, 1)          | Processing; D3 capacity = 2.           |
| **Target**                | (6, 1)          | Final destination (infinite capacity). |
| **Charging Station 1**    | (4, 1)          | Full battery recharge.                 |
| **Charging Station 2**    | (3, 4)          | Full battery recharge.                 |

---

## 2. Rover Dynamics

### Blue Rover (Logistics)

- **Role:** Moves workpieces through the workflow: `Source → M1/D1 → M2/D2 → M3/D3 → Target`.
- **Storage Capacity:** \* Can carry up to **2** workpieces picked from the source.
  - Can carry up to **2** workpieces picked from $D_1$.
  - Can carry up to **2** workpieces picked from $D_2$.
  - Can carry up to **2** workpieces picked from $D_3$.
  - _Note:_ Total global carrying capacity is restricted by Requirement R3.

### Orange Rover (Maintenance)

- **Role:** Repairs machines ($M_1, M_2, M_3$) when they break down.
- **Action:** Must reach the specific tile of the broken machine to perform a repair.

### Shared Constraints

- **Movement:** Up, Down, Left, Right (within grid boundaries).
- **Energy:** \* **Capacity:** 8 units.
  - **Consumption:** 1 unit per move.
  - **Starting State:** Fully charged.

---

## 3. Control Requirements

The supervisor must enforce the following policies (at least 3 must be formalized as requirements):

- **R1:** No rover runs out of battery on tiles that are not charging stations.
- **R2:** The sum of the units of energy of the two batteries is always $\ge 1$.
- **R3:** The maximum number of workpieces that the blue rover can carry is **4**.
- **R4:** Each rover can charge provided its battery is not already full.
- **R5:** Rovers do not collide (occupy the same tile).
- **R6:** If $D_3$ is full, then $D_1$ can store at most one workpiece.

---

## 4. Deliverables & Tasks

### Technical Tasks

1.  **SVG Interface:** Design a suitable SVG graphical interface for the plant.
2.  **Plant Modules:** Design the modules and describe the choice for the marking.
3.  **Synthesis:** Write a `tooldef` script to synthesize a supervisor enforcing all requirements.

### Documentation

- **PDF Report:** Max 10 pages (A4) justifying all design choices.

### File Organization

- **Root Folder:** Named with surnames of group members (e.g., `bresolin-zavatteri/`).
- **Subfolder `escet/`:** Contains all CIF, tooldef, and SVG implementation files.
- **Report:** `report.pdf` located inside the root folder.

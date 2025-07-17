# 📘 Shopfloor Qualification Management System (PowerApps + SQL)

## 🔧 Overview

This project is a comprehensive digital solution developed during my master's thesis at **Festool GmbH** to manage and scale the **qualification process on the shopfloor**. The goal is to ensure employees are properly trained to assemble various products while maintaining flexibility to adapt to production demands and process changes.

The application was developed using **Microsoft Power Platform** (PowerApps + Power Automate) with a **SQL Server backend**, and is designed to replace fragmented Excel-based tracking systems with a centralized, automated, and scalable solution.

---

## 🎯 Objectives

- Digitally manage training and qualification of shopfloor employees
- Ensure high flexibility for workers across multiple products and lines
- Track instruction steps, training plans, evaluations, and changes
- Make the system scalable, modular, and adaptable to future process needs
- Improve transparency, traceability, and compliance

---

## 🧱 Architecture & Data Model

### 🔗 Key Entities and Relationships

| Table | Description |
|-------|-------------|
| `staffs` | Master table of employees |
| `lines`, `products`, `locations` | Define where and how products are assembled |
| `instructionSteps` | All instruction steps (with versioning and hazards) |
| `AVOLocations` | Assign steps to specific locations in order |
| `qualificationPlans` | Training sessions with trainee, trainer, supervisors |
| `locationsInQualiPlans` | Locations involved in a training plan |
| `qualificationChecks` & `qualificationCheckDetails` | Supervisor evaluation of trainee performance |
| `traineeEvaluationThrTrainer` | Trainer's evaluation of the trainee |
| `trainerEvaluationThrPS` | Supervisor’s evaluation of the trainer |
| `qualificationPhotos`, `qualificationPlanPhotos` | Documentation of training/check activities |
| `AVOEmployees` | Historical qualification matrix (who can what, where) |

> Foreign key relationships are indicated by shared columns (e.g. `employeeID`, `stepID`, `locationID`)

---

## 🔄 Qualification Flow

### 🧩 General Concept

- Products are assembled on **assembly lines** using specific **instruction steps** at each **location**.
- **Not all employees** can assemble all products — training is required.
- The aim is to **maximize cross-product qualification** based on current and forecasted production needs.
- Even **general processes** (not tied to a product) are integrated using a special modeling logic (line = product = location = process name).

### 🧠 Modular Design

1. **Qualimatrix**  
   View which employee is qualified for which step and at which location.

2. **AVO Erstellen oder Bearbeiten**  
   Create or update instruction steps. If updated, a **new step version** is created with a reference (`ancestorID`), and all linked locations are updated. Affected employees are identified via `AVOEmployees` and flagged for re-instruction.

3. **Qualiplanen**  
   Managers plan training sessions with trainees, trainers, and supervisors, based on upcoming production and skill gaps.

4. **Qualidurchführen**  
   Trainers conduct training. If a training is pre-planned, trainer and trainee see only their assigned session.

5. **Qualichecks & Änderungen sehen**  
   Process Supervisors check whether the trainee is ready to work independently and ensure safety/productivity. This also includes:
   - Evaluating trainers
   - Viewing recent **instruction changes** (new/updated steps)
   - Notifying employees who are affected by these changes

---

## 🧠 Instruction Step Versioning

When an instruction step is modified:
1. A new `stepID` is generated
2. The old step is referenced via `ancestorID`
3. New records are created in `AVOLocations` to link the new step to the appropriate locations with updated order/version
4. Affected employees are identified through `AVOEmployees` and flagged for re-qualification

---

## 🖥️ Technologies Used

- **PowerApps (Canvas App)**: Main UI for managing the qualification process
- **Power Automate**: For sending notifications, automating updates, etc.
- **SQL Server**: Backend data storage
- **Draw.io / Figma / Whimsical**: For flowcharts and diagrams (used in documentation)

---

## 📸 Sample Screenshots

> _Add screenshots in the `/screenshots/` folder and embed them here later_

- Qualification Matrix Overview  
- Instruction Step Management  
- Plan Qualification  
- Conduct Training  
- Check & View Changes

---

## 📬 Future Improvements

- Add multilingual support (DE/EN)
- Add notification via Teams integration
- Integrate real-time skill gap analysis dashboard
- Implement AI-based training suggestions based on forecasted demand

---

## 👨‍💼 About the Developer

**Sagar Dhanani**  
Digitalization & Automation Enthusiast | Power Platform Developer | Mechatonics Engineer  
📍 Based in Germany & India  
📫 [sagardhanani5@gmail.com] | [www.linkedin.com/in/sagar-d-ab8b65179] 

---

## 📁 Repository Structure


# AI Agent Engineer Technical Assessment

### 🔗 Project Links
* **Demo Video:** 
---

### 📝 Project Overview & Approach
I engineered a production-grade ETL pipeline that transforms raw API data into high-integrity records and visual business intelligence. My approach used a centralized **JavaScript Transformation Engine** to process data in a single $O(n)$ pass. I designed a hybrid data architecture that allows a single workflow to power two different streams: row-level synchronization for Google Sheets and aggregate-level reporting for executive dashboards.

---

### 🛠️ Challenges & Solutions

* **Challenge 1: The "User vs. Stats" Data Structure.** I needed to send a list of users to Google Sheets while simultaneously providing summary statistics to the QuickChart nodes.
* **Solution:** I architected the **Code Node** to return a dual-layered JSON object containing both a `users` array and a `stats` object. This allows the workflow to use a **Split Out** node for row-based updates while the main branch feeds the reporting engine.

* **Challenge 2: Active Error Governance.** I needed a system that proactively manages failures rather than silently ignoring them.
* **Solution:** I implemented a dedicated **Error Workflow**. By connecting the main task to a specialized error-trigger handler, the system intercepts failures (like API timeouts), logs the incident, and ensures the pipeline remains observable and robust.

* **Challenge 3: Complex Visual Merging.** Standard nodes struggle to handle multiple separate image streams for a single email.
* **Solution:** I generated four distinct charts for Age, Gender, Role, and City. I then utilized **sequential Merge nodes** to consolidate these separate binary files into a single context for a unified visual report.

---

### 🌟 Bonus Features: Aggregation & Reporting
I implemented **Aggregation/Reporting** because raw data lacks immediate business value without visualization.
* **Advanced Aggregation:** The custom Code node calculates live distributions for Age, Gender, and Role, alongside batch success rates.
* **Native Visualization:** The workflow utilizes four built-in **QuickChart** nodes to generate high-fidelity visuals, bridging the gap between raw logs and executive summary reports.

---

### 📸 Project Gallery
*All technical screenshots and sample outputs are located in the `/screenshots` folder.*

#### **1. Full System Architecture**
![Full Workflow](./screenshots/Screenshot%202025-12-19%20170246.png)

#### **2. Custom JavaScript Logic (Users vs. Stats)**
![Code Node Logic](./screenshots/Screenshot%202025-12-19%20170425.png)

#### **3. Sample Output: Executive BI Report**
![Email Output](./screenshots/Screenshot%202025-12-19%20170655.png)

---

### 🚀 Instructions to Test/Run
1. **Import:** Download and import the `Task.json` file into n8n.
2. **Setup:** Connect your **Google Sheets** and **Gmail** OAuth2 credentials.
3. **Trigger:** Execute the **Webhook** or click **Execute Workflow**.
4. **Observe:** Check the Google Sheet for cleaned records and your Inbox for the merged visual infographic.

---

### 📂 Repository Contents
* **`Task.json`**: The complete n8n workflow export.
* **`/screenshots`**: A dedicated folder containing all workflow visualizations, logic captures, and sample data outputs.

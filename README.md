# AI Agent Engineer: Resilient ETL & BI Pipeline

> **More than just an ETL pipeline—this is a resilient BI solution.** I engineered an n8n workflow that goes beyond simple data movement. By leveraging custom JavaScript for deep data sanitization and deduplication, I ensured that only high-quality records reach the destination. The architecture concludes with a sophisticated reporting layer, delivering visual insights directly to stakeholders' inboxes while maintaining a robust, error-tolerant core.

---

### 📊 Project Summary
This project demonstrates a production-grade ETL (Extract, Transform, Load) workflow designed with scalability and resilience in mind. Beyond the core requirements of fetching and storing data, I engineered a **Business Intelligence layer** that performs real-time data aggregation and visual reporting. The system is built on **defensive programming principles**, ensuring that API failures are captured and handled through an error-handling configuration, preventing workflow stagnation and maintaining system observability.

#### **Technical Implementation & Data Logic**
At the heart of the workflow is a centralized **JavaScript Transformation Engine** within a custom Code node. By consolidating the logic into a single execution pass ($O(n)$ complexity), I optimized performance and maintainability. This engine handles:
* **Data Sanitization:** Normalizing naming conventions and validating email structures.
* **Integrity Filtering:** Implementing a "seen" hash map to ensure 100% data deduplication and enforcing strict domain-specific filters.
* **Schema Enhancement:** Injecting high-resolution timestamps (`processed_at`) and metadata for auditability.

#### **Advanced Reporting (Bonus Features)**
To provide strategic value, I extended the core requirements by building an **Automated Reporting system**. The transformation logic calculates real-time distribution metrics—including Age groups, Gender splits, and Top Cities—alongside a calculated success rate for the batch.
* **Visual Intelligence:** The workflow utilizes the **built-in QuickChart nodes** to generate high-fidelity charts dynamically, including bar, doughnut, and city-based distribution charts.
* **Multi-Channel Delivery:** Cleaned records are synchronized to **Google Sheets** via a Split Out node for operational use, while a **Refined HTML Email** is dispatched via Gmail to stakeholders.

#### **Architectural Resilience**
A key challenge was maintaining a "flat" structure for spreadsheet compatibility while preserving "nested" objects for the reporting engine. I solved this by architecting a hybrid JSON return from the Code node, allowing downstream nodes to target specific data layers—like the `users` array for Google Sheets and the `stats` object for reporting—efficiently. By implementing defensive logic and "Continue on Fail" settings, the pipeline remains robust against external API instability, showcasing a professional-tier approach to automated data engineering.

---

### 🛠️ Tech Stack
* **Platform:** n8n
* **Language:** JavaScript (ES6+)
* **Integrations:** DummyJSON, Google Sheets, Gmail
* **Native n8n Features:** QuickChart Node, Code Node, Split Out, Merge

### 🚀 How to Run
1. **Import:** Download the `Task.json` file from this repo and import it into your n8n instance.
2. **Credentials:** Connect your Google Sheets and Gmail accounts.
3. **Trigger:** Execute the workflow manually or via the Webhook URL to initiate the ETL and reporting process.

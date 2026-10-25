<div align="center">

# 🪪 Pakistan Driver Licensing Exam Analytics

A SQL Server reporting demo for driver licensing exam sessions, results, audit-event matching, and controlled non-PII enrichment.

![SQL Server](https://img.shields.io/badge/Database-SQL%20Server-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white)
![T-SQL](https://img.shields.io/badge/Language-T--SQL-0078D4?style=for-the-badge)
![Demo](https://img.shields.io/badge/Data-Synthetic%20Demo-16a34a?style=for-the-badge)
![Validation](https://img.shields.io/badge/Validation-SQL%20Checks-2563eb?style=for-the-badge)

<p><b>Relational constraints · Parameterized reporting · Synthetic Pakistan demo data · Privacy-aware fields</b></p>

</div>

---

## 📌 Project Overview

This project contains a reproducible SQL Server demonstration for a Pakistan-focused driver licensing exam report. The included schema and seed rows are fictional demonstration data.

The report returns exam-level results with office, test, language, duration, and optional secondary-verification attributes. Protected workstation and driver-license tokens are used only as internal demo join keys and are not selected into the final report.

## 🎯 Objectives

- Define a typed demo schema for offices, tests, languages, vault tokens, sessions, exams, audit events, and optional driver-license enrichment.
- Enforce identifiers, foreign-key relationships, and exam-domain checks.
- Seed fictional data in a transaction using `IF NOT EXISTS` checks.
- Provide an editable date-range report and a fixed-parameter example.
- Show table counts and check exam values and foreign-key relationships with SQL.

## 🧱 Database Model

| Schema | Tables | Purpose |
| --- | --- | --- |
| `PUBLIC_AKTE` | `DIM_OFFICE`, `REF_TESTS`, `REF_LANG`, `DIM_VAULT`, `FACT_SESSIONS`, `FACT_EXAMS`, `AUDIT_HISTORY` | Demo reference, session, exam, and audit data |
| `PUBLIC_DL` | `V_DL_MASTER_NONCONF` | Synthetic optional token-based enrichment table |

The model includes a composite session key `(SESSION_ID, OFFICE_ID)`, an exam primary key, foreign keys for sessions, exams, and optional enrichment, unique/reference constraints, and check constraints for exam results, flags, duration, counters, and score range.

## ✨ Main Features

### 📊 Reporting SQL

- Half-open date filtering using `@StartDate` and `@EndDate`.
- Exam/session/reference joins using declared keys.
- An `EXISTS` check that flags a matching audit event within 15 minutes before a session.
- Derived exam duration and pass/fail counters.
- Optional token-based enrichment with non-PII driver-license attributes.

### 🔐 Privacy and Reliability

- Synthetic demo records only; no production records or secrets are included.
- Raw IP and license values are absent from the demo schema.
- Seed inserts run inside a transaction with `XACT_ABORT ON`.
- Verification SQL displays row counts and checks exam values and foreign-key relationships.

## 📁 Project Structure

```text
Pakistan Driver Licensing Exam Analytics/
├── demo_setup.sql
├── demo_query.sql
├── demo_query_example.sql
├── verify_demo.sql
├── README.md
├── LICENSE
└── .gitignore
```

## ⚙️ Run the Demo

Use SQL Server Express or Developer Edition with SQL Server Management Studio. Run the scripts in this order:

1. `demo_setup.sql` creates the demo database, tables, constraints, and sample rows.
2. `verify_demo.sql` displays row counts and integrity-check counts.
3. `demo_query_example.sql` shows a basic exam report.
4. Change `@StartDate` and `@EndDate` in `demo_query.sql` to select another date range.

The scripts have not been executed in this review environment. Run them in SQL Server Management Studio and inspect the verification results before making runtime claims. The account running `demo_setup.sql` needs permission to create a database and tables. The setup script creates missing tables but does not migrate existing ones.

## 🧰 Technology Stack

| Technology | Purpose |
| --- | --- |
| SQL Server / T-SQL | Demo schema, constraints, seeding, and reporting |
| SQL Server Management Studio | Documented execution environment |
| Joins, `CASE`, and `EXISTS` | Exam reporting and audit flag |
| Transactions and `IF NOT EXISTS` | Repeatable synthetic seed insertion |

## 🧭 Scope and Limitations

This archive demonstrates a synthetic reporting model, not a production connection. The production tables, physical metadata, tokenization process, permissions, and Tableau workbook must be supplied and approved separately. The audit flag uses a protected token and a 15-minute time window; confirm those rules against the production system before using real data.

## 🧑‍💻 Author

**Muhammad Ali Nawaz**  
SQL Developer / Database Developer

## 📄 License

This project is licensed under the [MIT License](LICENSE).

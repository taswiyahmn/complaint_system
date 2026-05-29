## Rebuilding the Personnel Complaint Management System: Complete Analysis & Data Architecture

### Core Operational Problems

The previous system broke down trying to manage over 5,900 records flowing from four separate sources (legacy web portal, Google Forms, WhatsApp, and physical files). The core issues weren't technical constraints—they were structural: no consistent data format rules, no unified workflow, and no way to track anything systematically. This project tackled three specific failures:

* **Noise in the data**: More than 60% of WhatsApp entries were automated bot messages, duplicates, or spam. Filtering these out to find actual criminal complaints was impossible at scale.
* **Data scattered across the organization**: Hierarchy information (headquarters, regional offices, police stations), ethics code sections, and department structures lived in dozens of separate spreadsheets with no consistent database design.
* **Blind spot at the management level**: Leadership couldn't see patterns in complaint types, violation trends by region, or how quickly cases were being resolved. Real-time visibility didn't exist.

---

### Approach & New System

Two separate applications were built from the ground up:

1. **Operations Layer**: A public-facing complaint submission interface and internal handling dashboard using digital queue management instead of manual file routing.
2. **Executive Layer**: Real-time monitoring system showing violation trends broken down by location, demographics, and violation type.

---

### What Was Built (8-Month Timeline)

Acting as a **hybrid data analyst and system bridge**, I worked with 3 full-stack developers and 1 UI/UX designer across three connected workstreams:

```
[Upstream: ETL & Workflow Design] → [Middle: Query Architecture] → [Downstream: Documentation & Launch]
```

* **Upstream (ETL & Process Engineering)**: Mapped the old workflow, redesigned it for digital execution, and cleaned messy text data using Python scripts to extract valid information.
* **Middle (Data Modeling)**: Built complex query logic (involving 10+ table joins) that merged organizational hierarchy, staffing units, and violation codes into a single consistent data source.
* **Downstream (Technical Specification)**: Created a JSON data dictionary as the API contract and led technical briefings to ensure developers built exactly what the design specified.

**Data Ingestion Flow**

![Data Ingestion Flow](Sources%20Flow.png)

**Application Flow**

![Application Flow](Application%20Flow.png)

### Technical Work Breakdown

* **Complex Query Design**: Assembled and executed advanced SQL involving 8+ simultaneous table joins to consolidate fragmented data structures into unified datasets.
* **Performance Tuning**: Reduced query execution time to under 1 second across computationally heavy scripts, ensuring the system remained responsive.
* **Schema Analysis**: Mapped database structure deeply to locate and extract 20+ specific data points and metrics from a single core transaction table.

### Phase 2: Cataloging Dimensions & Setting Up Data Control

![Cataloging Dimensions & Setting Up Data Control](Catalog%20Dimension.png)

**Moving to Production**: The 1,900+ cleaned records were migrated into PostgreSQL to serve as the backbone for the relational query architecture below.

![Cataloging Dimensions & Setting Up Data Control (2)](Catalog%20Dimension%20(2).png)

```json
{
    "perpetrator_id": "0-00001",
    "report_id": "0",
    "type": null,
    "group_name": null,
    "status": "Dalam Penanganan",
    "status_alias": "Dalam Penanganan",
    "date_activity": "2026-04-28 07:14:42.369",
    "responsible_person_name": null,
    "officer_report_name": "Renata Ramadhanyandra",
    "handling_progress": "test",
    "subject": null,
    "previous_case_position": "KABAG BAGYANDUAN",
    "case_position": "POLDA RIAU",
    "polda": "POLDA RIAU",
    "polres": null,
    "police_function": "DIV PROPAM MABES POLRI",
    "sub_function": null,
    "sub_status": null,
    "special_case": null,
    "attachments": [
      {
        "url": "https://example.com/evidence.jpg",
        "size": "0",
        "detail": null,
        "file_name": "evidence"
      },
      {
        "url": "s3://mybucket/documents/laporan.pdf",
        "size": "0",
        "detail": null,
        "file_name": "laporan"
      }
    ]
}
```

![Dashboard](Dahsboard%20Monitoring.png)

#### **1. Complaint Volume by Source**

Tracks the raw count of incoming reports, broken down individually by channel (WhatsApp and Google Forms).

#### **2. Geographic Distribution & Regional Details (Interactive Modal)**

An interactive map component showing complaint counts by province and jurisdiction. Clicking a specific region opens a detailed view with localized statistics.

#### **3. Personnel Implicated in Misconduct**

Aggregates headcount of internal staff members named in reports involving criminal activity or serious violations.

#### **4. Violation Categories & Subcategories**

A hierarchical matrix displaying complaint volumes organized by violation type, subcategory, and specific form of misconduct.

#### **5. Violation Rankings by Region**

A sortable list ranking all jurisdictions by complaint volume (highest to lowest) to identify problem areas quickly.

#### **6. Complaint Source Distribution**

A pie chart showing the percentage breakdown of each incoming channel to monitor which routes receive most use.

#### **7. Subject Demographics**

A matrix showing alleged subjects grouped by rank, academy graduation year, and education level, with counts and percentages.

#### **8. SLA Violations & Justifications**

Shows volume and percentage of cases that missed resolution deadlines, categorized by the stated reason for delay.

#### **9. Age Distribution of Alleged Subjects**

A statistical breakdown of alleged subjects grouped by generational age bands, calculated from birth date records.

![Detail Penanganan](Halaman%20Detail%20Petugas.png)

#### **1. Automated Case Timeline & Summary**

Displays the detailed chronology of events alongside a machine-generated executive summary synthesized from the case record.

#### **2. Report Core Information**

The fundamental details of the specific case under review, including current status and administrative flags.

#### **3. Complainant Details**

Identity and background information of the person who filed the report.

#### **4. Alleged Subject Profile**

Rank, organizational assignment, and background of the internal personnel named in the report.

#### **5. Case History Timeline**

An audit trail showing every action taken on the case from initial submission through most recent update.

## Project Outcomes & Deliverables

The automated pipeline and dual-platform system reshaped the organization's operations over 8 months, with measurable results:

* **60%+ Noise Reduction**: Filtered out bot responses, duplicates, and non-criminal messages from 10,000+ WhatsApp entries through automated processing.
* **Eliminated Manual Cross-Referencing**: Automated lookups for 1,900+ form submissions using Python-based dimension matching, freeing hundreds of staff hours.
* **Two Production Systems Deployed**: Launched a public complaint portal and internal case management interface backed by a robust multi-handler architecture.
* **No Implementation Delays from Miscommunication**: Clear data dictionaries and technical specifications kept 3 developers and 1 designer aligned with the architecture design, allowing early project completion.
* **Sub-Second Dashboard Performance**: Optimized queries across 10+ table joins execute in under 0.8 seconds, enabling live monitoring at both management and operational levels.

---

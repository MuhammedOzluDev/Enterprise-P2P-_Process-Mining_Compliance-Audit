# Enterprise-P2P-_Process-Mining_Compliance-Audit

## Overview
This repository contains a comprehensive Process Mining analysis applied to a Procure-to-Pay (P2P) event log. Using Python and the pm4py library, this project transitions from raw event data to actionable business intelligence by discovering the actual process model, identifying performance bottlenecks, and executing rigorous conformance checking against target business rules. 

## Dataset
The analysis is based on the `P2P.csv` event log, which tracks the lifecycle of purchase orders.
- **Case ID** (`Order_ID`): The unique identifier for each process instance.
- **Activity** (`Activity`): The specific operational step executed.
- **Timestamp** (`Timestamp`): The exact time the activity occurred.

**Summary** 934 unique cases, 7,782 events, and 9 distinct activities.

## Analytical Pipeline
The notebook (`ProcessMining_InternshipDAY1.ipynb`) follows a structured, end-to-end process mining methodology:

1. **Data Ingestion & Preprocessing:** Formatting the raw CSV into an event log compliant with `pm4py` standards, ensuring chronological integrity.
2. **Descriptive Statistics:** Analyzing case durations, event frequencies, and variant distributions.
3. **Process Discovery:** Mapping the "As-Is" process using Directly-Follows Graphs (DFG) and generating mathematically sound Petri Nets via the Inductive Miner.
4. **Variant Analysis:** Isolating the "happy paths" from exceptional or rare procedural sequences.
5. **Performance Analysis:** Generating performance-annotated DFGs to pinpoint exact bottlenecks and excessive wait times between activities.
6. **Conformance Checking:** Utilizing both Token-Based Replay (TBR) and Alignment techniques to evaluate how well the real-world data fits the discovered model.
7. **Rule-Based Auditing (To-Be Process):** Applying `LTL` (Linear Temporal Logic) style eventual-follows filtering to audit specific compliance constraints.

## Key Business Findings & Audit Results
- **Financial Risk:** **17.7%** of cases violated payment protocols (Make Payment occurred without a preceding Approve Invoice activity).
- **Procedural Deviations:** **16.0%** of cases bypassed initial authorization (Create Purchase Order occurred without Create Purchase Requisition).
- **Inventory Risk:** **19.4%** of cases violated receiving protocols (Create Invoice occurred before Receive Goods).
- **Bottlenecks:** The performance analysis highlighted severe delays in specific transitions, such as the gap between approving a requisition and receiving goods (averaging 23.1 days).

## Technologies Used
- **Python 3**
- **pm4py** (Process Mining for Python)
- **pandas** & **numpy** (Data Manipulation)
- **Graphviz / matplotlib** (Process Visualization)

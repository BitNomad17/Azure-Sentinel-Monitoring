# Azure-Sentinel-Monitoring
Microsoft Sentinel + Log Analytics demo lab for security monitoring, KQL detections and incident workflows.

# Azure Sentinel Monitoring – Demo Lab

This repository contains sample Kusto Query Language (KQL) queries and a reference workflow
for building a basic security monitoring lab using Microsoft Sentinel and Azure Log Analytics.

The goal is to demonstrate how to:
- Ingest Azure AD and Azure Activity data into a Log Analytics workspace
- Enable Microsoft Sentinel
- Create analytics rules using KQL
- Investigate suspicious sign-ins and privilege escalations

---

## Architecture Overview

High-level flow:

1. Azure resources send logs to **Log Analytics workspace**
2. **Microsoft Sentinel** is enabled on that workspace
3. Sentinel uses **KQL queries** to detect:
   - Sign-in anomalies
   - High-privilege role assignments
4. Incidents are created in Sentinel for security investigation

You can later extend this with:
- Logic Apps playbooks (SOAR)
- Workbooks and dashboards
- Alerts integration with email, Teams, ITSM

---

## Prerequisites

- Azure subscription
- Log Analytics workspace
- Microsoft Sentinel enabled on the workspace
- Data connectors configured for:
  - Azure Active Directory sign-in logs
  - Azure Active Directory audit logs
  - Azure Activity

---

## How to Use the Queries

1. Open the Azure portal and go to **Microsoft Sentinel**.
2. Select your Sentinel-enabled workspace.
3. Go to **Logs**.
4. Open the `queries` folder in this repo.
5. Copy the contents of `.kql` files and paste into the Log query window.
6. Run the query and verify the results.
7. Convert validated queries into **Scheduled analytics rules**:
   - Sentinel → Analytics → + Create → Scheduled query rule
   - Set frequency and lookback period
   - Configure incident creation and severity

---

## Files

### `queries/signin-anomalies.kql`

Detects suspicious sign-in activity such as:
- Multiple failed sign-ins
- Sign-ins from multiple countries in a short period
- Sign-ins from high-risk countries

### `queries/privilege-escalation.kql`

Detects privileged role assignments such as:
- Global Administrator
- Privileged Role Administrator
- User Access Administrator
- Security Administrator

---

## Future Ideas

- Add Logic Apps playbooks to:
  - Disable user on confirmed compromise
  - Notify security team via email or Teams
- Build a Sentinel workbook with:
  - Failed sign-in trends
  - High-risk IP addresses
  - Admin role changes over time

This lab is for learning and demonstration. Always tune detections for your environment before production use.


## Demo Status

This lab has been tested in a personal Azure subscription with:
- Azure AD sign-in logs
- Azure Activity logs
- Microsoft Sentinel enabled on a single workspace


## Screenshots

Below are sample screenshots demonstrating how Microsoft Sentinel and Azure Log Analytics
visualize data, run KQL queries, generate incidents, and create analytics rules.

### 🔹 Sentinel Overview Dashboard
Shows incidents, alerts, and event trends.
![Sentinel Overview](images/sentinel-overview.png)

### 🔹 Sentinel Incidents Page
Displays security incidents generated from analytics rules and anomaly detections.
![Sentinel Incidents](images/sentinel-incidents.png)

### 🔹 KQL Query Execution in Logs
Query window used to run detections such as sign-in anomalies or privilege escalations.
![KQL Query Results](images/kql-query-results.png)

### 🔹 Scheduled Analytics Rule (Query Rule)
Shows how detections are operationalized using Sentinel analytics.
![Analytics Rule](images/analytics-rule.png)

### 🔹 Azure Log Analytics Query Results
Basic query results showing structured log events feeding Sentinel.
![Log Analytics Query](images/loganalytics-query.png)

### 🔹 Workbook Visualization
Dashboard visualizing insights, trends, and context from Sentinel data.
![Sentinel Workbook](images/sentinel-workbook.png)

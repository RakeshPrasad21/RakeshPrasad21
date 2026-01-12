#### Audit Log Capture & Ingestion
- Enable Audit Logging in Security Copilot via Microsoft Purview—admins opt in during setup or via the Owner settings (“Logging audit data in Microsoft Purview”).
- The CloudAppEvents table in Sentinel ingests Copilot audit logs through the Defender XDR connector, capturing user/admin actions and Copilot responses in nearly real time.
#### Connector Setup & Data Verification
- Ingested logs flow into Sentinel’s Log Analytics workspace.
- You can verify correct ingestion using this KQL:
 
```
CloudAppEvents
| where parse_json(RawEventData)["AppIdentity"] == "Copilot.Security.SecurityCopilot"
  and parse_json(RawEventData)["Workload"] == "Copilot"
```
 
#### Interactive Workbook for Monitoring
The prebuilt workbook in Sentinel—accessible via “Security Copilot Audit”—offers:
Dashboard Overview:
- Total Copilot interactions over time
- Interaction types (plugins, promptbook changes, etc.)
- Geographical activity distribution
- Top users by prompt volume
Promptbook and Plugin Activities
- Tables and graphs showing promptbook creations, deletions, updates, and plugin enable/disable events.
Sign-in Analysis
- Visuals for successful vs. failed sign-ins (by location)
- Details such as IP, OS, failure reasons (e.g., MFA challenge, invalid credentials).
SCU (Service Consumption Unit) Events
- Details on bought or modified SCUs, including who made changes
- SCU capacity trends over time.

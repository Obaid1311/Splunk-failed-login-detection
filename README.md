Splunk Failed Login Detection (SOC Analyst Project)

Overview:

This project demonstrates how to detect and analyze failed login attempts using Splunk SIEM. It focuses on identifying brute-force attack patterns from Windows Security Event Logs.

Objective:
- Detect failed login attempts (Event ID 4625)
- Analyze login behavior
- Identify potential brute-force attacks
- Visualize security events

Tools & Technologies:
- Splunk Enterprise (SIEM)
- Windows Event Logs
- SPL (Search Processing Language)

Data Source:
- Sourcetype: WinEventLog:Security

Event IDs:
- 4625 → Failed Login
- 4624 → Successful Login

Methodology:
1. Collected Windows Security logs
2. Filtered authentication events
3. Created SPL queries to analyze logs
4. Counted failed login attempts per user
5. Visualized data using charts

SPL Queries Used:
1. Failed & Successful Logins:
index=main sourcetype="WinEventLog:Security" (EventCode=4624 OR EventCode=4625)
| eval Status=if(EventCode=4625,"Failed","Successful")
| table _time Status Account_Name host Source_Network_Address Source_Port
| sort -_time

2. Failed Login Count:
index=main EventCode=4625 sourcetype="WinEventLog:Security"
| stats count by Account_Name, host
| sort -count

Findings:
- Multiple failed login attempts detected for user obaid
- Source IP: 127.0.0.1 (local system)
- Pattern indicates brute-force attack simulation

Security Analysis:
- Repeated failed logins indicate possible brute-force attack
- Monitoring Event ID 4625 is critical in SOC operations
- Correlation with successful logins helps detect compromise

Recommendations:
- Enable account lockout policy
- Implement Multi-Factor Authentication (MFA)
- Monitor logs continuously using SIEM
- Create alerts for repeated failed login attempts

Screenshots:
- Search Results:
"Search" (screenshots/search_results.png)
- Visualization Chart:
"Chart" (screenshots/chart.png)
- Event Log Details:
"Logs" (screenshots/event_log.png)

Project Structure:
splunk-failed-login-detection/
├── README.md
├── queries/
├── screenshots/
├── sample_logs/
├── report/

Skills Gained:
- SIEM (Splunk)
- Log Analysis
- Threat Detection
- Security Monitoring
- Basic Incident Analysis

Conclusion:

This project showcases practical SOC analyst skills such as log analysis, threat detection, and security monitoring using Splunk.

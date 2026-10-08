# Sports Security Incident Detection and Response Lab

## Project Overview

This project simulates a security incident investigation for a fictional sports organization. I analyzed authentication logs, identified suspicious login activity, investigated the affected account, created a Splunk detection query, and documented containment and recovery recommendations.

The investigation identified five failed login attempts against the `scouting.lee` account from `198.51.100.77` within 32 seconds. A successful login from the same IP address occurred 21 seconds after the final failure. This pattern is consistent with a suspected brute-force attack and possible account compromise.

## Objectives

- Analyze authentication logs for suspicious activity
- Identify repeated failed login attempts
- Investigate the affected user and source IP address
- Import and analyze logs in Splunk Enterprise
- Create a reusable SPL detection query
- Document indicators of compromise
- Recommend containment and recovery actions
- Produce a professional incident report

## Tools and Technologies

- Splunk Enterprise
- Splunk Processing Language
- Authentication log analysis
- Windows
- GitHub
- Markdown
- CSV

## Key Findings

| Field | Finding |
|---|---|
| Affected account | `scouting.lee` |
| Suspicious source IP | `198.51.100.77` |
| Failed attempts | 5 |
| First failed attempt | September 9, 2026 at 05:05:10 |
| Last failed attempt | September 9, 2026 at 05:05:42 |
| Successful login | September 9, 2026 at 05:06:03 |
| Time from final failure to success | 21 seconds |
| Severity | High |
| Classification | Suspected brute-force attack and possible account compromise |

## Splunk Detection Query

```spl
sourcetype=auth_log action=login status=failure
| stats count AS failed_attempts earliest(_time) AS first_attempt latest(_time) AS last_attempt by user src_ip
| where failed_attempts >= 5
| convert ctime(first_attempt) ctime(last_attempt)
```

This query groups failed login attempts by user and source IP address. It returns results when the same account receives five or more failed login attempts from the same source.

## Investigation Process

1. Reviewed the raw authentication log.
2. Identified repeated failures against `scouting.lee`.
3. Confirmed that all five failures came from `198.51.100.77`.
4. Identified a successful login from the same IP address.
5. Imported the authentication log into Splunk Enterprise.
6. Used SPL searches to isolate and summarize the suspicious activity.
7. Created and saved the repeated failed login detection report.
8. Exported the detection result as a CSV file.
9. Documented the incident findings and recommended response actions.

## Recommended Response

- Temporarily disable the affected account
- Reset the user’s password
- Revoke active sessions and authentication tokens
- Verify whether the successful login was authorized
- Review activity performed after the login
- Monitor or block the suspicious source IP address
- Require multifactor authentication
- Review account lockout and authentication monitoring policies

## Evidence

- [Raw authentication log](sample-data/authentication.log)
- [Initial investigation notes](notes/initial-investigation.md)
- [Splunk search queries](queries/splunk-queries.md)
- [Final incident report](reports/incident-report.md)
- [Splunk detection results](reports/splunk-failed-login-detection.csv)
- [Splunk screenshots](screenshots)

## Detection Result

![Splunk failed login detection](screenshots/Screenshot%202026-10-07%20171636.png)

## Repository Structure

```text
sports-security-incident-response-lab/
├── notes/
│   └── initial-investigation.md
├── queries/
│   └── splunk-queries.md
├── reports/
│   ├── incident-report.md
|   ├── splunk-authentication-results.csv
│   └── splunk-failed-login-detection.csv
├── sample-data/
│   └── authentication.log
├── screenshots/
│   └── Splunk investigation evidence
└── README.md
```

## Skills Demonstrated

- Security monitoring
- SIEM log analysis
- Splunk SPL
- Incident detection
- Authentication analysis
- Threat investigation
- Indicator identification
- Incident response
- Technical documentation
- Evidence-based security analysis

## Disclaimer

This project uses fictional data and was created for cybersecurity training and portfolio purposes.

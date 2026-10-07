# Security Incident Report

## Incident Summary

A suspicious authentication pattern was identified in the fictional sports organization’s authentication logs. The account `scouting.lee` received five failed login attempts from the source IP address `198.51.100.77` within 32 seconds. A successful login from the same IP address occurred 21 seconds after the final failed attempt.

The activity may indicate a brute-force attack that resulted in account compromise.

## Incident Details

| Field | Information |
|---|---|
| Incident type | Suspected brute-force attack |
| Affected account | scouting.lee |
| Source IP address | 198.51.100.77 |
| Failed login attempts | 5 |
| First failed attempt | September 9, 2026 at 05:05:10 |
| Last failed attempt | September 9, 2026 at 05:05:42 |
| Successful login | September 9, 2026 at 05:06:03 |
| Time between final failure and success | 21 seconds |
| Severity | High |
| Status | Investigation completed |

## Detection

The authentication log was uploaded into Splunk Enterprise and assigned the `auth_log` sourcetype. A Splunk detection query grouped failed login attempts by user and source IP address.

The detection triggered when the same account received five or more failed login attempts from the same source IP address.

```spl
sourcetype=auth_log action=login status=failure
| stats count AS failed_attempts earliest(_time) AS first_attempt latest(_time) AS last_attempt by user src_ip
| where failed_attempts >= 5
| convert ctime(first_attempt) ctime(last_attempt)

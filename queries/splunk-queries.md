# Splunk Search Queries

These Splunk Processing Language searches were used to analyze authentication activity and detect suspicious login behavior.

## View All Authentication Events

```spl
source="authentication.log" host="Jalins-PC" sourcetype="auth_log"
```

Purpose: Displays all authentication events imported from the sample log file.

## Find Failed Logins for the Affected User

```spl
sourcetype=auth_log user="scouting.lee" status="failure"
```

Purpose: Isolates failed authentication attempts targeting the `scouting.lee` account.

## Detect Repeated Failed Login Attempts

```spl
sourcetype=auth_log action=login status=failure
| stats count AS failed_attempts earliest(_time) AS first_attempt latest(_time) AS last_attempt by user src_ip
| where failed_attempts >= 5
| convert ctime(first_attempt) ctime(last_attempt)
```

Purpose: Identifies users receiving five or more failed login attempts from the same source IP address.

## Review the Suspicious Source IP

```spl
sourcetype=auth_log src_ip="198.51.100.77"
| sort _time
```

Purpose: Displays the complete sequence of activity associated with the suspicious source IP address.

## Detect Failures Followed by Success

```spl
sourcetype=auth_log action=login
| stats count(eval(status="failure")) AS failed_attempts count(eval(status="success")) AS successful_logins earliest(_time) AS first_event latest(_time) AS last_event by user src_ip
| where failed_attempts >= 5 AND successful_logins >= 1
| convert ctime(first_event) ctime(last_event)
```

Purpose: Identifies possible credential compromise when repeated failures are followed by a successful login from the same source IP address.

# Initial Investigation Notes

## Incident Summary
A series of failed login attempts was observed against the scouting.lee account. Five failed attempts were followed by a successful login from the same source IP address. The activity is suspicious and may indicate password guessing or unauthorized access.
## Account Involved
scouting.lee
## Source IP
198.51.100.77
## Timeline
- 09:05:10 UTC - First failed login attempt
- 09:05:18 UTC - Second failed login attempt
- 09:05:26 UTC - Third failed login attempt
- 09:05:34 UTC - Fourth failed login attempt
- 09:05:42 UTC - Fifth failed login attempt
- 09:06:03 UTC - Successful login from the same source IP
## Evidence
- five failed authentication attempts
- same username
- same source IP
- successful login shortly afterward
- no evidence yet showing what the account did after login
## Initial Assessment
The activity could be a brute force or password guessing attempt. Since there were multiple failed login attempts followed by a successful login, it is possible that the correct password was eventually entered. However, the authentication log by itself does not prove that the login was unauthorized or that the account was compromised.
## Additional Evidence Needed
- MFA authentication logs
- Device information
- Geographic login location
- User confirmation of the login
- VPN logs
- Endpoint activity
- Files accessed after authentication
- Other authentication attempts from the same IP address
## Recommended Containment
- Contact the account owner to verify whether the login was legitimate.
- Temporarily disable the account if unauthorized access is suspected.
- Revoke active sessions.
- Reset the user's password.
- Require MFA verification.
- Monitor the source IP for additional suspicious activity.
- Preserve relevant logs for further investigation.
## Lessons Learned
This investigation showed me that repeated failed logins followed by a successful login can be an important indicator of suspicious activity. I also learned that one log source is not enough to prove account compromise. Additional evidence is needed before making a final conclusion.

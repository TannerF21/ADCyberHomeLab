Offensive Findings Report
SSH Brute Force (Hydra)

Objective: Test password strength and logging on SSH.
Command: hydra -l bjohnson -P ~/passwords.txt ssh://10.10.10.184
Result: Multiple failed logins recorded in /var/log/auth.log. Authentication logging works, but no lockout or rate-limiting was detected.

2️ LDAP Enumeration

Objective: Enumerate Active Directory users and groups using valid credentials.
Command:

ldapsearch -LLL -x -H ldap://10.10.10.160 \
-D "bjohnson@HOMELAB.LOCAL" -W \
-b "dc=homelab,dc=local" "(objectClass=user)" sAMAccountName memberOf


Result: Successfully retrieved domain users and group membership information, confirming LDAP queries were accessible with basic user privileges.

3️ Kerberoasting (Impacket)

Objective: Extract and attempt to crack Kerberos service ticket hashes.
Command:

impacket-GetUserSPNs homelab.local/bjohnson:'Password123!' \
-dc-ip 10.10.10.160 -outputfile roast.hashes


Result: Service tickets were successfully requested, and offline cracking demonstrated password strength testing for service accounts.

Summary:
Performed three offensive exercises—SSH brute-force, LDAP enumeration, and Kerberoasting—to simulate common credential and discovery attacks. Results confirmed proper network communication, 
AD integration, and realistic attack visibility for future defensive tuning.

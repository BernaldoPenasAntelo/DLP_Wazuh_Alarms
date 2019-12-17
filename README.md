# DLP_Wazuh_Alarms
Alarms to emulates DLP with wazuh windows agent

To make them work paste them into:
/var/ossec/etc/rules/local_rules.xml


In windows server you must:

# 1.-Enable Windows Security Policies (GPO) — This is done on the Windows Agent
On the Server Manager dashboard:
Tools → Local Security policy → Local Policies → Audit Policies
From here we can set  the Audit Object Access policy to log successes and failures

# 2.-Setting up the directory we want to monitor
In order for us to test this, we will want to create a test directory and set the permissions. As an example you can create a directory in C:\tmp. From here we will set the windows security policy to audit this folder. Note- Selecting “Everyone” as the principal ensures the policy is active for every user that attempts to access the file.

Right click:
Properties → Security → Advanced → Auditing → Click Add → Select Principal → Everyone


# 3.-We need to configure the Wazuh agent to monitor the previous directory:

/var/ossec/etc/ossec.conf

'''<syscheck>
    <directories check_all="yes" whodata="yes">C:\tmp</directories>
</syscheck>'''

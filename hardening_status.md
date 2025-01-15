### Hardening Requirements and implementation status
| No. | Requirement |                                                                                        |
|:---:|-------------|:--------------------------------------------------------------------------------------:|
| 01  | Unnecessary services must be disabled. |                                          [✓]                                           |
| 02  | The accessibility of activated services must be restricted (remark: only SSH) |                                          [✓]                                           |
| 03  | Unused software must not be installed or must be uninstalled. |                                          [✓]                                           |
| 04  | Features that are not required in the software and hardware used must be deactivated |                                          [✓]                                           |
| 05  | Dedicated partitions must be used for growing content that can influence the availability of the system. |     Only one partition was available, should have been done on installation of OS      |
| 06  | Parameters nodev, nosuid and noexec must be set for partitions where this is applicable. |                                          [✓]                                           |
| 07  | Automounting of filesystems using "autofs" must be disabled. |                                          [✓]                                           |
| 08  | USB-Storage must be disabled. |                                          [✓]                                           |
| 09  | The use of "at" and "cron" must be restricted to authorized users. Remark: "at" is not included in image, only "cron" in focus. |                                          [✓]                                           |
| 10  | Sticky bit must be set on all world-writable directories. |                                          [✓]                                           |
| 11  | No regular files that are world writable must exist. |                                          [✓]                                           |
| 12  | Sessions must be automatically terminated after a period of inactivity adapted to the intended use. |                                          [✓]                                           |
| 13  | The default user "umask" must be 027 or more restrictive. |                                          [✓]                                           |
| 14  | Not needed SUID and SGID bits must be removed from executables. |                                          [✓]                                           |
| 15  | Core dumps must be disabled and crash reporting software must be removed. |                                          [✓]                                           |
| 16  | Protection against buffer overflows must be enabled. |                                          [✓]                                           |
| 17  | IPv4 protocol stack must be securely configured. |                                          [✓]                                           |
| 18  | IPv6 protocol stack must be securely configured. |                                          [✓]                                           |
| 19  | The software used must be obtained from trusted sources and checked for integrity | Almost always the case (docker and wazuh use apt gpg keys etc), but cant be guaranteed |
| 20  | It is needed to use releases of Linux distributions which are supported by their vendor. Absolutely necessary is security vulnerability support |                                          [✓]                                           |
| 21  | If needed, active software licenses must be installed to ensure security updates |                                          [✓]                                           |
| 22  | Known vulnerabilities in the software or hardware of the system must be fixed or protected against misuse |                                          [✓]                                           |
| 23  | GPG check for repository server must be activated and corresponding keys for trustable repositories must be configured. |                                          [✓]                                           |
| 24  | The operating system must have an Endpoint Detection and Response (EDR) solution|                          IDS is used, but just for monitoring                          |
| 25  | User accounts must ensure the unique identification of the user |                                          [✓]                                           |
| 26  | System accounts must be non-login. |                                          [✓]                                           |
| 27  | User accounts must be protected with at least one authentication attribute. |                                          [✓]                                           |         |
| 28  | Privileged user accounts must be protected with at least two authentication attributes from different factors. |                                          [✓]                                           |
| 29  | Authentication must be used for single user mode. |                                          [ ]                                           |
| 30  | The administration of the operating system must be done via a network interface which is independent from the production network. |              Not possible, since only one network interface is available               |
| 31  | Administrative services and accesses must be bound to only those interfaces that have been set up to administer. |                        only one network interface is available                         |
| 32  | Network based access used for operating system administration must have integrity protection, be encrypted and securely authenticated. |                                          [✓]                                           |
| 33  | If the system is not located in a room with at least protection class "high" (PC3), the BIOS and, if available, other options for local management must be secured against unauthorized access. |                       Protection level of the room is not known                        |
| 34  | If the system is not located in a room with at least protection class "high" (PC3), used data storages must be fully encrypted. |                       Protection level of the room is not known                        |
| 35  | Auditing must be enabled at boot by setting a kernel parameter. |                                          [✓]                                           |
| 36  | Log rotation for logfiles must be configured. |                            Logs etc are handled by the IDS                             |
| 37  | System time must be synchronized against a reference time source. |                                          [✓]                                           |
| 38  | Applicable retention and deletion periods must be observed for security-relevant logging data that is recorded locally. |                                          [✓]                                           |
| 39  | Security-relevant logging data must be provided to a SIDR solution in near-real-time. |                                  IDS is used instead                                   |
| 40  | "auditd" service must be used to log security relevant events. |                                          [✓]                                           |
| 41  | Syscalls "execve" (execute program) must be logged. |                                          [✓]                                           |
| 42  | System events must be logged. |                                          [✓]                                           |
| 43  | Access and Authentication events must be logged. |                                          [✓]                                           |
| 44  | Account and Group Management events must be logged. |                                          [✓]                                           |
| 45  | Configuration Change events must be logged. |                                          [✓]                                           |
| 46  | Auditd configuration must be immutable. |                                          [✓]                                           |
| 47  | Security relevant logging data must be sent to a remote system directly after their creation. |                                Should be covered by IDS                                |
| 48  | For security-relevant logging data that is forwarded to the separate log server, compliance with the applicable retention and deletion periods must be ensured. |                                   Cant be guaranteed                                   |
| 49  | If RSyslog is used, the default permission of 640 or more restrictive for logfiles must be configured. |                       Rsyslog is not used, instead using the IDS                       |
| 50  | If RSyslog is used, at least one central logging server must be configured. |                       Rsyslog is not used, instead using the IDS                       |
| 51  | If Syslog-NG is used, the default permission of 640 or more restrictive for logfiles must be configured. |                      Syslog-NG is not used, instead using the IDS                      |
| 52  | If Syslog-NG is used, at least one central logging server must be configured. |                      Syslog-NG is not used, instead using the IDS                      |
| 53  | If passwords are used as an authentication attribute, "Shadow Password Suite" must be configured to protect passwords by using a secure hashing function. Passwords must be kept at least 1 day and must be changed latest after 365 days. |                                          [✓]                                           |
| 54  | If PAM is used, it needs to be reconfigured to use strong salted password hash functions while doing many calculation rounds to protect passwords. |                                          [✓]                                           |
| 55  | If PAM is used, password rules must be configured for PAM to force the use of passwords with a minimum length of 12 characters and a combination of three out of the following categories: upper cases, lower case, numbers and special characters. |                                          [✓]                                           |
| 56  | If a password is used as an authentication attribute for technical accounts, it must have at least 30 characters and contain three of the following categories: lower-case letters, upper-case letters, digits and special characters. (applicable for ZAM "virtual user") |                                          [✓]                                           |
| 57 | If a password is used as an authentication attribute, the reuse of previous passwords must be prevented. |                                          [✓]                                           |
| 58 | If PAM is used, a protection against brute force and dictionary attacks that hinder password guessing must be configured in PAM. |                                          [✓]                                           |
| 59  | If PAM is used , PAM must be configured that motd did not contain any sensitive data. |                                          [✓]                                           |
| 60  | If iptables or ufw is used, policies for loopback traffic must be configured |                                          [✓]                                           |
| 61  | If iptables or ufw is used, rules for inbound and (if used) forwarding connections must be configured |                                          [✓]                                           |
| 62  | If iptables or ufw is used, policies must exist for all ports in listening state |                                          [✓]                                           |
| 63  | If iptables or ufw is used, the default policy for incoming or forwarding traffic has be to drop it |                                          [✓]                                           |
| 64  | If a system has Internet facing services, is a virtualization or container host, a MAC solution must be used to restrict these services respectively guest VMs. |                          Apparmor is used instead of SELinux                           |
| 65  | If SELinux is used, it must not be disabled in bootloader configuration. |                                          Apparmor is used instead of SELinux                                             |
| 66  | If SELinux is used, it must be run in "enforcing" mode to actually enforce policy. |                                          Apparmor is used instead of SELinux                                             |
| 67  | If SELinux is used, the policy must be configured. |                                          Apparmor is used instead of SELinux                                             |
| 68  | If SELinux is used, SETroubleshoot and MCS Translation Service must not be installed. |                                         Apparmor is used instead of SELinux                                             |
| 69  | If AppArmor is used, it must not be disabled in bootloader configuration. |                                          [✓]                                           |
| 70  | If AppArmor is used, its state must be enforced. |                                          [✓]                                           |
| 71  | No legacy + entries must exist in files passwd, shadows and group. |                                          [✓]                                           |
| 72  | A user's home directory must be owned by the user and have mode 750 or more restrictive. |                                          [✓]                                           |
| 73  | Default group for the root account must be GID 0. |                                          [✓]                                           |
| 74  | Root must be the only UID 0 account. |                                          [✓]                                           |
| 75  | All groups in /etc/passwd must exist in /etc/group. |                                          [✓]                                           |
| 76  | No duplicate UIDs and GIDs must exist. |                                          [✓]                                           |
| 77  | No duplicate user or group names must exist. |                                          [✓]                                           |
| 78  | The shadow group must be empty (only Debian-based Linux distributions). |                                          [✓]                                           |
| 79  | No files and directories without assigned user or group must exist. |                                          [na]                                          |
| 80  | Permissions of security relevant configuration files must have the distribution default values or more restrictive (if you want more restrictive, execute distributed script: ```req_80.sh```). |                                          [✓]                                           |



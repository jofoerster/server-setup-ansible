# Ansible

Jegliche Konfiguration und Installation der Komponenten (auf den Linux-Servern) sollte über Ansible durchgeführt werden

Das Hauptplaybook ist das ```setup_server.yml``` Playbook. <br>
Nach Ausführung dieses Playbooks sollen die Server komplett lauffähig und fertig eingerichtet sein.
In dem Playbook werden die einzelnen Playbooks importiert. In diesen wird dann festgelegt, auf welcher Servergruppe (bsp. revproxy, pipeline, docker) die Tasks dann ausgeführt werden

Unter ```playbook/files/group_vars``` können Variablen für die einzelnen Servergruppen angelegt werden, die dann zur Laufzeit automatisch importiert werden.

Für Secrets/Keys etc muss Ansible Vault verwendet werden, danach können die verschlüsselten Dateien/Strings auch sicher im Git abgelegt werden.
Dafür muss zuerst das Ansible Vault Plugin in der jeweiligen IDE installiert werden. <br>
Danach können damit bereits bestehende verschlüsselte Dateien geöffnet werden oder neue Dateien und Strings verschlüsselt werden.
Den Schlüssel für den Vault findet man in Gitlab unter den [CICD Variablen](https://gitlab.lrz.de/secsys2425/infrastruktur/ansible/-/settings/ci_cd)

## Achtung:
**Die UFW-Firewall braucht für einen Docker-Container immer eine Incoming + Forward Regel, damit die Verbindung von außen möglich ist!!!**

Die **Incoming Regel** muss übereinstimmen mit dem **Host-Port** in Docker, die **Forward/Route Regel** mit dem gewählten **Container-Port**.
Optional kann auch noch eine 2 Forward-Regel hinzugefügt werden (mit dem Docker-Network Interface als Interface), sodass aus dem Container auch über den Gateway auf andere Container zugegriffen werden kann (direkt innerhalb des Containers über **containername**:**Container-Port** ist immer möglich)

Am einfachsten ist es, die custom Rolle *add_firewall_rule* zu benutzen mit den entsprechenden Parametern:
```
- name: HTTPS-Traffic erlauben
  ansible.builtin.include_role:
    name: add_firewall_rule
  vars:
    firewall_rule_protocol: "tcp"
    firewall_rule_host_port: "{{ nginx_host_port }}"
    firewall_rule_container_port: "{{ revproxy_container_port }}"
```
Der dazugehörige Docker Container:
```
- name: Nginx Container erstellen
  community.docker.docker_container:
    name: "{{ revproxy_container_name }}"
    image: "{{ nginx_container_image }}"
    ports:
      - "{{ nginx_host_port }}:{{ revproxy_container_port }}"
```
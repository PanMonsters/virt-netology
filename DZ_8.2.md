# Домашнее задание к занятию "8.2 Работа с Playbook"

---
## Основная часть

##### 1. Приготовьте свой собственный inventory файл `prod.yml`.  

##### 2. Допишите playbook: нужно сделать ещё один play, который устанавливает и настраивает [vector](https://vector.dev).

##### 3. При создании tasks рекомендую использовать модули: `get_url`, `template`, `unarchive`, `file`.      

##### 4. Tasks должны: скачать нужной версии дистрибутив, выполнить распаковку в выбранную директорию, установить vector.

<details><summary></summary>

```
    - name: Install tar
      become: true
      ansible.builtin.yum:
        name: zip
    - name: Get vector distrib
      ansible.builtin.get_url:
        url: "https://packages.timber.io/vector/0.21.1/{{ vector_version }}.tar.gz"
        dest: "./{{ vector_version }}.tar.gz"
        mode: 0755
    - name: Creates directory /src/vector/
      become: true
      ansible.builtin.file:
        path: /src/vector/
        state: directory
        owner: vagrant
        group: vagrant
        mode: 0755
    - name: CP
      become: true
      ansible.builtin.copy:
        src: "./{{ vector_version }}.tar.gz"
        dest: /src/vector/{{ vector_version }}.tar.gz
        mode: 0755
        remote_src: yes
    - name: GUNZP
      ansible.builtin.shell: gunzip -f /src/vector/{{ vector_version }}.tar.gz
    - name: UNZIP
      become: true
      ansible.builtin.unarchive:      
        src: /src/vector/{{ vector_version }}.tar
        dest: /src/vector/
        extra_opts: [--strip-components=2]
        mode: 0755
        remote_src: yes
      ignore_errors: "{{ ansible_check_mode }}"        
    - name: Set environment vector
      become: true
      ansible.builtin.template:
        src: templates/vector.sh.j2
        dest: /etc/profile.d/vector.sh
        mode: 0755
```

</details>

    
##### 5. Запустите `ansible-lint site.yml` и исправьте ошибки, если они есть.

Все данные ошибки были связаны с лишними пробелами в конце строк и исправлены   

<details><summary></summary>

```
panmonster@panmonster-PC:~/ansible_8.2/playbook5$ ansible-lint site.yml
WARNING  Listing 5 violation(s) that are fatal
[201] Trailing whitespace
site.yml:28
        mode: 0755   

[201] Trailing whitespace
site.yml:34
        mode: 0755 

[201] Trailing whitespace
site.yml:35
        remote_src: yes    

[201] Trailing whitespace
site.yml:44
        mode: 0755 

[201] Trailing whitespace
site.yml:51
        mode: 0755    
        
```

</details>

##### 6. Попробуйте запустить playbook на этом окружении с флагом `--check`.
    
<details><summary></summary>

```
panmonster@panmonster-PC:~/ansible_8.2/playbook5$ ansible-playbook site.yml -i inventory/prod.yml --check

PLAY [Install Clickhouse] ******************************************************

TASK [Gathering Facts] *********************************************************
ok: [clickhouse-01]

TASK [Install tar] *************************************************************
ok: [clickhouse-01]

TASK [Get vector distrib] ******************************************************
ok: [clickhouse-01]

TASK [Creates directory /src/vector/] ******************************************
ok: [clickhouse-01]

TASK [CP] **********************************************************************
changed: [clickhouse-01]

TASK [GUNZP] *******************************************************************
skipping: [clickhouse-01]

TASK [UNZIP] *******************************************************************
skipping: [clickhouse-01]

TASK [Set environment vector] **************************************************
ok: [clickhouse-01]

TASK [Get clickhouse distrib] **************************************************
ok: [clickhouse-01] => (item=clickhouse-client)
ok: [clickhouse-01] => (item=clickhouse-server)
failed: [clickhouse-01] (item=clickhouse-common-static) => {"ansible_loop_var": "item", "changed": false, "dest": "./clickhouse-common-static-22.3.3.44.rpm", "elapsed": 0, "gid": 1000, "group": "vagrant", "item": "clickhouse-common-static", "mode": "0664", "msg": "Request failed", "owner": "vagrant", "response": "HTTP Error 404: Not Found", "size": 246310036, "state": "file", "status_code": 404, "uid": 1000, "url": "https://packages.clickhouse.com/rpm/stable/clickhouse-common-static-22.3.3.44.noarch.rpm"}

TASK [Get clickhouse distrib] **************************************************
ok: [clickhouse-01]

TASK [Install clickhouse packages] *********************************************
ok: [clickhouse-01]

TASK [Flash handlers] **********************************************************

TASK [Pause for 10 second for start servises] **********************************
Pausing for 10 seconds
(ctrl+C then 'C' = continue early, ctrl+C then 'A' = abort)
ok: [clickhouse-01]

TASK [Create database] *********************************************************
skipping: [clickhouse-01]

PLAY RECAP *********************************************************************
clickhouse-01              : ok=9    changed=1    unreachable=0    failed=0    skipped=3    rescued=1    ignored=0 
```

</details>

##### 7. Запустите playbook на `prod.yml` окружении с флагом `--diff`. Убедитесь, что изменения на системе произведены.
    
<details><summary></summary>

```
panmonster@panmonster-PC:~/ansible_8.2/playbook5$ ansible-playbook site.yml -i inventory/prod.yml --diff

PLAY [Install Clickhouse] **********************************************************************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Install tar] *****************************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Get vector distrib] **********************************************************************************************************************************************************************************
changed: [clickhouse-01]

TASK [Creates directory /src/vector/] **********************************************************************************************************************************************************************
--- before
+++ after
@@ -1,6 +1,6 @@
 {
-    "group": 0,
-    "owner": 0,
+    "group": 1000,
+    "owner": 1000,
     "path": "/src/vector/",
-    "state": "absent"
+    "state": "directory"
 }

changed: [clickhouse-01]

TASK [CP] **************************************************************************************************************************************************************************************************
changed: [clickhouse-01]

TASK [GUNZP] ***********************************************************************************************************************************************************************************************
changed: [clickhouse-01]

TASK [UNZIP] ***********************************************************************************************************************************************************************************************
changed: [clickhouse-01]

TASK [Set environment vector] ******************************************************************************************************************************************************************************
--- before
+++ after: /home/panmonster/.ansible/tmp/ansible-local-22149x1zmqjpl/tmpitj7xst9/vector.sh.j2
@@ -0,0 +1,5 @@
+# Warning: This file is Ansible Managed, manual changes will be overwritten on next playbook run.
+#!/usr/bin/env bash
+
+export VECTOR_HOME=/src/vector
+export PATH=$PATH:$VECTOR_HOME/bin

changed: [clickhouse-01]
```

</details>

##### 8. Повторно запустите playbook с флагом `--diff` и убедитесь, что playbook идемпотентен.
    
<details><summary></summary>

```
panmonster@panmonster-PC:~/ansible_8.2/playbook5$ ansible-playbook site.yml -i inventory/prod.yml --diff

PLAY [Install Clickhouse] **********************************************************************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Install tar] *****************************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Get vector distrib] **********************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Creates directory /src/vector/] **********************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [CP] **************************************************************************************************************************************************************************************************
changed: [clickhouse-01]

TASK [GUNZP] ***********************************************************************************************************************************************************************************************
changed: [clickhouse-01]

TASK [UNZIP] ***********************************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Set environment vector] ******************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Get clickhouse distrib] ******************************************************************************************************************************************************************************
ok: [clickhouse-01] => (item=clickhouse-client)
ok: [clickhouse-01] => (item=clickhouse-server)
failed: [clickhouse-01] (item=clickhouse-common-static) => {"ansible_loop_var": "item", "changed": false, "dest": "./clickhouse-common-static-22.3.3.44.rpm", "elapsed": 0, "gid": 1000, "group": "vagrant", "item": "clickhouse-common-static", "mode": "0664", "msg": "Request failed", "owner": "vagrant", "response": "HTTP Error 404: Not Found", "size": 246310036, "state": "file", "status_code": 404, "uid": 1000, "url": "https://packages.clickhouse.com/rpm/stable/clickhouse-common-static-22.3.3.44.noarch.rpm"}

TASK [Get clickhouse distrib] ******************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Install clickhouse packages] *************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Flash handlers] **************************************************************************************************************************************************************************************

TASK [Pause for 10 second for start servises] **************************************************************************************************************************************************************
Pausing for 10 seconds
(ctrl+C then 'C' = continue early, ctrl+C then 'A' = abort)
ok: [clickhouse-01]

TASK [Create database] *************************************************************************************************************************************************************************************
ok: [clickhouse-01]

PLAY RECAP *************************************************************************************************************************************************************************************************
clickhouse-01              : ok=12   changed=2    unreachable=0    failed=0    skipped=0    rescued=1    ignored=0   


TASK [Get clickhouse distrib] ******************************************************************************************************************************************************************************
changed: [clickhouse-01] => (item=clickhouse-client)
changed: [clickhouse-01] => (item=clickhouse-server)
failed: [clickhouse-01] (item=clickhouse-common-static) => {"ansible_loop_var": "item", "changed": false, "dest": "./clickhouse-common-static-22.3.3.44.rpm", "elapsed": 0, "item": "clickhouse-common-static", "msg": "Request failed", "response": "HTTP Error 404: Not Found", "status_code": 404, "url": "https://packages.clickhouse.com/rpm/stable/clickhouse-common-static-22.3.3.44.noarch.rpm"}

TASK [Get clickhouse distrib] ******************************************************************************************************************************************************************************
changed: [clickhouse-01]

TASK [Install clickhouse packages] *************************************************************************************************************************************************************************
changed: [clickhouse-01]

TASK [Flash handlers] **************************************************************************************************************************************************************************************

RUNNING HANDLER [Start clickhouse service] *****************************************************************************************************************************************************************
changed: [clickhouse-01]

TASK [Pause for 10 second for start servises] **************************************************************************************************************************************************************
Pausing for 10 seconds
(ctrl+C then 'C' = continue early, ctrl+C then 'A' = abort)
ok: [clickhouse-01]

TASK [Create database] *************************************************************************************************************************************************************************************
changed: [clickhouse-01]

PLAY RECAP *************************************************************************************************************************************************************************************************
clickhouse-01              : ok=13   changed=10   unreachable=0    failed=0    skipped=0    rescued=1    ignored=0 
```

</details>

##### 9. Подготовьте README.md файл по своему playbook. В нём должно быть описано: что делает playbook, какие у него есть параметры и теги.

<details><summary></summary>
    
[Ссылка на README.md](https://github.com/PanMonsters/Ansible_8.2/blob/5efc200f95295416946214d6e9ed9af96cd3d76c/README.md)

</details>

##### 10. Готовый playbook выложите в свой репозиторий, поставьте тег 08-ansible-02-playbook на фиксирующий коммит, в ответ предоставьте ссылку на него.
     
<details><summary></summary>

[Ссылка на репозиторий](https://github.com/PanMonsters/Ansible_8.2/tree/5efc200f95295416946214d6e9ed9af96cd3d76c)

</details>


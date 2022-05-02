# Домашнее задание к занятию "08.03 Использование Yandex Cloud"

---
## Основная часть

##### 1. Допишите playbook: нужно сделать ещё один play, который устанавливает и настраивает lighthouse.

##### 2. При создании tasks рекомендую использовать модули: `get_url`, `template`, `yum`, `apt`.

##### 3. Tasks должны: скачать статику lighthouse, установить nginx или любой другой webserver, настроить его конфиг для открытия lighthouse, запустить webserver. 

##### 4. Приготовьте свой собственный inventory файл `prod.yml`.

<details><summary></summary>

```
---
- name: Install Nginx
  hosts: lighthouse
  handlers:
    - name: Start nginx
      become: true
      ansible.builtin.command: nginx
    - name: Reload nginx
      become: true
      ansible.builtin.command: nginx -s reload
  tasks:
    - name: NGINX | Install eper-release
      become: true
      ansible.builtin.yum:
        name: epel-release
        state: present
    - name: NGINX | Install Nginx
      become: true
      ansible.builtin.yum:
        name: nginx
        state: present
      notify: Start nginx
    - name: NGINX | Create general config
      become: true
      ansible.builtin.template:
        src: templates/nginx.conf.j2
        dest: /etc/nginx/nginx.conf
        mode: 0644
      notify: Reload nginx
- name: Install Lighthouse
  hosts: lighthouse
  handlers:
    - name: Reload nginx
      become: true
      ansible.builtin.command: nginx -s reload
  pre_tasks:
    - name: Lighthouse | install git
      become: true
      ansible.builtin.yum:
        name: git
        state: present
  tasks:
    - name: Lighthouse | Copy from git
      become: true
      ansible.builtin.git:
        repo: "{{ lighthouse_vcs }}"
        version: master
        dest: "{{ lighthouse_location_dir }}"
    - name: Lighthouse | Create lighthouse config
      become: true
      ansible.builtin.template:
        src: lighthouse.conf.j2
        dest: /etc/nginx/conf.d/default.conf
        mode: 0644     
      notify: Reload nginx
- name: Install Clickhouse
  hosts: clickhouse
# handlers часть которая запрашивается различными плеями при её упоменании через  notify: Start clickhouse service
  handlers:
    - name: Start clickhouse service
      become: true
      ansible.builtin.service:
        name: clickhouse-server
        state: restarted
  tasks:
# block парамет говорящий об ипользовании цикла в этом плее например кусгксу
    - block:
        - name: Get clickhouse distrib
          ansible.builtin.get_url:
            url: "https://packages.clickhouse.com/rpm/stable/{{ item }}-{{ clickhouse_version }}.noarch.rpm"
            dest: "./{{ item }}-{{ clickhouse_version }}.rpm"
          with_items: "{{ clickhouse_packages }}"
# rescue блок использующийся появлении ошибки в основном плее и перезапуске его с выданными параметрами
      rescue:
        - name: Get clickhouse distrib
          ansible.builtin.get_url:
            url: "https://packages.clickhouse.com/rpm/stable/clickhouse-common-static-{{ clickhouse_version }}.x86_64.rpm"
            dest: "./clickhouse-common-static-{{ clickhouse_version }}.rpm"
    - name: Install clickhouse packages
      become: true
      ansible.builtin.yum:
        name:
          - clickhouse-common-static-{{ clickhouse_version }}.rpm
          - clickhouse-client-{{ clickhouse_version }}.rpm
          - clickhouse-server-{{ clickhouse_version }}.rpm
      notify: Start clickhouse service
    - name: Flash handlers
      ansible.builtin.meta: flush_handlers
    - name: Pause for 10 second for start servises
      pause:
        seconds: 10
    - name: Create database
      ansible.builtin.command: "clickhouse-client -h 127.0.0.1 -q 'create database logs;'"
      register: create_db
      failed_when: create_db.rc != 0 and create_db.rc !=82
      changed_when: create_db.rc == 0
    - name: CLICKHOUSE | Create general config
      become: true
      ansible.builtin.template:
        src: templates/config.xml.j2
        dest: /etc/clickhouse-server/config.xml
        mode: 0644
      notify: Start clickhouse service
- name: Install Vector
  hosts: vector
  tasks:
    - name: VECTOR | Install rpm
      become: true
      ansible.builtin.yum:
        name: "{{ vector_url }}"
        state: present
    - name: VECTOR | Template config
      become: true
      ansible.builtin.template:
        src: templates/vector.yml.j2
        dest: vector.yml
        mode: "0644"
        owner: "{{ ansible_user_id }}"
        group: "{{ ansible_user_gid }}"
        validate: vector validate --no-environment --config-yaml %s
    - name: VECTOR | Create systemd unit
      become: true
      ansible.builtin.template:
        src: templates/vector.service.j2
        dest: /etc/systemd/system/vector.service
        mode: "0644"
        owner: "{{ ansible_user_id }}"
        group: "{{ ansible_user_gid }}"
    - name: VECTOR | Start service
      become: true
      ansible.builtin.systemd:
        name: vector
        state: started
        daemon_reload: true
```

</details>

##### 5. Запустите `ansible-lint site.yml` и исправьте ошибки, если они есть.

<details><summary></summary>

Ошибок не было обнаружено.

</details>

##### 6. Попробуйте запустить playbook на этом окружении с флагом `--check`.
    
<details><summary></summary>

```
panmonster@PanMonster-PC:~/Ansible_8.2/playbook$ ansible-playbook site.yml -i inventory/prod.yml --check

PLAY [Install Nginx] **************************************************************************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************************************************************
ok: [clickhouse-02]

TASK [NGINX | Install eper-release] ***********************************************************************************************************************************************************************
ok: [clickhouse-02]

TASK [NGINX | Install Nginx] ******************************************************************************************************************************************************************************
ok: [clickhouse-02]

TASK [NGINX | Create general config] **********************************************************************************************************************************************************************
ok: [clickhouse-02]

PLAY [Install Lighthouse] *********************************************************************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************************************************************
ok: [clickhouse-02]

TASK [Lighthouse | install git] ***************************************************************************************************************************************************************************
ok: [clickhouse-02]

TASK [Lighthouse | Copy from git] *************************************************************************************************************************************************************************
ok: [clickhouse-02]

TASK [Lighthouse | Create lighthouse config] **************************************************************************************************************************************************************
ok: [clickhouse-02]

PLAY [Install Clickhouse] *********************************************************************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Get clickhouse distrib] *****************************************************************************************************************************************************************************
ok: [clickhouse-01] => (item=clickhouse-client)
ok: [clickhouse-01] => (item=clickhouse-server)
failed: [clickhouse-01] (item=clickhouse-common-static) => {"ansible_loop_var": "item", "changed": false, "dest": "./clickhouse-common-static-22.3.3.44.rpm", "elapsed": 0, "gid": 1000, "group": "centos", "item": "clickhouse-common-static", "mode": "0664", "msg": "Request failed", "owner": "centos", "response": "HTTP Error 404: Not Found", "secontext": "unconfined_u:object_r:user_home_t:s0", "size": 246310036, "state": "file", "status_code": 404, "uid": 1000, "url": "https://packages.clickhouse.com/rpm/stable/clickhouse-common-static-22.3.3.44.noarch.rpm"}

TASK [Get clickhouse distrib] *****************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Install clickhouse packages] ************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Flash handlers] *************************************************************************************************************************************************************************************

TASK [Pause for 10 second for start servises] *************************************************************************************************************************************************************
Pausing for 10 seconds
(ctrl+C then 'C' = continue early, ctrl+C then 'A' = abort)
ok: [clickhouse-01]

TASK [Create database] ************************************************************************************************************************************************************************************
skipping: [clickhouse-01]

TASK [CLICKHOUSE | Create general config] *****************************************************************************************************************************************************************
ok: [clickhouse-01]

PLAY [Install Vector] *************************************************************************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************************************************************
ok: [clickhouse-03]

TASK [VECTOR | Install rpm] *******************************************************************************************************************************************************************************
ok: [clickhouse-03]

TASK [VECTOR | Template config] ***************************************************************************************************************************************************************************
ok: [clickhouse-03]

TASK [VECTOR | Create systemd unit] ***********************************************************************************************************************************************************************
ok: [clickhouse-03]

TASK [VECTOR | Start service] *****************************************************************************************************************************************************************************
changed: [clickhouse-03]

PLAY RECAP ************************************************************************************************************************************************************************************************
clickhouse-01              : ok=5    changed=0    unreachable=0    failed=0    skipped=1    rescued=1    ignored=0   
clickhouse-02              : ok=8    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
clickhouse-03              : ok=5    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

</details>

##### 7. Запустите playbook на `prod.yml` окружении с флагом `--diff`. Убедитесь, что изменения на системе произведены.
    
<details><summary></summary>

```
panmonster@PanMonster-PC:~/Ansible_8.2/playbook$ ansible-playbook site.yml -i inventory/prod.yml --diff

PLAY [Install Nginx] ***********************************************************

TASK [Gathering Facts] *********************************************************
ok: [clickhouse-02]

TASK [NGINX | Install eper-release] ********************************************
ok: [clickhouse-02]

TASK [NGINX | Install Nginx] ***************************************************
changed: [clickhouse-02]

TASK [NGINX | Create general config] *******************************************
--- before: /etc/nginx/nginx.conf
+++ after: /home/panmonster/.ansible/tmp/ansible-local-5586xy2xc6b3/tmpe40f0x71/nginx.conf.j2
@@ -1,9 +1,6 @@
-# For more information on configuration, see:
-#   * Official English Documentation: http://nginx.org/en/docs/
-#   * Official Russian Documentation: http://nginx.org/ru/docs/
+user root;
+worker_processes 1;
 
-user nginx;
-worker_processes auto;
 error_log /var/log/nginx/error.log;
 pid /run/nginx.pid;
 
@@ -36,7 +33,7 @@
     include /etc/nginx/conf.d/*.conf;
 
     server {
-        listen       80;
+	listen       80;
         listen       [::]:80;
         server_name  _;
         root         /usr/share/nginx/html;
@@ -48,7 +45,7 @@
         location = /404.html {
         }
 
-        error_page 500 502 503 504 /50x.html;
+	error_page 500 502 503 504 /50x.html;
         location = /50x.html {
         }
     }

changed: [clickhouse-02]

RUNNING HANDLER [Start nginx] **************************************************
changed: [clickhouse-02]

RUNNING HANDLER [Reload nginx] *************************************************
changed: [clickhouse-02]

PLAY [Install Lighthouse] ******************************************************

TASK [Gathering Facts] *********************************************************
ok: [clickhouse-02]

TASK [Lighthouse | install git] ************************************************
changed: [clickhouse-02]

TASK [Lighthouse | Copy from git] **********************************************
>> Newly checked out d701335c25cd1bb9b5155711190bad8ab852c2ce
changed: [clickhouse-02]

TASK [Lighthouse | Create lighthouse config] ***********************************
--- before
+++ after: /home/panmonster/.ansible/tmp/ansible-local-5586xy2xc6b3/tmpn0pmzn72/lighthouse.conf.j2
@@ -0,0 +1,11 @@
+server {
+    listen       80;
+    server_name  localhost
+    
+    access_log  /var/log/nginx lighthouse_access.log  main;
+    
+    location / {
+        root   /home/aragast/lighthouse;
+        index  index.html;
+    }
+}

changed: [clickhouse-02]

RUNNING HANDLER [Reload nginx] *************************************************
changed: [clickhouse-02]

PLAY [Install Clickhouse] ******************************************************

TASK [Gathering Facts] *********************************************************
ok: [clickhouse-01]

TASK [Get clickhouse distrib] **************************************************
changed: [clickhouse-01] => (item=clickhouse-client)
changed: [clickhouse-01] => (item=clickhouse-server)
failed: [clickhouse-01] (item=clickhouse-common-static) => {"ansible_loop_var": "item", "changed": false, "dest": "./clickhouse-common-static-22.3.3.44.rpm", "elapsed": 0, "item": "clickhouse-common-static", "msg": "Request failed", "response": "HTTP Error 404: Not Found", "status_code": 404, "url": "https://packages.clickhouse.com/rpm/stable/clickhouse-common-static-22.3.3.44.noarch.rpm"}

TASK [Get clickhouse distrib] **************************************************
changed: [clickhouse-01]

TASK [Install clickhouse packages] *********************************************
changed: [clickhouse-01]

TASK [Flash handlers] **********************************************************

RUNNING HANDLER [Start clickhouse service] *************************************
changed: [clickhouse-01]

TASK [Pause for 10 second for start servises] **********************************
Pausing for 10 seconds
(ctrl+C then 'C' = continue early, ctrl+C then 'A' = abort)
ok: [clickhouse-01]

TASK [Create database] *********************************************************
changed: [clickhouse-01]

TASK [CLICKHOUSE | Create general config] **************************************
--- before: /etc/clickhouse-server/config.xml
+++ after: /home/panmonster/.ansible/tmp/ansible-local-5586xy2xc6b3/tmpfal52o8f/config.xml.j2
@@ -183,10 +183,7 @@
     <!-- <listen_host>0.0.0.0</listen_host> -->
 
     <!-- Default values - try listen localhost on IPv4 and IPv6. -->
-    <!--
-    <listen_host>::1</listen_host>
-    <listen_host>127.0.0.1</listen_host>
-    -->
+    <listen_host>0.0.0.0</listen_host>
 
     <!-- Don't exit if IPv6 or IPv4 networks are unavailable while trying to listen. -->
     <!-- <listen_try>0</listen_try> -->

changed: [clickhouse-01]

RUNNING HANDLER [Start clickhouse service] *************************************
changed: [clickhouse-01]

PLAY [Install Vector] **********************************************************

TASK [Gathering Facts] *********************************************************
ok: [clickhouse-03]

TASK [VECTOR | Install rpm] ****************************************************
changed: [clickhouse-03]

TASK [VECTOR | Template config] ************************************************
--- before
+++ after: /home/panmonster/.ansible/tmp/ansible-local-5586xy2xc6b3/tmpu08k5otv/vector.yml.j2
@@ -0,0 +1,18 @@
+sinks:
+    to_clickhouse:
+        compression: gzip
+        database: logs
+        endpoint: http://51.250.66.6:8123
+        healthcheck: false
+        inputs:
+        - our_log
+        skip_unknown_fields: true
+        table: log
+        type: clickhouse
+sources:
+    our_log:
+        ignore_older_secs: 600
+        include:
+        - /home/aragast/logs/*.log
+        read_from: beginning
+        type: file

changed: [clickhouse-03]

TASK [VECTOR | Create systemd unit] ********************************************
--- before
+++ after: /home/panmonster/.ansible/tmp/ansible-local-5586xy2xc6b3/tmpqo5_hfe1/vector.service.j2
@@ -0,0 +1,11 @@
+[Unit]
+Description=Vector service
+After=network.target
+Requires=network-online.target
+[Service]
+User=centos
+Group=1000
+ExecStart=/usr/bin/vector --config-yaml vector.yml --wath-config true
+Restart=always
+[Install]
+WantedBy=multi-user.target

changed: [clickhouse-03]

TASK [VECTOR | Start service] **************************************************
changed: [clickhouse-03]

PLAY RECAP *********************************************************************
clickhouse-01              : ok=8    changed=6    unreachable=0    failed=0    skipped=0    rescued=1    ignored=0   
clickhouse-02              : ok=11   changed=8    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
clickhouse-03              : ok=5    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

</details>

##### 8. Повторно запустите playbook с флагом `--diff` и убедитесь, что playbook идемпотентен.
    
<details><summary></summary>

```
panmonster@PanMonster-PC:~/Ansible_8.2/playbook$ ansible-playbook site.yml -i inventory/prod.yml --diff

PLAY [Install Nginx] **************************************************************************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************************************************************
ok: [clickhouse-02]

TASK [NGINX | Install eper-release] ***********************************************************************************************************************************************************************
ok: [clickhouse-02]

TASK [NGINX | Install Nginx] ******************************************************************************************************************************************************************************
ok: [clickhouse-02]

TASK [NGINX | Create general config] **********************************************************************************************************************************************************************
ok: [clickhouse-02]

PLAY [Install Lighthouse] *********************************************************************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************************************************************
ok: [clickhouse-02]

TASK [Lighthouse | install git] ***************************************************************************************************************************************************************************
ok: [clickhouse-02]

TASK [Lighthouse | Copy from git] *************************************************************************************************************************************************************************
ok: [clickhouse-02]

TASK [Lighthouse | Create lighthouse config] **************************************************************************************************************************************************************
ok: [clickhouse-02]

PLAY [Install Clickhouse] *********************************************************************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Get clickhouse distrib] *****************************************************************************************************************************************************************************
ok: [clickhouse-01] => (item=clickhouse-client)
ok: [clickhouse-01] => (item=clickhouse-server)
failed: [clickhouse-01] (item=clickhouse-common-static) => {"ansible_loop_var": "item", "changed": false, "dest": "./clickhouse-common-static-22.3.3.44.rpm", "elapsed": 0, "gid": 1000, "group": "centos", "item": "clickhouse-common-static", "mode": "0664", "msg": "Request failed", "owner": "centos", "response": "HTTP Error 404: Not Found", "secontext": "unconfined_u:object_r:user_home_t:s0", "size": 246310036, "state": "file", "status_code": 404, "uid": 1000, "url": "https://packages.clickhouse.com/rpm/stable/clickhouse-common-static-22.3.3.44.noarch.rpm"}

TASK [Get clickhouse distrib] *****************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Install clickhouse packages] ************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Flash handlers] *************************************************************************************************************************************************************************************

TASK [Pause for 10 second for start servises] *************************************************************************************************************************************************************
Pausing for 10 seconds
(ctrl+C then 'C' = continue early, ctrl+C then 'A' = abort)
ok: [clickhouse-01]

TASK [Create database] ************************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [CLICKHOUSE | Create general config] *****************************************************************************************************************************************************************
ok: [clickhouse-01]

PLAY [Install Vector] *************************************************************************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************************************************************
ok: [clickhouse-03]

TASK [VECTOR | Install rpm] *******************************************************************************************************************************************************************************
ok: [clickhouse-03]

TASK [VECTOR | Template config] ***************************************************************************************************************************************************************************
ok: [clickhouse-03]

TASK [VECTOR | Create systemd unit] ***********************************************************************************************************************************************************************
ok: [clickhouse-03]

TASK [VECTOR | Start service] *****************************************************************************************************************************************************************************
changed: [clickhouse-03]

PLAY RECAP ************************************************************************************************************************************************************************************************
clickhouse-01              : ok=6    changed=0    unreachable=0    failed=0    skipped=0    rescued=1    ignored=0   
clickhouse-02              : ok=8    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
clickhouse-03              : ok=5    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

</details>

##### 9. Подготовьте README.md файл по своему playbook. В нём должно быть описано: что делает playbook, какие у него есть параметры и теги.

<details><summary></summary>
    
[Ссылка на README.md](https://github.com/PanMonsters/Ansible_8.2/blob/85f00dfb42634172c40ad921faeab5e0e9474ddf/README.md)

</details>

##### 10. Готовый playbook выложите в свой репозиторий, поставьте тег 08-ansible-02-playbook на фиксирующий коммит, в ответ предоставьте ссылку на него.
     
<details><summary></summary>

[Ссылка на репозиторий](https://github.com/PanMonsters/Ansible_8.2/tree/85f00dfb42634172c40ad921faeab5e0e9474ddf)

</details>


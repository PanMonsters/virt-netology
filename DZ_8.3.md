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
clickhouse:
  hosts:
    clickhouse-01:
      ansible_host: 51.250.88.118
      ansible_ssh_user: centos
#      ansible_ssh_pass: vagrant
      
lighthouse:
  hosts:
    clickhouse-02:
      ansible_host: 51.250.82.170
      ansible_ssh_user: centos    
#      ansible_ssh_pass: vagrant
      
vector:
  hosts:
    clickhouse-03:
      ansible_host: 51.250.72.159
      ansible_ssh_user: centos
#      ansible_ssh_pass: vagrant

```

</details>

##### 5. Запустите `ansible-lint site.yml` и исправьте ошибки, если они есть.

<details><summary></summary>

Уменьшить данную строку не имеется возможности, но плейбук отрабатывает с ней без проблем.

panmonster@PanMonster-PC:~/Ansible_8.2/playbook$ ansible-lint site.yml
[204] Lines should be no longer than 160 chars
site.yml:98
      ansible.builtin.command: "clickhouse-client -h 127.0.0.1 -q 'CREATE TABLE IF NOT EXISTS  logs.access_logs ( message String ) ENGINE = MergeTree() ORDER BY tuple()'"

</details>

##### 6. Попробуйте запустить playbook на этом окружении с флагом `--check`.
    
<details><summary></summary>

```
panmonster@PanMonster-PC:~/Ansible_8.2/playbook$ ansible-playbook site.yml -i inventory/prod.yml --check

PLAY [Install Nginx] **************************************************************************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************************************************************
ok: [clickhouse-02]
ok: [clickhouse-03]

TASK [NGINX | Install eper-release] ***********************************************************************************************************************************************************************
ok: [clickhouse-02]
ok: [clickhouse-03]

TASK [NGINX | Install Nginx] ******************************************************************************************************************************************************************************
ok: [clickhouse-02]
ok: [clickhouse-03]

TASK [NGINX | Create general config] **********************************************************************************************************************************************************************
ok: [clickhouse-02]
ok: [clickhouse-03]

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

TASK [Create table] ***************************************************************************************************************************************************************************************
skipping: [clickhouse-01]

TASK [CLICKHOUSE | Create general config] *****************************************************************************************************************************************************************
ok: [clickhouse-01]

PLAY [Install Nginx (vector)] *****************************************************************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************************************************************
ok: [clickhouse-03]

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
ok: [clickhouse-03]

PLAY RECAP ************************************************************************************************************************************************************************************************
clickhouse-01              : ok=5    changed=0    unreachable=0    failed=0    skipped=2    rescued=1    ignored=0   
clickhouse-02              : ok=8    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
clickhouse-03              : ok=10   changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

</details>

##### 7. Запустите playbook на `prod.yml` окружении с флагом `--diff`. Убедитесь, что изменения на системе произведены.
    
<details><summary></summary>

```
panmonster@PanMonster-PC:~/Ansible_8.2/playbook$ ansible-playbook site.yml -i inventory/prod.yml --diff

PLAY [Install Nginx] ***********************************************************

TASK [Gathering Facts] *********************************************************
ok: [clickhouse-02]
ok: [clickhouse-03]

TASK [NGINX | Install eper-release] ********************************************
changed: [clickhouse-02]
changed: [clickhouse-03]

TASK [NGINX | Install Nginx] ***************************************************
changed: [clickhouse-03]
changed: [clickhouse-02]

TASK [NGINX | Create general config] *******************************************
--- before: /etc/nginx/nginx.conf
+++ after: /home/panmonster/.ansible/tmp/ansible-local-1003255tdizic/tmpfyxm99ac/nginx.conf.j2
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
--- before: /etc/nginx/nginx.conf
+++ after: /home/panmonster/.ansible/tmp/ansible-local-1003255tdizic/tmp0b1ycesr/nginx.conf.j2
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

changed: [clickhouse-03]

RUNNING HANDLER [Start nginx] **************************************************
changed: [clickhouse-03]
changed: [clickhouse-02]

RUNNING HANDLER [Reload nginx] *************************************************
changed: [clickhouse-02]
changed: [clickhouse-03]

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
+++ after: /home/panmonster/.ansible/tmp/ansible-local-1003255tdizic/tmp5zqntsi3/lighthouse.conf.j2
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

TASK [Create table] ************************************************************
changed: [clickhouse-01]

TASK [CLICKHOUSE | Create general config] **************************************
--- before: /etc/clickhouse-server/config.xml
+++ after: /home/panmonster/.ansible/tmp/ansible-local-1003255tdizic/tmpdx83uqgi/config.xml.j2
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

PLAY [Install Nginx (vector)] **************************************************

TASK [Gathering Facts] *********************************************************
ok: [clickhouse-03]

PLAY [Install Vector] **********************************************************

TASK [Gathering Facts] *********************************************************
ok: [clickhouse-03]

TASK [VECTOR | Install rpm] ****************************************************
changed: [clickhouse-03]

TASK [VECTOR | Template config] ************************************************
--- before
+++ after: /home/panmonster/.ansible/tmp/ansible-local-1003255tdizic/tmpkgy494sv/vector.yml.j2
@@ -0,0 +1,18 @@
+sinks:
+    to_clickhouse:
+        compression: gzip
+        database: logs
+        endpoint: http://10.128.0.31:8123
+        healthcheck: false
+        inputs:
+        - our_log
+        skip_unknown_fields: true
+        table: access_logs
+        type: clickhouse
+sources:
+    our_log:
+        ignore_older_secs: 600
+        include:
+        - /var/log/nginx/access.log
+        read_from: beginning
+        type: file

changed: [clickhouse-03]

TASK [VECTOR | Create systemd unit] ********************************************
--- before
+++ after: /home/panmonster/.ansible/tmp/ansible-local-1003255tdizic/tmp3yb0oktd/vector.service.j2
@@ -0,0 +1,12 @@
+[Unit]
+Description=Vector service
+After=network.target
+Requires=network-online.target
+[Service]
+User=root
+Group=root
+ExecStart=/usr/bin/vector --config-yaml /etc/vector/vector.yml
+Restart=always
+[Install]
+WantedBy=multi-user.target
+

changed: [clickhouse-03]

TASK [VECTOR | Start service] **************************************************
changed: [clickhouse-03]

PLAY RECAP *********************************************************************
clickhouse-01              : ok=9    changed=7    unreachable=0    failed=0    skipped=0    rescued=1    ignored=0   
clickhouse-02              : ok=11   changed=9    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
clickhouse-03              : ok=12   changed=9    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

</details>

##### 8. Повторно запустите playbook с флагом `--diff` и убедитесь, что playbook идемпотентен.
    
<details><summary></summary>

```
panmonster@PanMonster-PC:~/Ansible_8.2/playbook$ ansible-playbook site.yml -i inventory/prod.yml --diff

PLAY [Install Nginx] **************************************************************************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************************************************************
ok: [clickhouse-02]
ok: [clickhouse-03]

TASK [NGINX | Install eper-release] ***********************************************************************************************************************************************************************
ok: [clickhouse-02]
ok: [clickhouse-03]

TASK [NGINX | Install Nginx] ******************************************************************************************************************************************************************************
ok: [clickhouse-02]
ok: [clickhouse-03]

TASK [NGINX | Create general config] **********************************************************************************************************************************************************************
ok: [clickhouse-02]
ok: [clickhouse-03]

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

TASK [Create table] ***************************************************************************************************************************************************************************************
changed: [clickhouse-01]

TASK [CLICKHOUSE | Create general config] *****************************************************************************************************************************************************************
ok: [clickhouse-01]

PLAY [Install Nginx (vector)] *****************************************************************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************************************************************
ok: [clickhouse-03]

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
ok: [clickhouse-03]

PLAY RECAP ************************************************************************************************************************************************************************************************
clickhouse-01              : ok=7    changed=1    unreachable=0    failed=0    skipped=0    rescued=1    ignored=0   
clickhouse-02              : ok=8    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
clickhouse-03              : ok=10   changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

</details>

##### 9. Подготовьте README.md файл по своему playbook. В нём должно быть описано: что делает playbook, какие у него есть параметры и теги.

<details><summary></summary>
    
[Ссылка на README.md](https://github.com/PanMonsters/Ansible_8.2/blob/2f73e9501c03a30ca3e8ac2d6fa2176b7ffb5cf2/README.md)

</details>

##### 10. Готовый playbook выложите в свой репозиторий, поставьте тег `08-ansible-03-yandex` на фиксирующий коммит, в ответ предоставьте ссылку на него.
     
<details><summary></summary>

[Ссылка на репозиторий](https://github.com/PanMonsters/Ansible_8.2/tree/2f73e9501c03a30ca3e8ac2d6fa2176b7ffb5cf2)

</details>


# Домашнее задание к занятию "8.1. Введение в Ansible"

---
## Подготовка к выполнению

##### 1. Установите ansible версии 2.10 или выше.

<details><summary></summary>

```
panmonster@PanMonster-PC:~/Ansible$ ansible --version
ansible [core 2.12.4]
  config file = None
  configured module search path = ['/home/panmonster/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /home/panmonster/.local/lib/python3.8/site-packages/ansible
  ansible collection location = /home/panmonster/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/local/bin/ansible
  python version = 3.8.10 (default, Mar 15 2022, 12:22:08) [GCC 9.4.0]
  jinja version = 3.1.1
  libyaml = True
```

</details>

##### 2-3. Создайте свой собственный публичный репозиторий на github с произвольным именем и скачайте [playbook](./playbook/) из репозитория с домашним заданием и перенесите его в свой репозиторий.

<details><summary></summary>

[Ссылка на репозиторий](https://github.com/PanMonsters/Ansible_8.1)

</details>

---
## Основная часть

##### 1. Попробуйте запустить playbook на окружении из `test.yml`, зафиксируйте какое значение имеет факт `some_fact` для указанного хоста при выполнении playbook'a.
    
<details><summary></summary>

```
panmonster@PanMonster-PC:~/Ansible_8.1$ ansible-playbook -i inventory/test.yml site.yml

PLAY [Print os facts] ******************************************************************************************************************

TASK [Gathering Facts] *****************************************************************************************************************
ok: [localhost]

TASK [Print OS] ************************************************************************************************************************
ok: [localhost] => {
    "msg": "Ubuntu"
}

TASK [Print fact] **********************************************************************************************************************
ok: [localhost] => {
    "msg": 12
}

PLAY RECAP *****************************************************************************************************************************
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

 </details>

##### 2. Найдите файл с переменными (group_vars) в котором задаётся найденное в первом пункте значение и поменяйте его на 'all default fact'.
    
<details><summary></summary>

```
panmonster@PanMonster-PC:~/Ansible_8.1$ cat group_vars/all/examp.yml
---
  some_fact: 'all default fact'
```

</details>

##### 3. Воспользуйтесь подготовленным (используется `docker`) или создайте собственное окружение для проведения дальнейших испытаний.
    
<details><summary></summary>

```
panmonster@PanMonster-PC:~/Ansible_8.1$ docker run -itd --restart=always --name ubuntu --network host 42a4e3b21923
panmonster@PanMonster-PC:~/Ansible_8.1$ docker run -itd --restart=always --name centos7 --network host bafa54e44377

panmonster@PanMonster-PC:~/Ansible_8.1$ docker ps
CONTAINER ID   IMAGE          COMMAND       CREATED              STATUS              PORTS     NAMES
dd19b5807fa8   42a4e3b21923   "/bin/bash"   About a minute ago   Up About a minute             ubuntu
9c9434adaa01   bafa54e44377   "/bin/bash"   6 minutes ago        Up 6 minutes                  centos7
```

</details>

##### 4. Проведите запуск playbook на окружении из `prod.yml`. Зафиксируйте полученные значения `some_fact` для каждого из `managed host`.
    
<details><summary></summary>

```
panmonster@PanMonster-PC:~/Ansible_8.1$ ansible-playbook -i inventory/prod.yml site.yml

PLAY [Print os facts] ***********************************************************************************************************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************************************************************************************
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] *****************************************************************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ***************************************************************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el"
}
ok: [ubuntu] => {
    "msg": "deb"
}

PLAY RECAP **********************************************************************************************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

##### 5. Добавьте факты в `group_vars` каждой из групп хостов так, чтобы для `some_fact` получились следующие значения: для `deb` - 'deb default fact', для `el` - 'el default fact'.
    
<details><summary></summary>

```
panmonster@PanMonster-PC:~/Ansible_8.1$ cat group_vars/{deb,el}/*
---
some_fact: "deb default fact"
---
some_fact: "el default fact"
```

</details>

##### 6.  Повторите запуск playbook на окружении `prod.yml`. Убедитесь, что выдаются корректные значения для всех хостов.
    
<details><summary></summary>

```
panmonster@PanMonster-PC:~/Ansible_8.1$ ansible-playbook -i inventory/prod.yml site.yml

PLAY [Print os facts] ***********************************************************************************************************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************************************************************************************
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] *****************************************************************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ***************************************************************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}

PLAY RECAP **********************************************************************************************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

```

</details>

##### 7. При помощи `ansible-vault` зашифруйте факты в `group_vars/deb` и `group_vars/el` с паролем `netology`.
    
<details><summary></summary>

```
panmonster@PanMonster-PC:~/Ansible_8.1$ ansible-vault encrypt group_vars/deb/examp.yml
New Vault password:
Confirm New Vault password:
Encryption successful
panmonster@PanMonster-PC:~/Ansible_8.1$ ansible-vault encrypt group_vars/el/examp.yml
New Vault password:
Confirm New Vault password:
Encryption successful

panmonster@PanMonster-PC:~/Ansible_8.1$ cat group_vars/{deb,el}/*
$ANSIBLE_VAULT;1.1;AES256
39316338656561323263316237333036383463663938653139326262386463366161623261313236
6330396235616330386361656539616432636133346434300a383539303735656536623630623533
35303361323236666138663435613831366235316636346364316630646362633365646233636539
6532343361313461320a396331343762636261356536313334646535663665346234303739643837
30643236326365646530663464613337383562343964393864623734316331353137393565336664
3865316332636230356362396362653433323966626436393263
$ANSIBLE_VAULT;1.1;AES256
32656266333664366661373137336231653065356635666263326336363462623733383636643332
3838326261313337633363643564323635323339323338300a616465396232343633336365343331
32616364303063616439663162643738333538313438653063343965373162346265323439326339
6231656232633930640a353264326533643461363835653732613465653235366232326633636435
33623761303664383166336534633965356234633264636263633130663432653038666634316363
3365306335663665666666303038613065633763643232643934
```

</details>

##### 8. Запустите playbook на окружении `prod.yml`. При запуске `ansible` должен запросить у вас пароль. Убедитесь в работоспособности.
    
<details><summary></summary>

```
panmonster@PanMonster-PC:~/Ansible_8.1$ ansible-playbook -i inventory/prod.yml site.yml --ask-vault-pass
Vault password:

PLAY [Print os facts] ******************************************************************************************************************

TASK [Gathering Facts] *****************************************************************************************************************
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] ************************************************************************************************************************
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] **********************************************************************************************************************
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}

PLAY RECAP *****************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

##### 9. Посмотрите при помощи `ansible-doc` список плагинов для подключения. Выберите подходящий для работы на `control node`.
    
<details><summary></summary>

Плагин для подключения к `control node` выбрал 'local'

</details>

##### 10. В `prod.yml` добавьте новую группу хостов с именем  `local`, в ней разместите localhost с необходимым типом подключения.
     
<details><summary></summary>

```
panmonster@PanMonster-PC:~/Ansible_8.1$ cat inventory/prod.yml
---
  el:
    hosts:
      centos7:
        ansible_connection: docker
  deb:
    hosts:
      ubuntu:
        ansible_connection: docker
  local:
    hosts:
      localhost:
        ansible_connection: local
```

</details>

##### 11. Запустите playbook на окружении `prod.yml`. При запуске `ansible` должен запросить у вас пароль. Убедитесь что факты `some_fact` для каждого из хостов определены из верных `group_vars`.
     
<details><summary></summary>

```
panmonster@PanMonster-PC:~/Ansible_8.1$ ansible-playbook -i inventory/prod.yml site.yml --ask-vault-pass
Vault password:

PLAY [Print os facts] ***********************************************************************************************************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************************************************************************************
ok: [ubuntu]
ok: [localhost]
ok: [centos7]

TASK [Print OS] *****************************************************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Ubuntu"
}
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ***************************************************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "all default fact"
}
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}

PLAY RECAP **********************************************************************************************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

##### Заполните `README.md` ответами на вопросы. Сделайте `git push` в ветку `master`. В ответе отправьте ссылку на ваш открытый репозиторий с изменённым `playbook` и заполненным `README.md`.
     
<details><summary></summary>

[Ссылка на репозиторий](https://github.com/PanMonsters/Ansible_8.1)

</details>

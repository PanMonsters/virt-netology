# Домашнее задание к занятию "08.06 Создание собственных modules"

---
## Подготовка к выполнению

<details><summary></summary>

1. Создайте пустой публичных репозиторий в любом своём проекте: `my_own_collection`
2. Скачайте репозиторий ansible: `git clone https://github.com/ansible/ansible.git` по любому удобному вам пути
3. Зайдите в директорию ansible: `cd ansible`
4. Создайте виртуальное окружение: `python3 -m venv venv`
5. Активируйте виртуальное окружение: `. venv/bin/activate`. Дальнейшие действия производятся только в виртуальном окружении
6. Установите зависимости `pip install -r requirements.txt`
7. Запустить настройку окружения `. hacking/env-setup`
8. Если все шаги прошли успешно - выйти из виртуального окружения `deactivate`
9. Ваше окружение настроено, для того чтобы запустить его, нужно находиться в директории `ansible` и выполнить конструкцию `. venv/bin/activate && . hacking/env-setup`

</details>

## Основная часть

Наша цель - написать собственный module, который мы можем использовать в своей role, через playbook. Всё это должно быть собрано в виде collection и отправлено в наш репозиторий.

### Molecule

##### 1. В виртуальном окружении создать новый `my_own_module.py` файл.

##### 2. Наполнить его содержимым.

##### 3. Заполните файл в соответствии с требованиями ansible так, чтобы он выполнял основную задачу: module должен создавать текстовый файл на удалённом хосте по пути, определённом в параметре `path`, с содержимым, определённым в параметре `content`.

##### 4. Проверьте module на исполняемость локально.

<details><summary></summary>

```
(venv) panmonster@panmonster-PC:~/my_own_collection/ansible$ python -m ansible.modules.my_own_module payload.json

{"changed": true, "original_message": "Hellow world!", "message": "file recorder", "invocation": {"module_args": {"path": "/tmp/666.txt", "text": "Hellow world!"}}}
(venv) panmonster@panmonster-PC:~/my_own_collection/ansible$ cat /tmp/666.txt
Hellow world!(venv) panmonster@panmonster-PC:~/my_own_collection/ansible$ 
```

</details>

##### 5. Напишите single task playbook и используйте module в нём.

##### 6. Проверьте через playbook на идемпотентность.

<details><summary></summary>

```
(venv) panmonster@panmonster-PC:~/my_own_collection/ansible$ ansible-playbook site.yml
[WARNING]: You are running the development version of Ansible. You should only run Ansible from "devel" if you are modifying the Ansible engine, or trying out features under development. This is a
rapidly changing source of code and can become unstable at any point.
[WARNING]: No inventory was parsed, only implicit localhost is available
[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'

PLAY [test module] *****************************************************************************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************************************************************************
ok: [localhost]

TASK [test_my_own_module] **********************************************************************************************************************************************************************************
changed: [localhost]

TASK [info] ************************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "STATUS file recorder."
}

PLAY RECAP *************************************************************************************************************************************************************************************************
localhost                  : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

(venv) panmonster@panmonster-PC:~/my_own_collection/ansible$ ansible-playbook site.yml
[WARNING]: You are running the development version of Ansible. You should only run Ansible from "devel" if you are modifying the Ansible engine, or trying out features under development. This is a
rapidly changing source of code and can become unstable at any point.
[WARNING]: No inventory was parsed, only implicit localhost is available
[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'

PLAY [test module] *****************************************************************************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************************************************************************
ok: [localhost]

TASK [test_my_own_module] **********************************************************************************************************************************************************************************
ok: [localhost]

TASK [info] ************************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "STATUS file exists."
}

PLAY RECAP *************************************************************************************************************************************************************************************************
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0 
```

</details>

##### 7. Выйдите из виртуального окружения.

##### 8. Инициализируйте новую collection: `ansible-galaxy collection init my_own_namespace.yandex_cloud_elk`.

##### 9. В данную collection перенесите свой module в соответствующую директорию.

##### 10. Single task playbook преобразуйте в single task role и перенесите в collection. У role должны быть default всех параметров module.

##### 11. Создайте playbook для использования этой role.

<details><summary></summary>

```
---
- name: my_module
  hosts: localhost
  roles:
    - module_role
```

</details>

##### 12. Заполните всю документацию по collection, выложите в свой репозиторий, поставьте тег `1.0.0` на этот коммит.

[my_own_collection v.1.0.0](https://github.com/PanMonsters/my_own_collection/tree/cf714d8c4ef14c30a88ccd5d695cc9b65c6579aa) 

##### 13. Создайте .tar.gz этой collection: `ansible-galaxy collection build` в корневой директории collection.

<details><summary></summary>

```
panmonster@panmonster-PC:~/123/my_own_collection$ ansible-galaxy collection build
Created collection for my_own_namespace.my_collection at /home/panmonster/123/my_own_collection/my_own_namespace-my_collection-1.0.0.tar.gz
```

</details>

##### 14. Создайте ещё одну директорию любого наименования, перенесите туда single task playbook и архив c collection.

##### 15. Установите collection из локального архива: `ansible-galaxy collection install <archivename>.tar.gz`.

<details><summary></summary>

```
panmonster@panmonster-PC:~/123/my_own_collection$ ansible-galaxy collection install my_own_namespace-my_collection-1.0.0.tar.gz
Starting galaxy collection install process
Nothing to do. All requested collections are already installed. If you want to reinstall them, consider using `--force`.
```

</details>

##### 16. Запустите playbook, убедитесь, что он работает.

<details><summary></summary>

```
panmonster@panmonster-PC:~/123/my_own_collection/playbook$ ansible-playbook site.yml
[WARNING]: No inventory was parsed, only implicit localhost is available
[WARNING]: provided hosts list is empty, only localhost is available. Note that
the implicit localhost does not match 'all'

PLAY [test module] *************************************************************

TASK [Gathering Facts] *********************************************************
ok: [localhost]

TASK [test_my_own_module] ******************************************************
changed: [localhost]

TASK [info] ********************************************************************
ok: [localhost] => {
    "msg": "STATUS file recorder."
}

PLAY RECAP *********************************************************************
localhost                  : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

</details>

##### 17. В ответ необходимо прислать ссылку на репозиторий с collection

[my_own_collection](https://github.com/PanMonsters/my_own_collection) 

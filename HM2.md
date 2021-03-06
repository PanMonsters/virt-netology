
# Домашнее задание к занятию "5.2 Применение принципов IaaC в работе с виртуальными машинами"

---
## Задача 1

- Опишите своими словами основные преимущества применения на практике IaaC паттернов.
- Какой из принципов IaaC является основополагающим?

## Решение 1

	1) Опишите своими словами основные преимущества применения на практике IaaC паттернов.
	Преимущество IaaC состоит в Автоматизации, которая позволяет свести повторение одинаковых действий к минимуму, тем самым исключить возможные ошибки и дрейф в конфигурациях ВМ, что в свою очередь положительно сказывается на CI/CD.
	Есть возможность быстро восстановить рабочую среду так как хранятся все конфигурации ВМ
	Можно использовать систему контроля версий для отслеживания изменений конфигураций
	Удобно масштабировать
	
	2) Какой из принципов IaaC является основополагающим?
	Идемпоте́нтность это свойство объекта или операции, при повторном выполнении которой мы получаем результат идентичный предыдущему и всем последующим выполнения

  
---
## Задача 2

- Чем Ansible выгодно отличается от других систем управление конфигурациями?
- Какой, на ваш взгляд, метод работы систем конфигурации более надёжный push или pull?

## Решение 2

	1) Чем Ansible выгодно отличается от других систем управление конфигурациями?
	Отличается простотой использования, имеет безагентную архитектуру (не требует установки агента/клиента на целевую систему) и YAML-подобный DSL, написана на Python и легко расширяется за счет модулей, а так же удобен в использовании на текущей SSH инфраструктуре.
	
	2) Какой, на ваш взгляд, метод работы систем конфигурации более надёжный push или pull?
	Push надёжней, т.к. централизованно управляет конфигурацией и исключает ситуации, когда на сервере были внесены правки вручную, которые небыли отражены в Ansible.

---
## Задача 3

Установить на личный компьютер:

- VirtualBox
- Vagrant
- Ansible

*Приложить вывод команд установленных версий каждой из программ, оформленный в markdown.*

## Решение 3

- Графический интерфейс VirtualBox
- Версия 6.1.28 r147628 (Qt5.6.2).

------------------
- PS C:\Users\PanMonster> vagrant --version
- Vagrant 2.2.19

-----------------------
- $ ansible –version
- ansible 2.8.4
- config file = /etc/ansible/ansible.cfg
- configured module search path = ['/home/PanMonster/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
- ansible python module location = /usr/lib/python3.7/site-packages/ansible
- executable location = /usr/bin/ansible
- python version = 3.7.12 (default, Nov 23 2021, 18:58:07) [GCC 11.2.0]

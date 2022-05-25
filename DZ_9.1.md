# Домашнее задание к занятию "09.01 Жизненный цикл ПО"

---
## Подготовка к выполнению
1. Получить бесплатную [JIRA](https://www.atlassian.com/ru/software/jira/free)
2. Настроить её для своей "команды разработки"
3. Создать доски kanban и scrum

## Основная часть
В рамках основной части необходимо создать собственные workflow для двух типов задач: bug и остальные типы задач. Задачи типа bug должны проходить следующий жизненный цикл:
1. Open -> On reproduce
2. On reproduce -> Open, Done reproduce
3. Done reproduce -> On fix
4. On fix -> On reproduce, Done fix
5. Done fix -> On test
6. On test -> On fix, Done
7. Done -> Closed, Open

![image](https://github.com/PanMonsters/virt-netology/blob/4e2f24dca53db47c309fe9fb4439f26cb9da45a4/image/bug_task.png)

Остальные задачи должны проходить по упрощённому workflow:
1. Open -> On develop
2. On develop -> Open, Done develop
3. Done develop -> On test
4. On test -> On develop, Done
5. Done -> Closed, Open

![image](https://github.com/PanMonsters/virt-netology/blob/4e2f24dca53db47c309fe9fb4439f26cb9da45a4/image/other_task.png)

Создать задачу с типом bug, попытаться провести его по всему workflow до Done. Создать задачу с типом epic, к ней привязать несколько задач с типом task, провести их по всему workflow до Done. При проведении обеих задач по статусам использовать kanban. Вернуть задачи в статус Open.
Перейти в scrum, запланировать новый спринт, состоящий из задач эпика и одного бага, стартовать спринт, провести задачи до состояния Closed. Закрыть спринт.

![image](https://github.com/PanMonsters/virt-netology/blob/02777a88f20ffb59e5756d5f41b2c56f2b162db7/image/workflow.png)
![image](https://github.com/PanMonsters/virt-netology/blob/02777a88f20ffb59e5756d5f41b2c56f2b162db7/image/desk.png)

Если всё отработало в рамках ожидания - выгрузить схемы workflow для импорта в XML. Файлы с workflow приложить к решению задания.

[Bug workflow XML](https://github.com/PanMonsters/virt-netology/blob/02777a88f20ffb59e5756d5f41b2c56f2b162db7/image/PanMonster_workflow_to_bug.xml)  
[All workflow XML](https://github.com/PanMonsters/virt-netology/blob/02777a88f20ffb59e5756d5f41b2c56f2b162db7/image/PanMonster_to%20_all.xml) 
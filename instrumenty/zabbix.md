# Zabbix

### 1. Добавить хост

Configuration——Hosts

![6120144-1420fabef3e39688.png](https://russianblogs.com/images/187/b2399bb301a77af83c427457e198cf93.png)Добавить хост![6120144-c05730e218a6436d.png](https://russianblogs.com/images/648/6e47f60e8f5fe42d263bcf2bae013a60.png)Успешно добавлено

### 2. Добавьте элементы мониторинга

Configuration——Hosts——items——create items

![6120144-ef41f5ca590128dd.png](https://russianblogs.com/images/407/a885f2f70e437f709a19ea2406d84af7.png)Добавьте предмет![6120144-0d2cb216fb68056c.png](https://russianblogs.com/images/15/3400d2a3d38f20fd93d2e523027fd297.png)Установить элементы мониторинга

### 3. Просмотр мониторинга

Вернуться на панель мониторинга Мониторинг-Панель управления\
Вы можете видеть, что есть хост, и элемент включен

\
![6120144-0872ad1bfabb3ae9.png](https://russianblogs.com/images/906/5f25b59236d6c0194d7f6076b9052912.png)Мониторинг состояния

Просмотр последних данных Мониторинг —— Последние данные —— График

![6120144-c3cdf1fbdcb13a2d.png](https://russianblogs.com/images/990/c66884eab7f98b866ffe313ddd35333e.png)фильтр![6120144-e5d0938ce0faea1f.png](https://russianblogs.com/images/30/47e5f02056d5dbc38b56a86bbaf27e06.png)image.png

### 4. Добавить триггер

Сначала добавьте элемент мониторинга для мониторинга входящих пакетов

![6120144-6a766f251510247c.png](https://russianblogs.com/images/900/1ee708b3c232b889f5c582f86dd97694.png)Мониторинг входящих пакетов\


Метод обработки данных: рассчитать изменение в секунду

\
![6120144-c13b43a961bcad08.png](https://russianblogs.com/images/558/66deb999577712f2bf736cbf3f8fedde.png)Метод обработки данных

Добавить триггер

\
![6120144-60609b03a2970021.png](https://russianblogs.com/images/335/ff43c64231d236ca1668dd1a23bad5a7.png)image.png

Определите выражение «Выражение» для элементов и элементов триггера и предупредите, когда в секунду вводится 20 пакетов.

\
![6120144-c1b780e04f7b9616.png](https://russianblogs.com/images/988/264d729a59eaeefd62debcb772ff4944.png)image.png

панель приборов

![6120144-68fa871c838c52ad.png](https://russianblogs.com/images/851/0746004dd6eaadb36a4b20171bb1cd93.png)image.png

### 5. Добавить действие

Configuration——Actions——create action\
Добавить действие

\
![6120144-91e606a9ebfae88d.png](https://russianblogs.com/images/885/c035a0c48eb572f8117ac7113e406895.png)image.png

Определить условия

\
![6120144-307b7dc864adc4ec.png](https://russianblogs.com/images/314/c4d94bd0100114938bee54318be1f3ca.png)image.png\


Определить поведение

![6120144-531d5e71af0e797c.png](https://russianblogs.com/images/991/c1fa5fc8768f58845115ec068d00a737.png)image.png

***

\

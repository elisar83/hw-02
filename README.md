# Задание 1
Установите Zabbix Server с веб-интерфейсом.

Процесс выполнения
Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
Установите PostgreSQL. Для установки достаточна та версия что есть в системном репозитороии Debian 11
Пользуясь конфигуратором комманд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache
Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server
Требования к результаты
Прикрепите в файл README.md скриншот авторизации в админке
Приложите в файл README.md текст использованных команд в GitHub

# Ответ:

![image](https://github.com/elisar83/hw-02/assets/122297912/84da3e02-c1c5-4f52-b4d4-021eaf9026f6)
![image](https://github.com/elisar83/hw-02/assets/122297912/bff782a6-95cf-4832-8cc3-30d7e34ecd81)


sudo apt install postgresql

wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb

dpkg -i zabbix-release_6.0-4+debian11_all.deb

apt update

apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts

sudo -u postgres createuser --pwprompt zabbix

sudo -u postgres createdb -O zabbix zabbix

zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix

DBPassword=123

systemctl restart zabbix-server zabbix-agent apache2

systemctl enable zabbix-server zabbix-agent apache2


# Задание 2
Установите Zabbix Agent на два хоста.

Процесс выполнения
Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
Установите Zabbix Agent на 2 виртмашины, одной из них может быть ваш Zabbix Server
Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов
Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera
Проверьте что в разделе Latest Data начали появляться данные с добавленных агентов
Требования к результаты
Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером
Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.
Приложите в файл README.md текст использованных команд в GitHub

# Ответ:

![image](https://github.com/elisar83/hw-02/assets/122297912/23362a24-5021-4a0d-a4a4-8136abde73fb)
![image](https://github.com/elisar83/hw-02/assets/122297912/fc0b8bc5-4768-44a2-b53e-1a7a6f0359cb)
![image](https://github.com/elisar83/hw-02/assets/122297912/9f01d3a8-c8ab-4337-951c-2a329a32cf6b)
![image](https://github.com/elisar83/hw-02/assets/122297912/7e07fad1-ae7b-480f-aff8-036c398decc6)

# Установить агент

wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb

dpkg -i zabbix-release_6.0-4+debian11_all.deb

apt update

apt install zabbix-agent

systemctl restart zabbix-agent

systemctl enable zabbix-agent

# Добавить в /etc/zabbix/zabbix-agentd.conf

Server=192.168.1.109

DebugLevel=5

ServerActive=192.168.1.109

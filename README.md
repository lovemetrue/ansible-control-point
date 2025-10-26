Проверочные ad-hoc команды:

bash
# 1. Проверка связи со всеми хостами
ansible all -i inventory.ini -m ping

# 2. Проверка статуса Nginx на веб-серверах
ansible webservers -i inventory.ini -m systemd -a "name=nginx state=started" -b

# 3. Проверка статуса PostgreSQL на серверах БД
ansible dbservers -i inventory.ini -m systemd -a "name=postgresql state=started" -b

# 4. Проверка доступности веб-страницы
ansible webservers -i inventory.ini -a "curl -s http://localhost" -b

# 5. Проверка существования базы данных
ansible dbservers -i inventory.ini -a "sudo -u postgres psql -c '\l'" -b
Демонстрация идемпотентности:

bash
# Первый запуск - должны быть изменения (желтый CHANGED)
ansible-playbook -i inventory.ini deploy_infrastructure.yml

# Второй запуск - все задачи должны быть зеленые (OK)
ansible-playbook -i inventory.ini deploy_infrastructure.yml
Инструменты отладки:

bash
# Предварительный просмотр изменений
ansible-playbook -i inventory.ini deploy_infrastructure.yml --check

# Запуск только задач установки
ansible-playbook -i inventory.ini deploy_infrastructure.yml --tags "install"

# Детальный вывод
ansible-playbook -i inventory.ini deploy_infrastructure.yml -v



# Проверка веб-сервера
curl http://192.168.1.10

# Проверка базы данных
ansible dbservers -i inventory.ini -a "sudo -u postgres psql -c '\l'" -b
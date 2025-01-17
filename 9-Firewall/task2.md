# Открываем firewald

1. Удалите iptables и установите firewalld
2. Попробуйте так-же проверить возможность подключения по ssh
3. Если её нет то откройте порт
4. Выведите список открытых портов с помощью firewall-cmd
5. Можно ли там добавить порты по названию сервиса?
6. На вашей Локальной виртуальной машине попробуйте подключиться к серверу samba из предыдущих заданий
7. Если не получилось то откройте нужные порты
9. Сделайте так чтобы изменения были постоянными

# Решение:
1. Удаляем iptables:
   ```
   sudo apt remove --purge iptables-persistent
   ```
   Устанавливаем firewalld:
   ```
   sudo apt install firewalld
   sudo systemctl enable --now firewalld
   ```
2. Тестим:
   ```
   ssh ashenone@ip
   ```
3. Открываем порт:
   ```
   sudo firewall-cmd --zone=public --add-port=22/tcp --permanent
   sudo firewall-cmd --reload
   ```
4. ```
   sudo firewall-cmd --list-ports
   ```
5. Да. Например:
   ```
   sudo firewall-cmd --zone=public --add-service=ssh --permanent
   sudo firewall-cmd --reload
   ```
6. ```
   smbclient -L //ip
   ```
7.
   ```
   sudo firewall-cmd --zone=public --add-service=samba --permanent
   sudo firewall-cmd --reload
   ```
   Samba использует следующие порты:  
    TCP: 139, 445  
    UDP: 137, 138  
  Открываем их если всё ещё не работает:  
   ```
   sudo firewall-cmd --zone=public --add-port=139/tcp --permanent
   sudo firewall-cmd --zone=public --add-port=445/tcp --permanent
   sudo firewall-cmd --zone=public --add-port=137/udp --permanent
   sudo firewall-cmd --zone=public --add-port=138/udp --permanent
   sudo firewall-cmd --reload
   ```
8. Изменения должны были сохраниться благодаря флагу ```--permanent```, проверка:
   ```
   sudo firewall-cmd --list-all
   ```

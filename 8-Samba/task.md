
# Шарим


1. Установите пакет samba
2. ЧТо такое побщая папка, зачем оно может быть нужно?
3. Создайте общую папку без пароля с правами только на чтение файлов
4. Создайте общую папку с паролем с правами на чтение и запись
5. Создайте общую папку с доступом для какой-то группы с полными правами
6. Создайте общую папку в которой у одной группы будет полный доступ, а у другой только доступ на чтение.
Третья группа не должна иметь к ней доступа


#Решение:
1. ```sudo apt install samba```
   (В моём случае было бы ```sudo yum install samba```)
2. Общая папка — это директория, доступная для других пользователей в сети.
3. Создаём директорию:
   ```
   sudo mkdir -p /srv/samba/public
   sudo chmod 755 /srv/samba/public
   ```
   Настраиваем конфиг samba:
   ```
   sudo nano /etc/samba/smb.conf
   ```
   Добавляем в конфиг:
   ```
   [Public]
   path = /srv/samba/public
   browseable = yes
   read only = yes
   guest ok = yes
   ```
   Перезапускаем samba:
   ```
   sudo systemctl restart smbd
   ```
4. Создаём директорию, снова:
   ```
   sudo mkdir -p /srv/samba/secure
   sudo chmod 770 /srv/samba/secure
   ```
   Добавляем пользователя:
   ```
   sudo smbpasswd -a ashenone
   ```
   После чего терминал должен запросить установить пароль.
   Вносим изменения в конфиг и совершаем перезапуск:
   ```
   [Secure]
   path = /srv/samba/secure
   browseable = yes
   read only = no
   valid users = ashenone
   ```
   ```
   sudo systemctl restart smbd
   ```
5. Создаём группу и пользователей:
   ```
   sudo groupadd sambagroup
   sudo usermod -aG sambagroup ashenone
   ```
   Директория:
   ```
   sudo mkdir -p /srv/samba/mixed
   sudo chown :fullaccess /srv/samba/mixed
   sudo chmod 770 /srv/samba/mixed
   ```
   В конфиг:
   ```
   [GroupShare]
   path = /srv/samba/group
   browseable = yes
   read only = no
   valid users = @sambagroup
   ```
   Ребут:
   ```
   sudo systemctl restart smbd
   ```
6. Группа:
   ```
   sudo groupadd fullaccess
   sudo groupadd readaccess
   sudo usermod -aG fullaccess ashenone
   sudo usermod -aG readaccess user1
   ```
   Директория:
   ```
   sudo mkdir -p /srv/samba/mixed
   sudo chown :fullaccess /srv/samba/mixed
   sudo chmod 770 /srv/samba/mixed
   ```
   Настройка ACL (Access Control List):
   ```
   sudo setfacl -m g:fullaccess:rwx /srv/samba/mixed
   sudo setfacl -m g:readaccess:rx /srv/samba/mixed
   ```
   В конфиг:
   ```
   [MixedAccess]
   path = /srv/samba/mixed
   browseable = yes
   read only = no
   valid users = @fullaccess, @readaccess
   ```
   Ребут:
   ```
   sudo systemctl restart smbd
   ```

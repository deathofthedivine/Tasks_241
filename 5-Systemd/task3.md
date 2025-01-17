# Журнальчики

1. Посмотретите журналы ssh
2. Выведите журналы в реальном времени
3. Выведите лог в реальном времени для службы sshd
4. Можно ли без комады journalctl прочитать логи systemd?
5. Сколько будет 2-2?

# Решение:
1. ```
   sudo journalctl -u ssh
   ```
2. ```
   sudo journalctl -fu ssh
   ```
3. ```
   sudo journalctl -fu sshd
   ```
4. Да, в директории ```/var/log/syslog```.
5. я считать не умею
   ![photo_2025-01-17_14-40-00](https://github.com/user-attachments/assets/b1db86e3-b1a8-42d2-b837-29261e4f58d6)

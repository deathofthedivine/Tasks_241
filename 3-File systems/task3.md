# Продолжаем

1. Выведите содержимое fstab. Что хранится в fstab?
2. Добавьте в виртуальную машину ещё один диск
3. Узнайте как ситема видит ваш диск - выведите информацию о блочных устройствах
4. С помощью полученной информации создайте на диске таблицу разделов и фаловую систему ext4
5. Примонитруте диск в каталог /mnt
6. Зайдите в каталог и создайте там файлы
7. Отмонтируйте диск и проверье остались ли файлы
8. Сделайте так чтобы диск автоматически подключался при загрузке систем ( добавьте информацию о нём с fstab)
9. Проверьте корретность записанных в fstab данных перед перезагрузкой
10. Перезагрущите систему и убедитесь что диск был подключён к системе

# Решение:
1. ![image](https://github.com/user-attachments/assets/c4fd7695-d46a-41b1-81f3-9011b4065bd1)  
### Что хранится в fstab?  
- UUID или имя устройства.  
- Точка монтирования.  
- Тип файловой системы.  
- Опции монтирования.  
- Поля для проверки файловой системы.  
3. ![image](https://github.com/user-attachments/assets/c7177b7d-95b0-4815-9fe5-4aba0ffff6ae)  
4. ![image](https://github.com/user-attachments/assets/6e4fdf0f-2814-4f64-93fd-bcb401903045)    
5. ![image](https://github.com/user-attachments/assets/33a8426f-20e9-4249-8c9d-ab152d8edd93)  
6. ![image](https://github.com/user-attachments/assets/93095086-a9d0-4969-b591-071d52e42239)  
7. ![image](https://github.com/user-attachments/assets/887632bb-bd55-488e-8dbd-5c118d58ce51)  
8. Узнаём UUID раздела:  
  ![image](https://github.com/user-attachments/assets/874e85a2-3f77-451d-8a52-36ff21df82e8)  
  Входим в fstab:  
  ![image](https://github.com/user-attachments/assets/60790468-7798-4202-a045-a1430f6a9dbf)  
  ![image](https://github.com/user-attachments/assets/b66a362e-3041-49f6-8f31-9e7eccd0701c)  
  Добавляем запись о новом разделе:  
  ![image](https://github.com/user-attachments/assets/3360f5b8-2214-4d1d-bfbe-9ffd1715a19a)
9. ![image](https://github.com/user-attachments/assets/41f1aec5-79b1-4621-a0af-4d651146ae66)
10. После перезагрузки:  
  ![image](https://github.com/user-attachments/assets/9c440361-2a34-4cf4-bcc0-554e1104304d)



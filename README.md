# ZFS
Описание домашнего задания:

1. Определить алгоритм с наилучшим сжатием:

   
     - определить, какие алгоритмы сжатия поддерживает zfs (gzip, zle, lzjb, lz4);
     - создать 4 файловых системы, на каждой применить свой алгоритм сжатия;
     -  для сжатия использовать либо текстовый файл, либо группу файлов.


2. Определить настройки пула.


   2.1. С помощью команды zfs import собрать pool ZFS.


   2.2. Командами zfs определить настройки:
  
  
     - размер хранилища;
     - тип pool;
     - значение recordsize;
     - какое сжатие используется;
     - какая контрольная сумма используется.

3. Работа со снапшотами:
  
  
     - скопировать файл из удаленной директории;
     - восстановить файл локально. zfs receive;
     - найти зашифрованное сообщение в файле secret_message.

# 1. Определить алгоритм с наилучшим сжатием:
 
 1. Создадим pool:  

<img width="941" height="148" alt="zfs11" src="https://github.com/user-attachments/assets/bbc86db7-9ccf-4604-b312-b45ed36b8260" />

       **zpool create -f otus_pool mirror sdb sdc**


2. Создадим файловые системы в pool:
   
   <img width="606" height="335" alt="zfs12" src="https://github.com/user-attachments/assets/21948f53-0949-4421-80a4-d2036dcc4257" />

         **zfs create otus_pool/fs1**
         **zfs create otus_pool/fs2**
         **zfs create otus_pool/fs3**
         **zfs create otus_pool/fs4**

3. Зададим компрессию и алгоритм сжатия для 4 файловых систем:

<img width="602" height="252" alt="zfs14_1" src="https://github.com/user-attachments/assets/d3b8ed1b-2316-4b9e-ac32-851b8d18c5cf" />


      zfs set compression=lzjb otus_pool/fs1
      zfs set compression=lz4 otus_pool/fs2
      zfs set compression=gzip otus_pool/fs3
      zfs set compression=zle otus_pool/fs4

4. Скопируем файлы из /var/log/* в наши файловые системы:

   <img width="571" height="92" alt="zfs15" src="https://github.com/user-attachments/assets/b5a5f415-32ba-47f3-9f64-a0ec68ccde13" />

         cp -r /var/log/* /otus_pool/fs1
         cp -r /var/log/* /otus_pool/fs2
         cp -r /var/log/* /otus_pool/fs3
         cp -r /var/log/* /otus_pool/fs4

5. Определим алгоритм с наилучшим сжатием с помощью команд:
   

   <img width="645" height="451" alt="zfs16" src="https://github.com/user-attachments/assets/08f71b6b-dd38-4aa4-b394-d6e1988f6700" />

______________________________________________________________________________________
      zfs get compressratio

______________________________________________________________________________________
      zfs list

_____________________________________________________________________________________

      zfs get compression


Самым лучшим алгоритмом сжатия является gzip.


# 2 Определить настройки пула

# 2.1. С помощью команды zfs import собрать pool ZFS.

   2.1.1. Для сборки пула командой zfs import я удалю свой пул:

<img width="753" height="254" alt="zfs21" src="https://github.com/user-attachments/assets/9581ca56-b26b-4eb7-89f6-19577b4618f3" />


      zpool destroy otus_pool

   2.1.2. Собираю и переименовываю пул 

<img width="967" height="349" alt="zfs22" src="https://github.com/user-attachments/assets/090d59ed-5ef6-4e96-9eab-99c18012cc2b" />


      zpool import -D otus_pool otus_import

 # 2.2. Командами zfs определить настройки:
       
   <img width="592" height="332" alt="zfs23" src="https://github.com/user-attachments/assets/e3545416-bca7-49af-94e1-47b608b1d244" />

       
 2.2.1. Размер хранилища:  
 
       zfs get available otus_import

2.2.2. Тип pool:

      zfs get readonly otus_import

2.2.3. Значения recordsize:

      zfs get recordsize otus_import

2.2.4. Какое сжатие используется:

      zfs get compression otus_import

2.2.5. Какая контрольная сумма используется:

      zfs get checksum otus_import

# 3. Работа со снапшотами:

   3.1. Скопировать файл из удаленной директории:

   <img width="1656" height="128" alt="zfs31" src="https://github.com/user-attachments/assets/471b157e-89f2-48e0-872d-c2411505d302" />


         wget -O otus_task2.file --no-check-certificate https://drive.usercontent.google.com/download?id=1wgxjih8YZ-cqLqaZVa0lA3h3Y029c3oI&export=download


   3.2. Восстановить файл локально. zfs receive и найти зашифрованное сообщение в файле secret_message:


<img width="720" height="95" alt="zfs32" src="https://github.com/user-attachments/assets/aa3e8e96-7f38-4208-a0c6-646c02701a12" />


         find otus_import/test -name "secret_message"
_______________________________________________________________________________________________________________

         cat /otus_import/test/task1/file_mess/secret_message





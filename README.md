# ZFS
Описание домашнего задания:

Определить алгоритм с наилучшим сжатием:
определить, какие алгоритмы сжатия поддерживает zfs (gzip, zle, lzjb, lz4);
создать 4 файловых системы, на каждой применить свой алгоритм сжатия;
для сжатия использовать либо текстовый файл, либо группу файлов.
Определить настройки пула.
С помощью команды zfs import собрать pool ZFS.
Командами zfs определить настройки:
размер хранилища;
тип pool;
значение recordsize;
какое сжатие используется;
какая контрольная сумма используется.
Работа со снапшотами:
скопировать файл из удаленной директории;
восстановить файл локально. zfs receive;
найти зашифрованное сообщение в файле secret_message.

# 1 Создадим pool:  

<img width="941" height="148" alt="zfs11" src="https://github.com/user-attachments/assets/bbc86db7-9ccf-4604-b312-b45ed36b8260" />

    **zpool create -f otus_pool mirror sdb sdc**


# 2 Создадим файловые системы в pool:
   
   <img width="606" height="335" alt="zfs12" src="https://github.com/user-attachments/assets/21948f53-0949-4421-80a4-d2036dcc4257" />

      **zfs create otus_pool/fs1**
      **zfs create otus_pool/fs2**
      **zfs create otus_pool/fs3**
      **zfs create otus_pool/fs4**

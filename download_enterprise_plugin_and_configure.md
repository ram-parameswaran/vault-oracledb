```
root@ip-172-31-9-18:/etc/vault# mkdir oracle_client
root@ip-172-31-9-18:/etc/vault# cd oracle_client/
root@ip-172-31-9-18:/etc/vault/oracle_client# cd ..
root@ip-172-31-9-18:/etc/vault# curl -O https://download.oracle.com/otn_software/linux/instantclient/1923000/instantclient-basic-linux.x64-19.23.0.0.0dbru.zip
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 71.8M  100 71.8M    0     0  41.7M      0  0:00:01  0:00:01 --:--:-- 41.7M
root@ip-172-31-9-18:/etc/vault# ls -la
total 73632
drwxr-x---   5 root  vault     4096 May 20 14:29 .
drwxr-xr-x 100 root  root      4096 May  9 06:01 ..
-rw-r--r--   1 vault vault     1311 Apr 23 22:09 .license
-rw-r--r--   1 root  root       391 Apr 23 22:31 VaultCreds.txt
-rw-r--r--   1 root  root  75365808 May 20 14:29 instantclient-basic-linux.x64-19.23.0.0.0dbru.zip
drwxr-xr-x   2 root  root      4096 May 20 14:29 oracle_client
drwxr-x---   2 root  vault     4096 Apr 23 20:51 pki
drwxr-xr-x   4 vault vault     4096 May 20 14:26 plugins
-rw-r-----   1 root  vault      332 May  1 11:47 vault.hcl
root@ip-172-31-9-18:/etc/vault# rm -rf instantclient-basic-linux.x64-19.23.0.0.0dbru.zip
root@ip-172-31-9-18:/etc/vault# cd oracle_client/
root@ip-172-31-9-18:/etc/vault/oracle_client# curl -O https://download.oracle.com/otn_software/linux/instantclient/1923000/instantclient-basic-linux.x64-19.23.0.0.0dbru.zip
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 71.8M  100 71.8M    0     0   119M      0 --:--:-- --:--:-- --:--:--  119M
root@ip-172-31-9-18:/etc/vault/oracle_client# unzip instantclient-basic-linux.x64-19.23.0.0.0dbru.zip -d .
Archive:  instantclient-basic-linux.x64-19.23.0.0.0dbru.zip
  inflating: ./META-INF/MANIFEST.MF
  inflating: ./META-INF/ORACLE_C.SF
  inflating: ./META-INF/ORACLE_C.RSA
  inflating: ./instantclient_19_23/adrci
  inflating: ./instantclient_19_23/BASIC_LICENSE
  inflating: ./instantclient_19_23/BASIC_README
  inflating: ./instantclient_19_23/genezi
  inflating: ./instantclient_19_23/libclntshcore.so.19.1
    linking: ./instantclient_19_23/libclntsh.so  -> libclntsh.so.19.1
    linking: ./instantclient_19_23/libclntsh.so.10.1  -> libclntsh.so.19.1
    linking: ./instantclient_19_23/libclntsh.so.11.1  -> libclntsh.so.19.1
    linking: ./instantclient_19_23/libclntsh.so.12.1  -> libclntsh.so.19.1
    linking: ./instantclient_19_23/libclntsh.so.18.1  -> libclntsh.so.19.1
  inflating: ./instantclient_19_23/libclntsh.so.19.1
  inflating: ./instantclient_19_23/libipc1.so
  inflating: ./instantclient_19_23/libmql1.so
  inflating: ./instantclient_19_23/libnnz19.so
    linking: ./instantclient_19_23/libocci.so  -> libocci.so.19.1
    linking: ./instantclient_19_23/libocci.so.10.1  -> libocci.so.19.1
    linking: ./instantclient_19_23/libocci.so.11.1  -> libocci.so.19.1
    linking: ./instantclient_19_23/libocci.so.12.1  -> libocci.so.19.1
    linking: ./instantclient_19_23/libocci.so.18.1  -> libocci.so.19.1
  inflating: ./instantclient_19_23/libocci.so.19.1
  inflating: ./instantclient_19_23/libociei.so
  inflating: ./instantclient_19_23/libocijdbc19.so
  inflating: ./instantclient_19_23/liboramysql19.so
  inflating: ./instantclient_19_23/libtfojdbc1.so
   creating: ./instantclient_19_23/network/
  inflating: ./instantclient_19_23/ojdbc8.jar
  inflating: ./instantclient_19_23/ucp.jar
  inflating: ./instantclient_19_23/uidrvci
  inflating: ./instantclient_19_23/xstreams.jar
   creating: ./instantclient_19_23/network/admin/
  inflating: ./instantclient_19_23/network/admin/README
finishing deferred symbolic links:
  ./instantclient_19_23/libclntsh.so -> libclntsh.so.19.1
  ./instantclient_19_23/libclntsh.so.10.1 -> libclntsh.so.19.1
  ./instantclient_19_23/libclntsh.so.11.1 -> libclntsh.so.19.1
  ./instantclient_19_23/libclntsh.so.12.1 -> libclntsh.so.19.1
  ./instantclient_19_23/libclntsh.so.18.1 -> libclntsh.so.19.1
  ./instantclient_19_23/libocci.so -> libocci.so.19.1
  ./instantclient_19_23/libocci.so.10.1 -> libocci.so.19.1
  ./instantclient_19_23/libocci.so.11.1 -> libocci.so.19.1
  ./instantclient_19_23/libocci.so.12.1 -> libocci.so.19.1
  ./instantclient_19_23/libocci.so.18.1 -> libocci.so.19.1
root@ip-172-31-9-18:/etc/vault/oracle_client# ls -la
total 73616
drwxr-xr-x 4 root root      4096 May 20 14:31 .
drwxr-x--- 5 root vault     4096 May 20 14:30 ..
drwxr-xr-x 2 root root      4096 May 20 14:31 META-INF
-rw-r--r-- 1 root root  75365808 May 20 14:30 instantclient-basic-linux.x64-19.23.0.0.0dbru.zip
drwxr-xr-x 3 root root      4096 May 20 14:31 instantclient_19_23
root@ip-172-31-9-18:/etc/vault/oracle_client# rm -rf instantclient-basic-linux.x64-19.23.0.0.0dbru.zip
root@ip-172-31-9-18:/etc/vault/oracle_client# ls -la
total 16
drwxr-xr-x 4 root root  4096 May 20 14:31 .
drwxr-x--- 5 root vault 4096 May 20 14:30 ..
drwxr-xr-x 2 root root  4096 May 20 14:31 META-INF
drwxr-xr-x 3 root root  4096 May 20 14:31 instantclient_19_23
root@ip-172-31-9-18:/etc/vault/oracle_client# cd ..
root@ip-172-31-9-18:/etc/vault# export LD_LIBRARY_PATH=/etc/vault/oracle_client/instantclient_19_23
root@ip-172-31-9-18:/etc/vault# exit
logout
ubuntu@ip-172-31-9-18:~$ sudo /etc/vault/plugins/.runtime/vault-plugin-database-oracle_0.14.1+ent_linux_amd64/vault-plugin-database-oracle
/etc/vault/plugins/.runtime/vault-plugin-database-oracle_0.14.1+ent_linux_amd64/vault-plugin-database-oracle: error while loading shared libraries: libclntsh.so.19.1: cannot open shared object file: No such file or directory
ubuntu@ip-172-31-9-18:~$ sudo su -
root@ip-172-31-9-18:~# /etc/vault/plugins/.runtime/vault-plugin-database-oracle_0.14.1+ent_linux_amd64/vault-plugin-database-oracle
/etc/vault/plugins/.runtime/vault-plugin-database-oracle_0.14.1+ent_linux_amd64/vault-plugin-database-oracle: error while loading shared libraries: libclntsh.so.19.1: cannot open shared object file: No such file or directory
root@ip-172-31-9-18:~# export LD_LIBRARY_PATH=/etc/vault/oracle_client/instantclient_19_23
root@ip-172-31-9-18:~# echo $LD_LIBRARY_PATH
/etc/vault/oracle_client/instantclient_19_23
root@ip-172-31-9-18:~# /etc/vault/plugins/.runtime/vault-plugin-database-oracle_0.14.1+ent_linux_amd64/vault-plugin-database-oracle
This binary is a plugin. These are not meant to be executed directly.
Please execute the program that consumes these plugins, which will
load any plugins automatically
```
root@ip-172-31-9-18:~#

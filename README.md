# PartDB

Part-DB docker container

## Restore

Restore a backup onto a MySQL Server (mariadb) plus restore all the necessary files. At this point a MySQL user should already created.

1. Upload the SQL backup to you server. You can do that via PSFTP on windows or with scp on Linux
1. Unzip the backup file if it's zipped 

    ```bash
    gzip -d DB3625135_2025-11-06.sql.gz
    ```
1. Import the dump into the MySQL container directly. You need do that wih an uses that can access the target database from the local server.

    ```bash
    sudo docker exec -i  mariadb /bin/mysql -u root -pChangeMeOnlyDevelopement partdb < ~/DB3625135_2025-11-06.sql
    ```

1. Remove the SQL files.

    ```bash
    rm ~/DB3625135_2025-11-06.sql
    ```

1. 
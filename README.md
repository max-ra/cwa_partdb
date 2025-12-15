# PartDB

Part-DB docker container

## Create DB

1. Login to the mariadb server and create user with database.

    ```sql
    CREATE USER 'partdb'@'partdb.backbone_database' IDENTIFIED BY 'LongComplicatedPassword';
    GRANT ALL PRIVILEGES on partdb.* to 'partdb'@'partdb.backbone_database';
    CREATE DATABASE partdb;
    QUIT
    ```

## Restore DB

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

## Backup DB

Run the following command to do a full database backup

```bash
sudo docker exec -i  mariadb /bin/mariadb-dump -u root -pChangeMeOnlyDevelopement partdb > ~/Update_05.sql
```
#How to test migration tool
###MySql

in [db.changelog-persistence.xml](src/main/resources/db/changelog/db.changelog-persistence.xml)
steps:
1. remove two last include lines.
    ```shell
    <include file="db.changelog-initial_2022_07_3.xml" context="upgrade_2022_2_to_2022_07_3" relativeToChangelogFile="true"/>
    <include file="db.changelog-initial_2022_07_4.xml" context="upgrade_2022_3_to_2022_07_4" relativeToChangelogFile="true"/>
    ```

2. execute to create a partial DB schema
    ```shell
    mvn spring-boot:run -Dspring-boot.run.profiles=mysql
    ```

3. In db remode tables: `DATABASECHANGELOG`,`DATABASECHANGELOGLOCK`.

    This will emulate DB without liquibase.  
    So we have a DB schema and we can mark it as executed with liquibase. 

4. To init/mark already executed changes
    ```shell
    liquibase --url=jdbc:mysql://localhost:3306/demo --username=demo --password=d2m3 --changeLogFile=./src/main/resources/db/changelog/db.changelog-persistence.xml --logLevel=INFO changeLogSync
    ```
5. add two last include lines.
    ```shell
    <include file="db.changelog-initial_2022_07_3.xml" context="upgrade_2022_2_to_2022_07_3" relativeToChangelogFile="true"/>
    <include file="db.changelog-initial_2022_07_4.xml" context="upgrade_2022_3_to_2022_07_4" relativeToChangelogFile="true"/>
    ```

6.  execute to update exist DB with new changes
    ```shell
    mvn spring-boot:run -Dspring-boot.run.profiles=mysql
    ```





#Presenting
* [github liquibase](https://github.com/liquibase/liquibase)
* [liquibase](https://www.liquibase.org/)
* [Documentation liquibase](https://docs.liquibase.com/home.html)

## Features
- General behave
  - Flexible database change
  - Version control for your database
  - Built for developers
- Features you know you need
  - Flexible schema change
  - Auto-generate scripts
  - Repeatable migrations
  - Integrations and extensions
  - Rollbacks
  - Context-dependent logic
  
# Demo 
 * Migration onto exist DB. [Test Steps](Migrate_onto_exist_db.md)
    
## Run

```shell
mvn clean spring-boot:run`
```
```shell
mvn spring-boot:run -Dspring-boot.run.profiles=mysql
```
```shell
mvn spring-boot:run -Dspring-boot.run.profiles=mssql
```

Setup DB changelog (https://docs.liquibase.com/commands/maintenance/changelog-sync.html)
```shell
liquibase --url=jdbc:mysql://localhost:3306 --username=demo --password=d2m3 --changeLogFile=./src/main/resources/db/changelog/db.changelog-persistence.xml --logLevel=INFO changeLogSyncSQL
```
correct one with DB
```shell
liquibase --url=jdbc:mysql://localhost:3306/demo --username=demo --password=d2m3 --changeLogFile=./src/main/resources/db/changelog/db.changelog-persistence.xml --logLevel=INFO changeLogSyncSQL
```
Keep in mind. If you run migrations from spring boot and from external location the file name(`FILENAME`) path will be different. The `FILENAME` should be the same. 
use in changelog file `logicalFilePath="db/changelog/db.changelog-initial_2022.xml"`

Generate changelog
```shell
liquibase --url=jdbc:mysql://localhost:3306/demo --username=demo --password=d2m3 --changeLogFile=db.changelog-persistence.xml --logLevel=INFO --output-file=sync-sql.sql generateChangeLog
```

Generate update scripts
```shell
 liquibase --url=jdbc:mysql://localhost:3306/demo --username=demo --password=d2m3 --changeLogFile=./src/main/resources/db/changelog/db.changelog-persistence.xml update-sql
```
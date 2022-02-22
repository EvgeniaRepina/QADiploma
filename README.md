##  Процедура запуска автотестов
### Подготовка:
1. Установить:
* [Docker Desktop](https://www.docker.com/products/docker-desktop)
* [IntelliJ IDEA](https://www.jetbrains.com/idea)
2. Скачать [проект](https://github.com/EvgeniaRepina/QADiploma.git), открыть его в IDEA
3. Запустить Docker
4. Скачать 3 контейнера в терминале:
* docker image pull mysql:latest
* docker image pull postgres:13.2
* docker image pull node:8

### Запуск автотестов:

1. Запустить контейнеры СУБД MySQl, PostgerSQL и Node.js в терминале:
```
docker-compose up -d
```
#### MySQl
2. Запустить SUT, работающей на СУБД MySQl:
```
java -D:spring.datasource.url=jdbc:mysql://localhost:3306/app -jar artifacts/aqa-shop.jar
```
3. В новом терминале запустить автотесты для MySQL: 
```
./gradlew clean test -Durl=jdbc:mysql://localhost:3306/app
```
4. Сгенерировать отчет:
```
   ./gradlew allureReport
   ./gradlew allureServe
   ```
5. Закрыть терминал с SUT.

#### PostgreSQL
6. Запустить SUT, работающей на СУБД PostgreSQL:
```
java -D:spring.datasource.url=jdbc:postgresql://localhost:5432/app -jar artifacts/aqa-shop.jar
   ```
7. В новом терминале запустить автотесты для PostgreSQL:
```
./gradlew clean test -Durl=jdbc:postgresql://localhost:5432/app
   ```
8. Сгенерировать отчет:
``` 
./gradlew allureReport
./gradlew allureServe
```
9. Закрыть все терминалы.
10. Остановить и удалить все контейнеры.

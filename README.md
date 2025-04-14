# Многомодульный проект на Maven

## Описание
Для закрепления лекционного материала попрактикуемся в том, как создавать проекты.

Стандартный многомодульный проект имеет составляющие по функционалу:

db - модуль работы с базой данных;

api - модуль работы с web;

service - слой сервисов.

## Реализация
Для начала создайте одномодульный проект - как это было показано на занятии.

После необходимо установить packaging в pom

```java
<packaging>pom</packaging>
```

После создаем 3 модуля в корне проекта: db, api, service.

В каждом модуле будет создан *pom.xml* c содержимым:

```java
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>App</artifactId>
        <groupId>ru.netology</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>
    <artifactId>db</artifactId>
    <packaging>jar</packaging>
</project>
```
В каждом pom.xml обязательно указываем parent - в качестве родительского модуля с его данными и название *artifactId* текущего модуля (db, api, service)

Чтобы подключить новые модули к проекту, добавляем в корне проекта в файл *pom.xml* новые созданные модули:
```java

  <modules>
    <module>db</module>
    <module>api</module>
    <module>service</module>
  </modules> 
```
Подключим связанные модули между собой.

Для подключения модуля db в модуль service добавим зависимость:

    <dependencies>
        <dependency>
            <groupId>ru.netology</groupId>
            <artifactId>db</artifactId>
            <version>1.0-SNAPSHOT</version>
            <scope>compile</scope>
        </dependency>
    </dependencies>
Для подключения модуля service в модуль api добавим зависимость:

    <dependencies>
        <dependency>
            <groupId>ru.netology</groupId>
            <artifactId>service</artifactId>
            <version>1.0-SNAPSHOT</version>
            <scope>compile</scope>
        </dependency>
    </dependencies> 
Теперь можно собрать проект, выполнив команду:

mvn clean install
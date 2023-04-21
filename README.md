# maven-example

Пример сборки Maven Project

## Содержание:

1. [Установка Java/Maven](#установка-java--maven);
2. [Создаем Maven Project](#создаем-maven-project);
3. [Потрошим сроедстваим Java](#потрошим-средствами-java)
4. [Lyfecycle Maven](#lifecycle-maven)

## [Установка Java / Maven](#содержание)

В данном примере используется Java 11 - amazon version, и Maven:latest

Ссылки для быстрой загрузки используемых ресурсов

| Софт    |                                     Ссылка                                     | Версия |
| ------- | :----------------------------------------------------------------------------: | :----: |
| Java 11 | https://docs.aws.amazon.com/corretto/latest/corretto-11-ug/downloads-list.html | amazon |
| Maven   |                     https://maven.apache.org/download.cgi                      | latest |

Далее добавляем установленные ссылки на распакованные архивы в System или User PATH переменную

Для проверки работоспособности, используем команды:

```ps
java --version
mvn --version
```

> В случае успеха, увидите сообщения об установленных версиях

## [Создаем Maven Project](#содержание)

Для того чтобы создать проект автоматически, можем воспользоваться командой из Maven-Документации:

```ps
mvn archetype:generate -DgroupId=ru.cmx.maven.example -DartifactId=maven-example -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4 -DinteractiveMode=false
```

Далее, для удобства запускаем терминал и перемещаемся в директорию проекта. Пример:

```bat
cd maven-example
```

И если все прошло успешно при генерации, то у вас в проекте появится следующая структура:

```
- pom.xml
- src:
  - main.java.ru.cmx.mave.example:
    - App.java
  - test.java.ru.cmx.mave.example:
    - AppTest.java
```

Проверяется командой:

```cmd
tree /f
```

## [Потрошим средствами Java](#содержание)

Итак, попробуем запустить дефолтный проект Java, собранный после команды `mvn archetype:generate`

Для того, чтобы запустить приложение Java, необходимо сначала его скомпилириовать в байт-код

Чтобы скомпилировать файл, используем следующую команду:

```bat
javac src/main/java/ru/cmx/maven/example/App.java
```

Далее проверяем, что скомпилированный файл, появился:

```cmd
tree /f
```

И видим структуру

```
- pom.xml
- src:
  - main.java.ru.cmx.mave.example:
    - App.class
    - App.java
  - test.java.ru.cmx.mave.example:
    - AppTest.java
```

И запускаем то, что собрали:

```bat
java -cp {path_to_project}\src\main\java ru.cmx.maven.example.App
```

## [Lifecycle Maven](#содержание)

Для очистки всего свяазанного с старым билдом используем clean:

```ps
mvn clean
```

Для компилирования кода используем compile:

```ps
mvn compile
```

Для запуска тестов используем test:

```ps
mvn test
```

Для сборки в jar приложение со всеми предыдущими фазами используем package:

```ps
mvn package
```

Для того, чтобы использовать ваш проект, в другом вашем локальном проекте (например библиотеку) используем install:

```ps
mvn install
```

После этого, в вашей локальной папке для зависимостей (.m2) появится ваш проект, в собранном виде, который можно использовать в других проектах

> добавить в зависимости и готово!

>     	<dependency>
>     		<groupId>ru.cmx.maven.example</groupId>
>     		<artifactId>maven-example</artifactId>
>     		<version>1.0-SNAPSHOT</version>
>     	</dependency>

Так же фазы можно запускать последовательно одной командой:

```ps
mvn clean compile test-compile test
```

Ну и главное - а как запустить проект?

```ps
mvn exec:java -Dexec.mainClass="ru.cmx.maven.example.App"
```

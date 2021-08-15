## Introduction_to_Jenkins
========================

**1. Устанавливаем docker.**

Любым способом, подходящим для Windows или Linux.<br><br>
Например:<br>
https://www.docker.com/products/docker-desktop

----
**2. Запускаем docker, скачивая образ Linux с Jenkins**<br><br>
```docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts```<br><br>
*После инсталяции Jenkins будет крутится локально по адресу  ```http://localhost:8080```

----
**3. Переходим по ссылке ```http://localhost:8080```**
После перехода нам на странице нужно будет ввести пароль.<br><br>
Чтобы его найти: <br>
- Нужно ввести: ```docker ps```<br>
- Найти образ **jenkins/jenkins**.<br>
- Скопировать **CONTAINER ID**<br>
- Ввести ```docker logs < название ID>```<br>
- В логах, после строки **Please use the following password to proceed to installation**, будет пароль для входа

----
**4. Создаем аккаунт**<br><br>
*После создания аккаунта, нам больше не понадобится пароль из  ```docker logs```.

----
**5. Создаем проект/задачу.**<br><br>
- ```new_item -> freestyle_project``` 

----
**6. Конфигурируем.**<br><br>
Наример:<br>
1. Создаем **build steps**:<br>
  Во вкладке **Build** -> ```Executed shell``` <br>
  Вводим консольные команды для управления проектом, вводим скрипты и т.д.<br><br>
  
2. Создаем параметризиованный билд<br>
  ```General -> This project is parameterized```<br>
  *Он нужен что бы при создании билда передать какой то текст, что то поменять, пароль, опции.
  
----
**7. Устанавливаем плагины.**<br><br>
- Maven
Сборка этого проекта идет на Maven согласно файлу ```.pom```. Он должен быть в проекте на Github для сбрки. <br>
Шаги:<br>
1. ```Manage Jenkins -> Global Tool Configuration```<br>
2. ```Maven -> name```
3.  выбрать ```Install version```
4.  поставить галочку ```Install automatically```
5.  ```Apply -> Save```<br><br>

- Установка JDK<br>
Изначально Jenkins поддерживает JDK 9,  и мы можем выбрать только до 9 версии.<br>
Если нам нужны последние версии:<br>
Шаги:<br>
1. ```Manage Jenkins -> Manage Plugins```.
2. Установить ```AdoptOpenJDK installer Plugin``` (Устанавливаем, Jenkins перезагружаем)
3. Далее опять ```Manage Jenkins -> Global Tool Configuration -> Add JDK```
4. Устанавливаем имя
5. Добавляем ```Add installer -> Install from adoptopenjdk.net```
6. Выбираем версию
7. ```Apply -> Save```<br><br>

*По умолчанию JDK 9 удалите - кнопка ```Delete JDK```.

----
**8. Интеграция с GitHub.**<br><br>
*Для сборки должны быть необходимые зависимости для успешной сборки Java проекта.<br>
Шаги:<br>
1. ``` Configure -> Source Code Management```
2. Перключаем на ```Git```
3. Вставляем в *Repository URL*. Например: ```https://github.com/legionqa/ChessGame.git````
4. Добавляем в один из``` Add build step ```-> ```Invoke top-level Maven targets```.<br>
Так как сборка просиходит через Maven
5. Выбираем версию Maven
Далее необходимы команды для Maven:  ```https://maven.apache.org/plugins/index.html```<br>
6. В поле ```Goals```, под установкой версии Maven вставляем команду ```compile```
7. Собираем проект.
8. После заглядываем в ```Console Output```. Можно посмотреть какие git команды запускаются.<br>
В ```Workspace``` скачались файлы с git репозитория

*Если репозиторий не публичный будет необходима настройка *Credential*

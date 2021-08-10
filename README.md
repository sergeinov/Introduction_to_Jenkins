## Introduction_to_Jenkins
========================

**1. Устанавливаем docker.**

Любым способом, подходящим для Windows или Linux.<br><br>
Например:<br>
https://www.docker.com/products/docker-desktop

----
**2. Запускаем docker, скачивая образ Linux с Jenkins**<br><br>
```docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts```<br><br>
После инсталяции Jenkins будет крутится локально по адресу  ```http://localhost:8080```

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
**4. Устанавливаем плагины. Создаем аккаунт**<br><br>
После создания аккаунта, нам больше не понадобится пароль из  ```docker logs```.

----
**5. Создаем проект/задачу.**<br><br>
- ```new_item -> freestyle_project``` 

----
**6. Конфигурируем.**<br><br>
Создаем **build steps**:<br>
Во вкладке **Build** -> ```Executed shell``` 


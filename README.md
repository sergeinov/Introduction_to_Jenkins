## Introduction_to_Jenkins
===
**1. Устанавливаем docker.**

Любым способом подходящим для Windows или Linux.

Например:

https://www.docker.com/products/docker-desktop


---
**2. Запускаем docker, скачивая систему с Jenkins**


docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts


После инсталяции Jenkins будет крутится локально по адресу  http://localhost:8080

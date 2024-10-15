## Развертывание своего сервиса в kubernetes

### Шаг 1: Запуск Minikube

Откройте терминал и запустите следующую команду, чтобы создать локальный кластер Kubernetes:

```
minikube start
```
![Desktop_241015_1744](https://github.com/user-attachments/assets/93b50d40-e717-4295-82ed-b35374e817a9)

### Шаг 2: Разверните ресурсы Kubernetes с помощью одной команды

Разверните ресурсы Kubernetes с помощью одной команды:

```
kubectl apply -f deployment.yaml -f service.yaml -f configmap.yaml
```
![Desktop_241015_1744_1](https://github.com/user-attachments/assets/8c10a483-ca54-47d5-a528-21d4c7a59b92)

### Шаг 3: Проверьте работоспособность сервиса

Проверьте работоспособность сервиса, используя команду:

```
minikube service hello-world-service --url
```
![Desktop_241015_1745](https://github.com/user-attachments/assets/a0b49270-4213-468b-8e1b-d0ee758ba690)

Вывод должен быть похож на следующий:

http://192.168.99.100:30000

Откройте веб-браузер и перейдите по этому URL, чтобы увидеть страницу "Hello, World!".

![Desktop_241015_1746](https://github.com/user-attachments/assets/b36e6085-7fdf-4427-bca8-a428fef9710a)
## Результат:

Вы успешно подняли локальный Kubernetes кластер с помощью Minikube, развернули свой сервис, используя 2-3 ресурса Kubernetes, и проверили работоспособность сервиса.

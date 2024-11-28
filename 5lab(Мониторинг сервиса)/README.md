## Мониторинг сервиса с помощью prometheus и grafana

Для выполнения задания по мониторингу сервиса, развернутого в Kubernetes с использованием Prometheus и Grafana, следуйте пошаговой инструкции ниже. Я опишу процесс, который вы можете выполнить на своей машине или в облаке.

Шаг 1: **Установка Minikube (если еще не установлен)**

Если у вас еще нет установленного Kubernetes, вы можете использовать Minikube для локального развертывания.

Установите Minikube, следуя официальной документации.
Запустите Minikube:

```
    minikube start
```

![alt text](/img/Desktop_241128_0259.jpg)

Мы будем использовать Helm для установки Prometheus и Grafana.

Шаг 2: **Установка Helm**

Если у вас еще не установлен Helm, выполните следующие команды для установки:

```
	curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
```

![alt text](/img/Desktop_241128_0301.jpg)

Чтобы проверить, установлен ли Helm на вашем компьютере, вы можете выполнить следующую команду в терминале или командной строке:

```
	helm version
```

Ожидаемый результат

Если Helm установлен, вы увидите информацию о версии Helm, например:

```
	version.BuildInfo{Version:"v3.5.4", GitCommit:"abcdef123", GitTreeState:"clean", GoVersion:"go1.15.6"}
```

Если Helm не установлен, вы получите сообщение об ошибке, например:

```
	bash: helm: command not found
```

или

```
	'helm' is not recognized as an internal or external command, operable program or batch file.
```

![alt text](/img/image.png)
Шаг 3: **Установка Prometheus и Grafana**

Добавьте репозиторий с графиками для Prometheus и Grafana:

```
    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
    helm repo add grafana https://grafana.github.io/helm-charts
    helm repo update
```

![alt text](/img/image-1.png)

Установите Prometheus:

```
    helm install prometheus prometheus-community/prometheus
```

![alt text](/img/image-2.png)
Установите Grafana:

```
    helm install grafana grafana/grafana
```

![alt text](/img/image-3.png)

Шаг 4: **Проверка установки**

Убедитесь, что оба сервиса запущены:

```
kubectl get pods
```

![alt text](/img/image-4.png)

Шаг 5: **Настройка доступа к Grafana и к Prometheus**

Получите пароль для Grafana:

```
    kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```

![alt text](/img/image-5.png)

Настройте порт-форвардинг для доступа к Grafana и к Prometheus:

```
    kubectl port-forward svc/grafana 3002:80 & kubectl port-forward svc/prometheus-server 9092:80 &
```

![alt text](/img/image-6.png)

Теперь вы можете открыть Grafana в браузере по адресу http://localhost:3002. Войдите, используя логин admin и полученный пароль.

![alt text](/img/image-7.png)

Шаг 6: **Настройка источника данных в Grafana**

- Добавьте источник данных Prometheus:

- Перейдите в "Connection".

- Введите и выберите "Prometheus"

- Нажмите "Add data source".

- В поле URL введите http://prometheus-server:80.

- Нажмите "Save & Test".

![alt text](/img/image-8.png)

![alt text](/img/image-9.png)

Шаг 6: **Добавление дашборда**

В меню выбираем Dashboards и кликаем по Import. Используем уже готовый дашборд с номерами 8171 и 15759. Больше готовых дашбордов можно взять на сайте графаны.

![alt text](/img/image-10.png)

Установим prometheus в качестве источника данных для дашборда и нажмём Import.
![alt text](/img/image-11.png)

![alt text](/img/image-13.png)

![alt text](/img/image-12.png)

### Заключение

Теперь у вас есть работающий мониторинг сервиса в Kubernetes с использованием Prometheus и Grafana. Вы можете настраивать дополнительные метрики и графики в зависимости от ваших потребностей.

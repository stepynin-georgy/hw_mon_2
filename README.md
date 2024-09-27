# Домашнее задание к занятию 14 «Средство визуализации Grafana»

## Задание повышенной сложности

**При решении задания 1** не используйте директорию [help](./help) для сборки проекта. Самостоятельно разверните grafana, где в роли источника данных будет выступать prometheus, а сборщиком данных будет node-exporter:

- grafana;
- prometheus-server;
- prometheus node-exporter.

За дополнительными материалами можете обратиться в официальную документацию grafana и prometheus.

В решении к домашнему заданию также приведите все конфигурации, скрипты, манифесты, которые вы 
использовали в процессе решения задания.

**При решении задания 3** вы должны самостоятельно завести удобный для вас канал нотификации, например, Telegram или email, и отправить туда тестовые события.

В решении приведите скриншоты тестовых событий из каналов нотификаций.

## Обязательные задания

### Задание 1

1. Используя директорию [help](./help) внутри этого домашнего задания, запустите связку prometheus-grafana.
1. Зайдите в веб-интерфейс grafana, используя авторизационные данные, указанные в манифесте docker-compose.
1. Подключите поднятый вами prometheus, как источник данных.
1. Решение домашнего задания — скриншот веб-интерфейса grafana со списком подключенных Datasource.

Используя [docker-compose.yml](https://github.com/stepynin-georgy/hw_mon_2/blob/main/docker-compose.yml) развернул grafana, prometheus и node-exporter:

![изображение](https://github.com/stepynin-georgy/hw_mon_2/blob/main/img/Screenshot_101.png)

![изображение](https://github.com/stepynin-georgy/hw_mon_2/blob/main/img/Screenshot_92.png)

![изображение](https://github.com/stepynin-georgy/hw_mon_2/blob/main/img/Screenshot_93.png)

Проверка подключенного datasource:

![изображение](https://github.com/stepynin-georgy/hw_mon_2/blob/main/img/Screenshot_95.png)

![изображение](https://github.com/stepynin-georgy/hw_mon_2/blob/main/img/Screenshot_94.png)

## Задание 2

Изучите самостоятельно ресурсы:

1. [PromQL tutorial for beginners and humans](https://valyala.medium.com/promql-tutorial-for-beginners-9ab455142085).
1. [Understanding Machine CPU usage](https://www.robustperception.io/understanding-machine-cpu-usage).
1. [Introduction to PromQL, the Prometheus query language](https://grafana.com/blog/2020/02/04/introduction-to-promql-the-prometheus-query-language/).

Создайте Dashboard и в ней создайте Panels:

- утилизация CPU для nodeexporter (в процентах, 100-idle);

``` 100 - (avg(rate(node_cpu_seconds_total{job=~"node_exporter",mode="idle"}[5m])) * 100) ```

- CPULA 1/5/15;

```
avg(node_load1{job="node_exporter"})
avg(node_load5{job="node_exporter"})
avg(node_load15{job="node_exporter"})
```

- количество свободной оперативной памяти;

```
node_memory_MemFree_bytes - свободная ОЗУ
node_memory_MemTotal_bytes - общее количесвто ОЗУ
```

- количество места на файловой системе.

```
node_filesystem_avail_bytes
```

Для решения этого задания приведите promql-запросы для выдачи этих метрик, а также скриншот получившейся Dashboard.

![изображение](https://github.com/stepynin-georgy/hw_mon_2/blob/main/img/Screenshot_96.png)

## Задание 3

1. Создайте для каждой Dashboard подходящее правило alert — можно обратиться к первой лекции в блоке «Мониторинг».
1. В качестве решения задания приведите скриншот вашей итоговой Dashboard.

Создал телеграмм-бота, получил его токен и подключил в способах оповещений в Grafana:

![изображение](https://github.com/stepynin-georgy/hw_mon_2/blob/main/img/Screenshot_97.png)

Добавил алерты и увеличил нагрузку на CPU для проверки. Аллерт пришел в телеграмм:

![изображение](https://github.com/stepynin-georgy/hw_mon_2/blob/main/img/Screenshot_98.png)

![изображение](https://github.com/stepynin-georgy/hw_mon_2/blob/main/img/Screenshot_99.png)

После спада нагрузки пришло сообщение, что проблема решена:

![изображение](https://github.com/stepynin-georgy/hw_mon_2/blob/main/img/Screenshot_100.png)

## Задание 4

1. Сохраните ваш Dashboard.Для этого перейдите в настройки Dashboard, выберите в боковом меню «JSON MODEL». Далее скопируйте отображаемое json-содержимое в отдельный файл и сохраните его.
1. В качестве решения задания приведите листинг этого файла.

[dashboard.json](https://github.com/stepynin-georgy/hw_mon_2/blob/main/dashboard.json)

---

### Как оформить решение задания

Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории.

---

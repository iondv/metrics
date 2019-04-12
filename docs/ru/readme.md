This page in [English](/readme.md)

# IONDV. Metrics

Метрики является приложением IONDV. Framework. 

### Чтобы начать работать с IONDV. Framework

Перейдите
* [IONDV. Framework](https://github.com/iondv/framework/blob/master/README.md)
* [IONDV. Framework документация](https://github.com/iondv/framework/blob/master/docs/en/index.md)

## Описание

**IONDV. Metrics** -  приложение собирающее и отображающее данные собранные с помощью модуля [IONDV. Watch](https://github.com/iondv/watch).

Пример использования:

* разверните приложение IONDV. Metrics по типовой инструкции [IONDV. Framework](https://github.com/iondv/framework/blob/master/README.md) application
* или получите готовый докер образ и запустите его по типовой инструкции [IONDV. Framework](https://github.com/iondv/framework/blob/master/README.md)
* разместите html код `<div><img src="https://your.domain/watch/METRIC-IDENTIFICATOR" style="position:absolute; left:-9999px;" alt="iondv metrics"></div>` на вашей страничке с сылкой на запущенное приложение IONDV. Metrics
* или для любого приложения IONDV. Framework зайдтей в deploy.json параметр `pageEndContent` для глобальных настроек (для всех модулей) или для отдельного модуля :
```json
{
  "globals": {
    "pageEndContent": "<div><img src=\"http://your.domain/watch/METRIC-IDENTIFICATOR\" style=\"position:absolute; left:-9999px;\" height=1 width=1 alt=\"iondv-metrics\" /></div>"
  }
}
```
* откройте html страничку или IONDV приложение, например запущенное локально по адресу http://localhost:8888 для отправки метрик посещения страницы
* откройте ваше приложение http://your.domain/registry для просмотра записанных метрик

### Docker
Следуйте следующим инструкциям для запуска контейнера с приложением:

1. Запустите СУБД Mongodb

1. Запустите СУБД Mongodb

```bash
docker run  --name mongodb \
            -v mongodb_data:/data/db \
            -p 27017:27017 \
            --restart unless-stopped \
            -d \
            mongo
```

2. Разверните метаданные приложения **IONDV. Metrics**
```bash
docker run --entrypoint="" --link mongodb --rm iondv/metrics node bin/import --src ./applications/metrics --ns metrics
docker run --entrypoint="" --link mongodb --rm iondv/metrics node bin/setup metrics --reset
```

3. Создайте пользователя `admin` с паролем `123` и ролью`admin`
```
docker run --entrypoint="" --link mongodb --rm iondv/metrics node bin/adduser --name admin --pwd 123
docker run --entrypoint="" --link mongodb --rm iondv/metrics node bin/acl --u admin@local --role admin --p full
```

4. Запустите приложение
```
docker run -d -p 80:8888 --name metrics --link mongodb iondv/metrics
```

Откройте в браузере `http://localhost/watch`. Вы получите результирующий статус `OK`. Адрес в нотации `http://your.domain/watch` не отслеживается и служит для проверки состояния докер контейнера.
Откройте в браузере `http://localhost/watch/test`. Результатом будет однопиксельная картинка PNG, а результат запроса будет сохранен и доступен через модуль [**IONDV. Registry**](https://github.com/iondv/registry).
Откройте в браузере `http://localhost/registry` и после авторизации вы увидите список осуществленных запросов с параметрами запросов по адресу `http://localhost/watch/**`.



--------------------------------------------------------------------------  


 #### [Licence](/LICENCE.md) &ensp;  [Contact us](https://iondv.com) &ensp;  [English](/readme.md)   &ensp; [FAQs](/faqs.md)          

<div><img src="https://mc.iondv.com/watch/github/docs/app/metrics" style="position:absolute; left:-9999px;" height=1 width=1 alt="iondv metrics"></div>

--------------------------------------------------------------------------  

Copyright (c) 2019 **LLC "ION DV"**.  
All rights reserved. 
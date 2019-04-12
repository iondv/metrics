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


Типовые параметры для запуска docker
```bash
docker run  --name watch \
            -v /iondv-metrics/config/setup.ini:/var/www/config/setup.ini:ro \
            --port 80:8888 \
            --health-cmd="curl -f http://localhost:8888/watch" \
            --health-interval=1m30s \
            --health-timeout=10s \
            --health-retries=5 \
            --health-start-period=40s \
            --restart unless-stopped \
            -d \
            iondv-metrics
```

NB Обратите внимание, что адресс `http://your.domain/watch` не регистрируется трекером и используется для диагности статуса health в докере.


--------------------------------------------------------------------------  


 #### [Licence](/LICENCE.md) &ensp;  [Contact us](https://iondv.com) &ensp;  [English](/readme.md)   &ensp; [FAQs](/faqs.md)          

<div><img src="https://mc.iondv.com/watch/github/docs/app/metrics" style="position:absolute; left:-9999px;" height=1 width=1 alt="iondv metrics"></div>

--------------------------------------------------------------------------  

Copyright (c) 2019 **LLC "ION DV"**.  
All rights reserved. 
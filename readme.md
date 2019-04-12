Эта страница на [Русском](/docs/ru/readme.md)

# IONDV. Metrics

Metrics is a IONDV. Framework application. 

### Start with IONDV. Framework

* [IONDV. Framework Core](https://github.com/iondv/framework/blob/master/README.md)
* [IONDV. Framework Docs](https://github.com/iondv/framework/blob/master/docs/en/index.md)

## Description 

**IONDV. Metrics** -  is an application for collect and show metrics witch [IONDV. Watch](https://github.com/iondv/watch) module.

Typical use:

* build your IONDV. Metrics application with instructions for typical [IONDV. Framework](https://github.com/iondv/framework/blob/master/README.md) application 
* or get ready docker image and start with typical instraction [IONDV. Framework](https://github.com/iondv/framework/blob/master/README.md)
* place html code `<div><img src="https://your.domain/watch/METRIC-IDENTIFICATOR" style="position:absolute; left:-9999px;" alt="iondv metrics"></div>` in your html with URL to IONDV. Metrics application
* or set IONDV. Framework application deploy.json `pageEndContent` params in globals (for all modules) or module (for once):
```json
{
  "globals": {
    "pageEndContent": "<div><img src=\"http://your.domain/watch/METRIC-IDENTIFICATOR\" style=\"position:absolute; left:-9999px;\" height=1 width=1 alt=\"iondv-metrics\" /></div>"
  }
}
```
* open html page or IONDV application, for example http://localhost:8888 for send metrics information about this page visit
* open http://your.domain/registry to view saved metrics


Typical params for docker run
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

NB Request adress http://your.domain/watch didn't tracking, and used for check docker health status


--------------------------------------------------------------------------  


 #### [Licence](/LICENCE.md) &ensp;  [Contact us](https://iondv.com) &ensp;  [Russian](/docs/ru/readme.md)   &ensp; [FAQs](/faqs.md)          

<div><img src="https://mc.iondv.com/watch/github/docs/app/metrics" style="position:absolute; left:-9999px;" height=1 width=1 alt="iondv metrics"></div>

--------------------------------------------------------------------------  

Copyright (c) 2019 **LLC "ION DV"**.  
All rights reserved. 
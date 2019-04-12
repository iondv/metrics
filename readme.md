Эта страница на [Русском](/docs/ru/readme.md)

# IONDV. Metrics

Metrics is a IONDV. Framework application. 

### Start with IONDV. Framework

* [IONDV. Framework Core](https://github.com/iondv/framework/)
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
* open http://your.domain/registry to view saved metrics.


### Docker
Follow these steps to deploy docker container:

1. Run mongodb

```bash
docker run  --name mongodb \
            -v mongodb_data:/data/db \
            -p 27017:27017 \
            --restart unless-stopped \
            -d \
            mongo
```

2. Deploy your **IONDV. Metrics** application
```bash
docker run --entrypoint="" --link mongodb --rm iondv/metrics node bin/import --src ./applications/metrics --ns metrics
docker run --entrypoint="" --link mongodb --rm iondv/metrics node bin/setup metrics --reset
```

3. Create user `admin` with password `123` and `admin` role
```
docker run --entrypoint="" --link mongodb --rm iondv/metrics node bin/adduser --name admin --pwd 123
docker run --entrypoint="" --link mongodb --rm iondv/metrics node bin/acl --u admin@local --role admin --p full
```

4. Start application
```
docker run -d -p 80:8888 --name metrics --link mongodb iondv/metrics
```

Open `http://localhost/watch` in your browser. Result status is `OK`. Adress http://your.domain/watch didn't tracking, and used for health check for Docker container.
Open `http://localhost/watch/test` in your browser. Result is the small image in PNG and your request is saved in [**IONDV. Registry**](https://github.com/iondv/registry).
Open `http://localhost/registry` in your browser, and after authorisation you will see list with made requests to `http://localhost/watch/**`.


--------------------------------------------------------------------------  


 #### [Licence](/LICENCE.md) &ensp;  [Contact us](https://iondv.com) &ensp;  [Russian](/docs/ru/readme.md)   &ensp; [FAQs](/faqs.md)          

<div><img src="https://mc.iondv.com/watch/github/docs/app/metrics" style="position:absolute; left:-9999px;" height=1 width=1 alt="iondv metrics"></div>

--------------------------------------------------------------------------  

Copyright (c) 2019 **LLC "ION DV"**.  
All rights reserved. 
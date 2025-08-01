# 📁 Логирование с Fluent Bit + OpenSearch + OpenSearch Dashboards  
  
Этот комплект поднимает систему сбора, хранения и визуализации логов для Docker-контейнеров на одном хосте.  

1. **`fluent-bit`** — агент для сбора логов всех Docker-контейнеров на хосте.  
2. **`opensearch`** — хранилище логов (аналог Elasticsearch).  
3. **`opensearch-dashboards`** — веб-интерфейс для просмотра и анализа логов (аналог Kibana).  
4. Доступ к Dashboards —  домен через **Traefik** с HTTPS.  
  
## Настройка  
### 1. Установите пароль в `docker-compose.yml`  
В секции `opensearch` замените пароль:  
```   
environment:  
  - 'OPENSEARCH_INITIAL_ADMIN_PASSWORD=ваш_пароль'  
```  
### 2. Установите тот же пароль в `./conf/fluent-bit.conf`  
В секции `[OUTPUT]` к `opensearch` укажите правильный пароль:   
```  
[OUTPUT]  
    Name  opensearch  
    Match *  
    Host  opensearch  
    Port  9200  
    Suppress_Type_Name On  
    Index docker  
    HTTP_User admin  
    HTTP_Passwd ваш_пароль   # ← здесь  
    tls     On  
    tls.verify Off  
```  
🔁 Пароль должен быть **одинаковым** в `docker-compose.yml` и `fluent-bit.conf`  
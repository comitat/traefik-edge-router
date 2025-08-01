### Harbor с Traefik
**Harbor** (частный Docker Registry) с автоматическим HTTPS через **Traefik**.
  
####  Скачай и распакуй Harbor  
```  
# Скачать офлайн-установщик (последняя на данный момент версия — 2.13.2)  
wget https://github.com/goharbor/harbor/releases/download/v2.13.2/harbor-offline-installer-v2.13.2.tgz  

# Распаковать  
tar -xzvf harbor-offline-installer-v2.13.2.tgz  
  
# Перейти в папку  
cd harbor  
```  
#### Настройка `harbor.yml`  
```  
# Следует указать свой адрес и внешний  
hostname: registry.yourdomain.com  
external_url: https://registry.yourdomain.com  
  
http:  
  port: 80  
  
```  
  
Подготовка окружения `./prepare`  
  
Запуск окружения   
```  
docker compose up -d
```  
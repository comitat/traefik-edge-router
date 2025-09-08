# 📊 Monitoring Stack (Prometheus + Loki + Grafana)  
проект разворачивает полноценный стек мониторинга на базе Docker и Traefik, включая сбор метрик, логов и визуализацию.  
  
---  
## Как запустить  
```  
mkdir -p ./data/grafana  
chown -R 472:472 ./data/grafana  
  
# Поднятие стека  
docker-compose up -d  
```  
  
После запуска:  
Grafana будет автоматически настроена с источниками данных (Prometheus, Loki).  
Perses нужно настроить вручную (см. ниже).  
  
---  
### Bonus: Perses  
Perses — это экспериментальный, GitOps-ориентированный аналог Grafana.   
  
---  
- Docker Compose — оркестрация контейнеров  
- Traefik v3 — реверс-прокси, HTTPS, Let's Encrypt  
- Basic Auth — защита доступа  
- Let's Encrypt — бесплатные TLS-сертификаты  
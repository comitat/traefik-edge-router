## 🤖 Robots.txt Blocker
Сервис, запрещающий индексацию для всех поисковых роботов на тестовых и внутренних стендах. 
#### Что делает  
Сервис, блокирующий доступ к `/robots.txt` на домене:  
```  
User-agent: *  
Disallow: /  
```  
Можно блокировать на указанных поддоменах, в docker compose есть пример 
Полностью запрещает сканирование сайта поисковиками  
  
Можно дополнительно добавить basic auth    
```  
- "traefik.http.middlewares.robots-auth.basicauth.users=user:$$apr1$$..."  
- "traefik.http.routers.robots-https.middlewares=robots-compress,robots-auth"  
```  
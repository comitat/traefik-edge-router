# Forgejo Self-Hosted Git Server

Forgejo — это легковесная свободная альтернатива GitHub/GitLab, основанная на Gitea.  
Этот проект предоставляет готовую конфигурацию для запуска Forgejo с PostgreSQL и Traefik в Docker.

## Требования

- Docker и Docker Compose
- Доступ к домену (например, `git.your-domain.com`)
- Traefik как внешний reverse proxy (уже должен быть настроен с TLS-резолвером `myresolver`)

## Установка

1. Склонируйте этот репозиторий.
2. Отредактируйте `docker-compose.yml`:
   - Укажите свой пароль от БД.
   - Замените `git.your-domain.com` на ваш домен.
3. Запустите:  
```  
   docker-compose up -d  
```  
4. Откройте https://git.your-domain.com в браузере и завершите установку (первый пользователь станет администратором)  
  
#### Пример создания пользователя  
Пользователя можно создать через UI интерфейс, зайдя на url адрес указанного домена.   
Или, к примеру, командой для докер контейнера  
```   
docker exec -u git forgejo \  
  /usr/local/bin/gitea admin user create \  
    --admin \  
    --username name \  
    --password 'your-strong-passwd' \  
    --email admin@mail.com  
```
  
## SSH-доступ  
  
Forgejo слушает SSH на порту 2222. Чтобы использовать Git по SSH:  
  
1. Добавьте свой публичный SSH-ключ в профиль через веб-интерфейс (Settings → SSH Keys).  
2. Клонируйте репозитории так:  
```  
GIT_SSH_COMMAND="ssh -i /path/to/your/private_key -p 2222" \
  git clone ssh://git@git.your-domain.com:10022/username/repo.git
```   
3. Для удобства создайте `~/.ssh/config`:  
```  
Host git.your-domain.com  
  Port 2222  
  User git  
  IdentityFile /path/to/your/private_key  
  IdentitiesOnly yes  
```  
После этого можно использовать обычные команды:  
```  
git clone git@git.your-domain.com:username/repo.git  
```  
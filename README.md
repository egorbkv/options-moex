# MOEX Options Chain — Деплой

## Разовая настройка на сервере

SSH на сервер и выполни один раз:

```bash
# Клонируй репо в /var/www/options-moex
cd /var/www
sudo git clone https://github.com/ВАШ_ЮЗЕР/options-moex.git options-moex
sudo chown -R $USER:$USER /var/www/options-moex

# Nginx конфиг
sudo cp /var/www/options-moex/nginx.conf /etc/nginx/sites-available/options-moex
sudo ln -sf /etc/nginx/sites-available/options-moex /etc/nginx/sites-enabled/options-moex
sudo nginx -t && sudo systemctl reload nginx

# SSL через Let's Encrypt (если certbot уже стоит)
sudo certbot --nginx -d options.exclusivehub.link
```

## DNS

В панели своего DNS-провайдера добавь A-запись:

```
options.exclusivehub.link  →  <IP твоего сервера>
```

(тот же IP, что у exclusivehub.link)

## GitHub — секреты

В новом репо (Settings → Secrets → Actions) добавь те же три секрета, что и в expense-tracker:

- `SSH_HOST` — IP сервера
- `SSH_USER` — имя пользователя на сервере
- `SSH_PRIVATE_KEY` — приватный SSH-ключ

## Дальнейший деплой

После первоначальной настройки любой `git push` в `master` автоматически обновит сайт.

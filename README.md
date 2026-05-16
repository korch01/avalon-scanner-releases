# Avalon Scanner — публичные релизы

Этот репозиторий **только для дистрибутива** (zip + `version.json`). Исходный код — в закрытом репозитории `avalon-scanner`.

## Файлы

| Файл | Назначение |
|------|------------|
| `version.json` | Манифест для автообновления GUI (версия, URL zip, SHA256) |
| Releases | Архивы `avalon-windows-portable-amd64.zip` по тегам `v*` |

## Первичная настройка

1. Создайте **публичный** репозиторий `avalon-scanner-releases` на GitHub.
2. Залейте содержимое этой папки в `main`.
3. В **закрытом** репозитории `avalon-scanner` создайте Fine-grained PAT или classic token с правами на **этот** репозиторий: Contents (read/write).
4. Добавьте секрет в `avalon-scanner` → Settings → Secrets → Actions: **`RELEASES_TOKEN`**.

После этого каждый тег `v*` в закрытом репо соберёт zip и опубликует сюда через CI.

## Ручная публикация

Из закрытого репозитория (после `make build-windows`):

```bash
export RELEASES_TOKEN=ghp_...
VERSION=1.0.0 TAG=v1.0.0 SHA256=$(sha256sum dist/avalon-windows-portable-amd64.zip | awk '{print $1}')
./scripts/publish-releases-public.sh
```

## Ссылки для приложения

- Манифест: `https://raw.githubusercontent.com/korch01/avalon-scanner-releases/main/version.json`
- Последний релиз: `https://github.com/korch01/avalon-scanner-releases/releases/latest`

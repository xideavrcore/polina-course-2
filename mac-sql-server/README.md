# SQL Server в Docker для Mac (вне папок лабораторных)

Эта папка **не является частью** лабораторных работ `3/` и `4/`.  
Она нужна только для локального запуска MvcMovie на macOS, где нет SQL Server LocalDB.

Код лабораторной работы 4 остаётся как в методике: `UseSqlServer` + строка из `appsettings.json`.  
На Mac строку подключения к Docker SQL Server задаём **через переменную окружения**, не меняя `appsettings.json` в `4/`.

## Требования

- Docker Desktop
- На Apple Silicon: в Docker Desktop включите **Use Rosetta for x86_64/amd64 emulation** (Settings → General)

## Запуск SQL Server

```bash
cd "/Users/redfox/data/ЗАКАЗЫ/Полина/2 курс/polina-course-2/mac-sql-server"
docker compose up -d
```

Проверка:

```bash
docker compose ps
```

Пароль SA (как в `docker-compose.yml`): `Your_strong_Passw0rd`

## Запуск лабораторной работы 4 с переопределением строки подключения

Строка в `4/MvcMovie/appsettings.json` остаётся методической. Для Mac переопределите её переменной окружения `ConnectionStrings__MvcMovieContext` (два подчёркивания — стандарт ASP.NET Core Configuration):

```bash
export DOTNET_ROOT=$HOME/.dotnet
export PATH=$HOME/.dotnet:$PATH

cd "../4/MvcMovie"

ConnectionStrings__MvcMovieContext="Server=localhost,1433;Database=MvcMovie;User Id=sa;Password=Your_strong_Passw0rd;TrustServerCertificate=True" dotnet run
```

При старте приложение применит миграции (`Database.Migrate()`) и заполнит таблицу через `SeedData`.

Откройте в браузере: `https://localhost:7xxx/Movies` (порт смотрите в выводе `dotnet run` / `launchSettings.json`).

## Остановка

```bash
cd "/Users/redfox/data/ЗАКАЗЫ/Полина/2 курс/polina-course-2/mac-sql-server"
docker compose down
```

Чтобы удалить и данные контейнера:

```bash
docker compose down -v
```

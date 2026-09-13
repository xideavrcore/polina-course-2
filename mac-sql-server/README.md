# SQL Server в Docker для Mac (вне папок лабораторных)

Эта папка **не является частью** лабораторных работ.  
Нужна для локального запуска на macOS, где нет SQL Server LocalDB.

Строки подключения в `appsettings.json` лабораторных **не меняем** под Docker.  
На Mac переопределяем через переменные окружения ASP.NET Core (`ConnectionStrings__...`).

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

## Лаба 4–6 (MvcMovie)

```bash
export DOTNET_ROOT=$HOME/.dotnet
export PATH=$HOME/.dotnet:$HOME/.dotnet/tools:$PATH

cd "../4/MvcMovie"   # или 5/MvcMovie, 6/MvcMovie

ConnectionStrings__MvcMovieContext="Server=localhost,1433;Database=MvcMovie;User Id=sa;Password=Your_strong_Passw0rd;TrustServerCertificate=True" dotnet run
```

## Лаба 7 (ContosoUniversity)

```bash
export DOTNET_ROOT=$HOME/.dotnet
export PATH=$HOME/.dotnet:$HOME/.dotnet/tools:$PATH

cd "../7/ContosoUniversity"

ConnectionStrings__SchoolContext="Server=localhost,1433;Database=CU-1;User Id=sa;Password=Your_strong_Passw0rd;TrustServerCertificate=True" dotnet run
```

При старте: `Database.Migrate()` + `DbInitializer.Initialize`.

## Остановка

```bash
cd "/Users/redfox/data/ЗАКАЗЫ/Полина/2 курс/polina-course-2/mac-sql-server"
docker compose down
```

Чтобы удалить и данные контейнера:

```bash
docker compose down -v
```

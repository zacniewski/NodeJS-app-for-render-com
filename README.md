# NodeJS Render.com Demo App

Prosta aplikacja REST API zbudowana w NodeJS (Express.js) z bazą danych SQLite (Sequelize), przygotowana do wdrożenia na platformie Render.com.

## Funkcje
- Listowanie zadań (`GET /tasks`)
- Dodawanie zadań (`POST /tasks`)
- Aktualizacja zadań (`PUT /tasks/:id`)
- Usuwanie zadań (`DELETE /tasks/:id`)

## Przykłady użycia API (cURL)

Poniżej znajdziesz przykłady jak zarządzać zadaniami (zastąp `http://localhost:3000` adresem swojej aplikacji na Renderze, jeśli testujesz w chmurze).

### 1. Dodawanie nowego zadania (Create)
```bash
curl -X POST http://localhost:3000/tasks \
     -H "Content-Type: application/json" \
     -d '{"title": "Kupić mleko"}'
```

### 2. Pobieranie wszystkich zadań (Read)
```bash
curl http://localhost:3000/tasks
```

### 3. Aktualizacja zadania (Update)
Załóżmy, że zadanie ma ID `1`:
```bash
curl -X PUT http://localhost:3000/tasks/1 \
     -H "Content-Type: application/json" \
     -d '{"title": "Kupić mleko i chleb", "completed": true}'
```

### 4. Usuwanie zadania (Delete)
```bash
curl -X DELETE http://localhost:3000/tasks/1
```

## Instalacja lokalna

1. Sklonuj repozytorium:
   ```bash
   git clone <url-twojego-repozytorium>
   cd NodeJS-app-for-render-com
   ```

2. Zainstaluj zależności:
   ```bash
   npm install
   ```

3. Uruchom aplikację:
   ```bash
   npm start
   ```
   Aplikacja będzie dostępna pod adresem: `http://localhost:3000`

---

# Tutorial: Wdrożenie na Render.com (Krok po kroku)

Ten przewodnik pomoże Ci wdrożyć tę aplikację na platformie Render.com.

## Krok 1: Przygotowanie repozytorium GitHub

Upewnij się, że Twój kod znajduje się w publicznym lub prywatnym repozytorium na GitHub (lub GitLab/Bitbucket).

## Krok 2: Rejestracja i logowanie na Render.com

1. Wejdź na stronę [render.com](https://render.com/) i załóż darmowe konto.
2. Po zalogowaniu zostaniesz przeniesiony do panelu sterowania (Dashboard).

## Krok 3: Tworzenie nowej usługi (Web Service)

1. W panelu Render kliknij przycisk **"New +"** i wybierz **"Web Service"**.

> ![Placeholder: Ekran wyboru New Web Service]

2. Połącz swoje konto GitHub i wybierz repozytorium `NodeJS-app-for-render-com`.

> ![Placeholder: Ekran wyboru repozytorium z GitHub]

## Krok 4: Konfiguracja usługi

Wypełnij formularz konfiguracji następującymi danymi:

- **Name**: Dowolna nazwa (np. `my-node-app`)
- **Region**: Wybierz najbliższy (np. `Frankfurt (EU Central)`)
- **Branch**: `main`
- **Root Directory**: (pozostaw puste)
- **Runtime**: `Node`
- **Build Command**: `npm install`
- **Start Command**: `npm start`

W sekcji **Instance Type** wybierz darmowy plan (**Free**).

> ![Placeholder: Formularz konfiguracji usługi na Render]

## Krok 5: Konfiguracja bazy danych (SQLite lub PostgreSQL)

Ponieważ Render używa efemerycznego systemu plików (zmiany w plikach znikają po restarcie), w darmowym planie baza SQLite będzie się resetować przy każdym wdrożeniu. Aby zachować dane, na Renderze zazwyczaj używa się dysków (Blueprints/Disks), ale w darmowym planie Web Service możemy po prostu korzystać z bazy w pamięci lub akceptować resetowanie. 

Jeśli chcesz, aby baza była trwała i profesjonalna, zalecane jest użycie PostgreSQL. Render oferuje darmowy plan dla Postgres (na 90 dni).

### Opcja A: SQLite (Dla szybkich testów)
1. Kliknij **Advanced** w konfiguracji Web Service.
2. Dodaj zmienną środowiskową:
   - Key: `DATABASE_URL`
   - Value: `./database.sqlite`

> ![Placeholder: Sekcja Environment Variables dla SQLite]

### Opcja B: PostgreSQL (Zalecane)

1. W Dashboard Render kliknij **"New +"** i wybierz **"PostgreSQL"**.
2. Wypełnij nazwę bazy (np. `my-database`) i kliknij **Create Database**.
3. Po utworzeniu bazy, znajdź sekcję **"Internal Database URL"** i skopiuj jej wartość.

> ![Placeholder: Ekran z Internal Database URL w panelu Postgres]

4. Wróć do konfiguracji swojego **Web Service**.
5. W sekcji **Advanced** dodaj zmienną środowiskową:
   - Key: `DATABASE_URL`
   - Value: (wklej skopiowany URL, powinien zaczynać się od `postgres://...`)

> ![Placeholder: Sekcja Environment Variables dla Postgres]

## Krok 6: Wdrożenie (Deploy)

1. Kliknij **Create Web Service** na dole strony.
2. Render rozpocznie proces budowania i wdrażania Twojej aplikacji. Możesz śledzić postęp w konsoli logów.

> ![Placeholder: Widok logów z procesu budowania/wdrożenia]

3. Gdy status zmieni się na **"Live"**, Twoja aplikacja jest dostępna pod adresem URL widocznym w lewym górnym rogu panelu.

> ![Placeholder: Status Live i link do aplikacji]

## Krok 7: Testowanie wdrożonej aplikacji

Możesz sprawdzić czy aplikacja działa, wchodząc na jej adres URL w przeglądarce lub używając narzędzia typu Postman/cURL, aby odpytać endpoint `/tasks`.

Gratulacje! Twoja aplikacja NodeJS działa w chmurze!
# Weather App

A small Docker Compose weather application used for practicing containerized services.

The project contains four services:

- `ui`: Node.js/Express frontend served on port `3000`
- `auth`: Go authentication API served internally on port `8080`
- `weather`: Python/Flask weather API served internally on port `5000`
- `db`: MySQL database used by the auth service

## Project Structure

```text
weatherapp/
├── UI/                 # Node.js frontend
├── auth/               # Go authentication service
├── weather/            # Python weather service
├── docker-compose.yaml
└── .env-example
```

## Requirements

- Docker
- Docker Compose
- A RapidAPI key for `weatherapi-com.p.rapidapi.com`

## Environment Variables

Create a `.env` file inside the `weatherapp` directory:

```bash
cp .env-example .env
```

Then update the values:

```env
DB_USER=root
DB_PASSWORD=your_mysql_root_password
DB_NAME=weatherapp
MYSQL_ROOT_PASSWORD=your_mysql_root_password
MYSQL_DATABASE=weatherapp
APIKEY=your_rapidapi_key
```

Note: the auth service connects to MySQL as `root`, so `DB_PASSWORD` should match `MYSQL_ROOT_PASSWORD`.

## Run the App

From the `weatherapp` directory, start all services:

```bash
docker compose up --build
```

Open the app in your browser:

```text
http://localhost:3000
```

## Stop the App

```bash
docker compose down
```

To remove the MySQL data volume created at `./db-data`, delete that directory after stopping the app.

## Useful Endpoints

- UI: `http://localhost:3000`
- UI health check: `http://localhost:3000/health`
- Auth health check: available inside the Compose network at `http://auth:8080`
- Weather health check: available inside the Compose network at `http://weather:5000`

## Common Commands

Rebuild and start:

```bash
docker compose up --build
```

Run in the background:

```bash
docker compose up -d
```

View logs:

```bash
docker compose logs -f
```

Stop containers:

```bash
docker compose down
```

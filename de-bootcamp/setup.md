# Instruction Manual: Setting up Docker, pgAdmin, and Cloning a GitHub Repository

## 1. Install Docker

### Windows & Mac:
- Download Docker Desktop from [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
- Run the installer and follow the instructions.
- Start Docker Desktop after installation.

### Linux (Ubuntu example):
```sh
sudo apt update
sudo apt install docker.io
sudo systemctl start docker
sudo systemctl enable docker
```
- Add your user to the Docker group (optional, for non-root usage):
```sh
sudo usermod -aG docker $USER
```
- Log out and log back in for this to take effect.

## 2. Install Docker Compose (if not included)

### Windows & Mac:
- Docker Compose is included with Docker Desktop.

### Linux:
```sh
sudo apt install docker-compose
```

## 3. Set Up PostgreSQL and pgAdmin Using Docker Compose
1. Create a directory for your Docker setup:
```sh
mkdir pgdocker
cd pgdocker
```

2. Create a file named `docker-compose.yml` with the following content:
```yaml
version: '3.8'
services:
  db:
    image: postgres:15
    restart: always
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: mydatabase
    ports:
      - "5432:5432"
    volumes:
      - pgdata:/var/lib/postgresql/data

  pgadmin:
    image: dpage/pgadmin4
    restart: always
    environment:
      PGADMIN_DEFAULT_EMAIL: admin@admin.com
      PGADMIN_DEFAULT_PASSWORD: admin
    ports:
      - "5050:80"
    depends_on:
      - db

volumes:
  pgdata:
```

3. Start the services:
```sh
docker-compose up -d
```

4. Access pgAdmin:
- Open your browser and go to [http://localhost:5050](http://localhost:5050)
- Login with email: `admin@admin.com`, password: `admin`
- Add a new server:
  - Name: `Postgres`
  - Host: `db`
  - Username: `postgres`
  - Password: `postgres`

## 4. Clone a GitHub Repository

1. Install Git (if not already installed):

- Windows & Mac: Download from [https://git-scm.com/downloads](https://git-scm.com/downloads)
- Linux (Ubuntu):
```sh
sudo apt install git
```

2. Clone your GitHub repository:
```sh
git clone https://github.com/your-username/your-repo.git
```
- Replace `your-username/your-repo` with the actual repository path.

---


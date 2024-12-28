# Flask Blog App

This is a simple Flask-based blog application that uses Gunicorn as the WSGI HTTP server and is containerized with Docker and Docker Compose for easy deployment.

## Features
- Create, read, update, and delete blog posts.
- User authentication (login, signup, logout).
- RESTful architecture.
- Dockerized for seamless deployment.
- Runs with Gunicorn for production.

---

## Prerequisites

Ensure the following are installed:

- [Python](https://www.python.org/) (>= 3.7)
- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)

---

## Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/flask-blog-app.git
cd flask-blog-app
```

### 2. Configuration
Create a `.env` file for environment variables:
```env
FLASK_APP=app.py
FLASK_ENV=production
SECRET_KEY=your-secret-key
DATABASE_URL=sqlite:///blog.db
```

### 3. Build and Run the App

#### Using Docker Compose
1. Build the containers:
   ```bash
   docker-compose build
   ```

2. Start the services:
   ```bash
   docker-compose up
   ```

The app will be accessible at `http://localhost:5000`.

#### Running Flask App Locally (Optional)
If you want to run the app locally without Docker:

1. Create a virtual environment and activate it:
   ```bash
   python3 -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Run the Flask app:
   ```bash
   flask run
   ```

---

## Docker Compose Overview

The `docker-compose.yml` file contains the following services:

- **web**: Runs the Flask application using Gunicorn.
- **db**: (Optional) Database container for persistence (e.g., PostgreSQL).

### Sample `docker-compose.yml`
```yaml
version: '3.8'

services:
  web:
    build: .
    ports:
      - "5000:5000"
    env_file:
      - .env
    depends_on:
      - db

  db:
    image: postgres:13
    environment:
      POSTGRES_USER: your_db_user
      POSTGRES_PASSWORD: your_db_password
      POSTGRES_DB: flask_blog
    volumes:
      - db_data:/var/lib/postgresql/data

volumes:
  db_data:
```

---

## Gunicorn Configuration

Gunicorn is used for running the application in a production-ready setup. The configuration can be customized in the `gunicorn_config.py` file.

### Sample `gunicorn_config.py`
```python
bind = "0.0.0.0:5000"
workers = 3
threads = 2
```

---

## File Structure
```
flask-blog-app/
├── app.py              # Main application entry point
├── requirements.txt    # Python dependencies
├── Dockerfile          # Docker build configuration
├── docker-compose.yml  # Docker Compose configuration
├── .env                # Environment variables
├── gunicorn_config.py  # Gunicorn configuration
├── static/             # Static files (CSS, JS, images)
├── templates/          # HTML templates
└── README.md           # Project documentation
```

---

## Contributing

Feel free to submit issues or pull requests for improvements and new features. Contributions are welcome!

---

## License

This project is licensed under the [MIT License](LICENSE).

---

## Acknowledgments

- Flask: [Flask Documentation](https://flask.palletsprojects.com/)
- Gunicorn: [Gunicorn Documentation](https://gunicorn.org/)
- Docker: [Docker Documentation](https://docs.docker.com/)

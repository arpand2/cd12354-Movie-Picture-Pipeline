FROM python:3.10-slim

# Install system dependencies
RUN apt-get update && apt-get install -y \
    gcc \
    libpcre3-dev \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Install pipenv
RUN pip install pipenv

# Copy dependency files
COPY Pipfile* ./

# Install dependencies
RUN pipenv install --system --deploy --ignore-pipfile

# Copy application code
COPY . .

# Create non-root user
RUN useradd -m appuser && chown -R appuser /app
USER appuser

EXPOSE 5000

CMD ["pipenv", "run", "serve"]
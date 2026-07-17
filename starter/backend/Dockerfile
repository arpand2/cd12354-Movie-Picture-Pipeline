FROM python:3.10-slim

# Install system dependencies (use libpcre2-dev instead of libpcre3-dev)
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    gcc \
    libpcre2-dev \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Install pipenv
RUN pip install --no-cache-dir pipenv

# Copy dependency files
COPY Pipfile* ./

# Install Python dependencies
RUN pipenv install --system --deploy --ignore-pipfile

# Copy application code
COPY . .

# Create non-root user
RUN useradd -m appuser && chown -R appuser /app
USER appuser

EXPOSE 5000

CMD ["pipenv", "run", "serve"]
FROM python:3.12-slim

WORKDIR /app

# Install system dependencies for pip packages
RUN apt-get update && apt-get install -y \
    # Essential build tools and common libraries
    build-essential \
    libpq-dev \
    libssl-dev \
    libffi-dev \
    python3-dev \
    \
    # Cairo dependencies (resolves the "pkg-config" and "cairo" errors)
    pkg-config \
    libcairo2-dev \
    libpango1.0-dev \
    libgirepository1.0-dev \
    \
    # Cleanup to keep the image size small
    && rm -rf /var/lib/apt/lists/*

# Copy dependencies and install
COPY requirements.txt .
RUN pip install --upgrade pip \
    && pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY . .

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
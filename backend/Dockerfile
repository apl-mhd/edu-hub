# Use Python with Alpine
FROM python:3.12-alpine

# Set work directory
WORKDIR /app

# Install system dependencies needed for building Python packages
RUN apk add --no-cache --virtual .build-deps \
        gcc musl-dev libffi-dev openssl-dev python3-dev cargo \
    && apk add --no-cache libpq-dev

# Copy and install Python dependencies
COPY requirements.txt .
RUN pip install --upgrade pip \
    && pip install --no-cache-dir -r requirements.txt

# Copy the rest of the app
COPY . .

# Clean up build dependencies to reduce image size
RUN apk del .build-deps

# Expose port
EXPOSE 8000

# Run Django
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]

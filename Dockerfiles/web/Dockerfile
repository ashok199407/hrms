# Stage 1: Build Python environment and install dependencies
FROM python:3.8.18 AS builder

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Set the working directory in the container
WORKDIR /code

# Copy the requirements file into the container at /code/
COPY requirements.txt .

# Install any needed packages specified in requirements.txt
RUN pip install --upgrade pip && \
    pip install --no-cache-dir -r requirements.txt

# Stage 2: Create a lightweight runtime environment
FROM python:3.8.18-slim AS runtime

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Copy the installed dependencies from the builder stage
COPY --from=builder /usr/local/lib/python3.8/site-packages/ /usr/local/lib/python3.8/site-packages/

# Set the working directory in the container
WORKDIR /code

# Copy the application code into the container at /code/
COPY . .

# Collect static files and start Django server
CMD python manage.py makemigrations && \
    python manage.py migrate && \
    python manage.py runserver 0.0.0.0:8000

# Expose port 8000
EXPOSE 8000

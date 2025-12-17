# Django Docker Commands Cheatsheet

## 1. Initial Project Setup

# Generate Django project files in the current directory
# Note: The dot (.) at the end is important
docker-compose run web django-admin startproject <project_name> .

# Fix file permissions (Required for Linux/Arch users)
# Changes ownership of files from root to current user
sudo chown -R $USER:$USER .

## 2. Daily Development (Run & Stop)

# Start the server (logs visible in terminal)
docker-compose up

# Start the server in background (detached mode)
docker-compose up -d

# Stop containers and remove network
docker-compose down

# Rebuild the image
# Use this when you add new packages to requirements.txt
docker-compose up --build

## 3. Django Management Commands

# Create migration files (detect changes in models)
docker-compose exec web python manage.py makemigrations

# Apply migrations to the database
docker-compose exec web python manage.py migrate

# Create a superuser for Admin Panel
docker-compose exec web python manage.py createsuperuser

# Create a new Django App
# Note: Remember to add the new app to INSTALLED_APPS in settings.py
docker-compose exec web python manage.py startapp <app_name>

## 4. Deployment (Docker Hub)

# Login to Docker CLI
docker login

# Tag the image for Docker Hub
# Format: docker tag <local_image> <hub_username>/<repo_name>:<version>
docker tag <local_image_name> <username>/<image_name>:<tag>

# Push the image to Docker Hub
docker push <username>/<image_name>:<tag>

## 5. Cleanup & Maintenance

# Remove a specific container by name or ID
docker rm <container_id_or_name>

# Remove all stopped containers (Frees up space)
docker container prune

# Deep clean: Remove unused containers, networks, and dangling images
# Warning: Do not use if you want to keep cached data
docker system prune
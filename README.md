# Poetry-Docker
Install Poetry in a docker image so that Spark is available for package development


# pcservices-data-science-poetry

This repository contains a custom Docker image based on `mclg/data-science-container:1.7` with Poetry installed.  
It is designed for Python and PySpark package development in a reproducible, containerized environment using VS Code Dev Containers.

---

## Overview

- **Base image:** `mclg/data-science-container:1.7`  
- **Added:** Poetry (Python dependency and package manager)  
- **Purpose:** Provide a ready-to-use data science environment with PySpark and Poetry for package development  
- **Published image:** `ganglab/pcservices-data-science-poetry:1.0` on Docker Hub

---

## Why use this image?

- Consistent environment with all necessary dependencies pre-installed  
- Poetry makes Python package development, dependency management, and publishing easy  
- Ideal for PySpark-related projects, with Spark UI ports forwarded  
- Use with VS Code's Dev Container feature for seamless local development

---

## Building the Custom Docker Image

If you want to rebuild or customize the image locally, follow these steps:

1. Create a `Dockerfile` with the following content:

   ```Dockerfile
   FROM mclg/data-science-container:1.7

   # Install Poetry
   RUN curl -sSL https://install.python-poetry.org | python3 - \
       && echo 'export PATH="$HOME/.local/bin:$PATH"' >> /etc/profile.d/poetry.sh

2. Build the image locally (run in the folder containing the Dockerfile):
   docker build -t ganglab/pcservices-data-science-poetry:1.0 .
   
3. Push the image to Docker Hub (make sure you are logged in with `docker login`):
   docker push ganglab/pcservices-data-science-poetry:1.0

## Using the Custom Image with VS Code Dev Container

1. Make sure your project has a `.devcontainer/devcontainer.json` file. Set or update the `image` field to:
   {
  "image": "ganglab/pcservices-data-science-poetry:1.0"
   }

2. Open your project in VS Code.

3. Use the Dev Containers extension to reopen the project in the container:
   Command Palette: `Dev Containers: Reopen in Container`

4. VS Code will pull the image (if not available locally) and start a container with your environment.

5. You can now use Poetry and PySpark seamlessly inside the container.

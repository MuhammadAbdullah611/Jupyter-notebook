# Jupyter-notebook
Creating a "Hello World" application using Docker and a DevContainer in a Jupyter Notebook involves several steps. Below is a guide to achieve this:

### Step 1: Install Docker
Ensure Docker is installed on your system. If it's not installed, you can download and install it from the [official Docker website](https://www.docker.com/get-started).

### Step 2: Create a Project Directory
Start by creating a directory for your project. This will hold your Docker configuration and the Jupyter Notebook.

```bash
mkdir hello-world-docker-devcontainer
cd hello-world-docker-devcontainer
```

### Step 3: Create a Simple "Hello World" Python Script
In this directory, create a simple Python script that will print "Hello, World!".

```bash
echo 'print("Hello, World!")' > hello.py
```

### Step 4: Create a `Dockerfile`
A Dockerfile is a script that contains instructions on how to build a Docker image.

Create a `Dockerfile` in the same directory:

```Dockerfile
# Use an official Python runtime as a parent image
FROM python:3.12-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
# RUN pip install --no-cache-dir -r requirements.txt

# Make port 8888 available to the world outside this container
EXPOSE 8888

# Run hello.py when the container launches
CMD ["python", "hello.py"]
```

### Step 5: Create a `.devcontainer` Directory
DevContainers allow you to define the development environment for Visual Studio Code using Docker.

Create a `.devcontainer` directory:

```bash
mkdir .devcontainer
```

### Step 6: Create a `devcontainer.json` File
Inside the `.devcontainer` directory, create a `devcontainer.json` file to configure the development container.

```json
{
    "name": "Python Hello World",
    "dockerFile": "../Dockerfile",
    "appPort": [8888],
    "extensions": [
        "ms-python.python"
    ],
    "settings": {
        "terminal.integrated.shell.linux": "/bin/bash"
    }
}
```

### Step 7: Create a Jupyter Notebook
You can now create a Jupyter Notebook file (`.ipynb`) in the project directory to interact with the Docker container.

Here’s a simple example of what the notebook might include:

```python
# This code cell will run a Docker command from within the Jupyter Notebook
import os

# Build the Docker image
os.system('docker build -t hello-world-image .')

# Run the Docker container
os.system('docker run --rm hello-world-image')
```

### Step 8: Run the Notebook
1. Open the Jupyter Notebook and navigate to the directory containing your `.ipynb` file.
2. Execute the code cells to build and run your Docker container.

### Step 9: Open the Project in Visual Studio Code
To open this project in Visual Studio Code with the DevContainer:

1. Open VS Code.
2. Install the "Remote - Containers" extension if you haven't already.
3. Open the project directory in VS Code.
4. When prompted, reopen the project in a DevContainer.

VS Code will then build the Docker image as specified in the `devcontainer.json` file, and you will have a full-fledged development environment within a Docker container.

### Conclusion
This setup allows you to create a simple "Hello, World!" application that runs in a Docker container, with the added benefit of using a DevContainer for consistent development environments. You can expand on this by adding dependencies to your `Dockerfile`, extending the Python script, or utilizing the DevContainer further for your development workflow.

Let me know if you need any more details or help with specific parts!
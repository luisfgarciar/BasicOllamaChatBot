# Local ChatBot with Ollama and Open WebUI

This project provides a Docker Compose configuration to easily set up and run a local Large Language Model (LLM) chat interface. It integrates **Ollama** as the backend for running models and **Open WebUI** as the user-friendly frontend.

## Compose File Overview

The `compose.yaml` file orchestrates two main services:

### 1. ollama
*   **Image**: `ollama/ollama:latest`
*   **Purpose**: Acts as the backend server to run LLMs.
*   **Ports**: Exposes port `11434`.
*   **Volumes**: Persists model data locally in the `./ollama_data` directory.

### 2. open-webui
*   **Image**: `ghcr.io/open-webui/open-webui:main`
*   **Purpose**: Provides a feature-rich web interface (similar to ChatGPT) to interact with the models running on Ollama.
*   **Ports**: Accessible on the host at port `3000` (mapped to container port `8080`).
*   **Volumes**: Persists application data (users, history, etc.) in the `./webui_data` directory.
*   **Environment**: Configured with `OLLAMA_BASE_URL` to communicate directly with the `ollama` service container.

## Prerequisites

*   Docker Desktop or Docker Engine
*   Docker Compose

## How to Run

1.  **Start the services:**
    Run the following command in the directory containing `compose.yaml`:
    ```bash
    docker compose up -d
    ```

    Then pull the model manually:
    ```bash
    docker exec -it ollama ollama pull llama3.2:1b
    ```


2.  **Access the Web UI:**
    Once the containers are running, open your web browser and navigate to:
    http://localhost:3000

3.  **Stop the services:**
    ```bash
    docker compose down
    ```

# 🚀 Multi-Container LLM App

This project consists of two main components: a Node.js API server (`node-conversation-api`) and a Python LLM server (`python-llm-service`). The Node.js API server interacts with the Python LLM server to process user queries, supports selecting a model, sending queries, and maintaining conversation history.

## 🛠 Getting Started

### 📋 Prerequisites

- Docker
- Docker Compose

### 🔧 Setup

1. Clone the repository.

    ```sh
    git clone https://github.com/ANURADHAJHA99/multi-container-llm-app.git
    cd multi-container-llm-app
    ```

2. Ensure the directory structure is as follows:
    ```
    multi-container-llm-app/
    ├── docker-compose.yml
    ├── node-conversation-api/
    └── python-llm-service/
    ```

3. Build and run the Docker containers using Docker Compose.

    ```sh
    docker-compose up --build
    ```

    This command will build and start both the Node.js API server and the Python LLM server.

### 📝 Example Conversation

1. Send the first query:

    ```sh
    curl --location 'http://localhost:3000/api/conversations/query' --header 'Content-Type: application/json' --data '{
        "user_id": "123",
        "model": "llama2",
        "question": "Who is the president of the USA?"
    }'
    ```

2. Send a follow-up query to maintain context:

    ```sh
    curl --location 'http://localhost:3000/api/conversations/query' --header 'Content-Type: application/json' --data '{
        "user_id": "123",
        "model": "llama2",
        "question": "What age is he?"
    }'
    ```

## 🌐 API Endpoints

### 📦 Node.js API Server

#### 📦 Send Query

- **URL:** `/api/conversations/query`
- **Method:** `POST`
- **Request Body:**
  ```json
  {
    "user_id": "123",
    "model": "llama2",
    "question": "What is the capital of France?"
  }
  ```
- **Response:**
  ```json
  {
    "answer": "The capital of France is Paris."
  }
  ```

#### 📦 List Conversation History

- **URL:** `/api/conversations/:user_id`
- **Method:** `GET`
- **Response:**
  ```json
  [
    {
      "id": 1,
      "userId": "123",
      "question": "What is the capital of France?",
      "answer": "The capital of France is Paris.",
      "createdAt": "2023-08-05T14:12:00Z",
      "updatedAt": "2023-08-05T14:12:00Z"
    }
  ]
  ```

#### 📦 Get Conversation Details

- **URL:** `/api/conversations/detail/:id`
- **Method:** `GET`
- **Response:**
  ```json
  {
    "id": 1,
    "userId": "123",
    "question": "What is the capital of France?",
    "answer": "The capital of France is Paris.",
    "createdAt": "2023-08-05T14:12:00Z",
    "updatedAt": "2023-08-05T14:12:00Z"
  }
  ```

### 📝 Example cURL Requests

#### 📦 Send Query

```sh
curl --location 'http://localhost:3000/api/conversations/query' --header 'Content-Type: application/json' --data '{
    "user_id": "123",
    "model": "llama2",
    "question": "What is the capital of France?"
}'
```

#### 📦 List Conversation History

```sh
curl --location 'http://localhost:3000/api/conversations/123'
```

#### 📦 Get Conversation Details

```sh
curl --location 'http://localhost:3000/api/conversations/detail/1'
```

### 📑 Postman Collection

You can import the provided Postman collection [here](https://dark-resonance-874488.postman.co/workspace/public~d3c714b6-434c-42c6-96b0-ffa97ea17e00/collection/8821057-0252beef-aad2-4b21-8774-6ef98fae99cb?action=share&creator=8821057) to test the endpoints.

### 🔧 Troubleshooting

If you encounter the following error:
```
Missing baseUrl in compilerOptions. tsconfig-paths will be skipped
Unable to connect to the database: ConnectionRefusedError [SequelizeConnectionRefusedError]
```
It may be necessary to restart the server as it is hosted on-prem and may occasionally experience connection issues.

# Spring AI: RAG-Powered Knowledge Base with Vector Store

## Overview

This project showcases a robust implementation of Retrieval Augmented Generation (RAG) using Spring AI. The primary focus is on creating an intelligent knowledge base that enhances Large Language Model (LLM) responses with contextual information from PDF documents.

The system offers two vector store implementations:

1. **SimpleVectorStore**: Uses a local JSON file to store embeddings, ideal for development and smaller datasets
2. **PGVectorStore**: Leverages PostgreSQL with pgvector extension for production-grade vector similarity search

While RAG is the core functionality, the project also demonstrates other Gen-AI capabilities through Spring AI's integration with OpenAI:

- Text-to-Image generation
- Image-to-Text analysis
- Speech-to-Text transcription
- Text-to-Speech synthesis

## Features

- Spring Boot 3.3.5 with Java 21
- Spring AI integration (version 1.0.0-M3)
- PDF document processing with automatic chunking and embedding
- Dual vector storage options:
  - SimpleVectorStore (JSON-based) for development
  - PGVectorStore (PostgreSQL) for production
- Docker Compose setup for PostgreSQL with pgvector extension
- RESTful API endpoints for various AI operations
- Structured data extraction from AI responses

## API Endpoints and Functionality

All endpoints are accessible at `http://localhost:8080` when running locally.

### RAG (Retrieval Augmented Generation)

- **ICSController: Question Answering with Vector Search**
  - `GET /ics`
  - Parameters: q (string) - Your question about the Indian Constitution
  - Response: Direct text response enhanced with relevant context from the Constitution
  ```
  http://localhost:8080/ics?q=What are the fundamental rights?
  ```

  - `GET /ic`
  - Parameters: q (string) - Your question about the Indian Constitution
  - Response: Text response using custom prompt and explicit vector search
  ```
  http://localhost:8080/ic?q=Tell me about right to equality
  ```

### Gen-AI Features

- **HelloController: Text Generation**
  - `GET /`
  - Parameters: message (string) - Any text prompt
  - Response: Direct text response from GPT-4
  ```
  http://localhost:8080/?message=Tell me about Spring Framework
  ```

  - `GET /celeb`
  - Parameters: name (string) - Celebrity name
  - Response: Structured information about the celebrity
  ```
  http://localhost:8080/celeb?name=Leonardo DiCaprio
  ```

  - `GET /sports`
  - Parameters: game (string) - Sport name
  - Response: Detailed information about the sport and its rules
  ```
  http://localhost:8080/sports?game=cricket
  ```

- **ImageController: Image Processing**
  - `GET /image-to-text`
  - Parameters: url (string) - Public URL of an image
  - Response: Textual description of the image content
  ```
  http://localhost:8080/image-to-text?url=https://example.com/image.jpg
  ```

  - `GET /image/{prompt}`
  - Parameters: prompt (string) - Description of the image you want to generate
  - Response: DALL-E generated image URL (copy and open in new tab to view)
  ```
  http://localhost:8080/image/A serene landscape with mountains
  ```

- **AudioController: Audio Processing**
  - `POST /audio-to-text`
  - Body: audio file (multipart/form-data)
  - Response: Transcribed text from the audio file
  ```
  http://localhost:8080/audio-to-text
  ```

  - `GET /text-to-audio/{text}`
  - Parameters: text (string) - Text to convert to speech
  - Response: MP3 audio file (downloads automatically)
  ```
  http://localhost:8080/text-to-audio/Hello world
  ```

- **PlayerController: Structured Data**
  - `GET /player`
  - Parameters: name (string) - Player name
  - Response: JSON object with player details and statistics
  ```
  http://localhost:8080/player?name=Virat Kohli
  ```

  - `GET /achievement/player`
  - Parameters: name (string) - Player name
  - Response: JSON array of player achievements
  ```
  http://localhost:8080/achievement/player?name=Sachin Tendulkar
  ```

## Prerequisites

- Java 21 or higher
- Maven
- Docker and Docker Compose
- OpenAI API key

## Tech Stack

- Spring Boot 3.3.5
- Spring AI
- Spring Data JPA
- PostgreSQL with pgvector
- Docker
- Maven

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/kalpit00/AI-RAG-Vector-Store.git
cd spring-ai
```

### 2. Configuration

Create an `application.properties` file in `src/main/resources` with your OpenAI API credentials:

```properties
# OpenAI Configuration
spring.ai.openai.api-key=your-api-key-here
spring.ai.openai.organization-id=your-org-id-here
spring.ai.openai.project-id=your-project-id-here

# PGVector Configuration (Optional - for production use)
spring.ai.vectorstore.pgvector.index-type=HNSW
spring.ai.vectorstore.pgvector.distance-type=COSINE_DISTANCE
spring.ai.vectorstore.pgvector.dimensions=1536

spring.datasource.url=jdbc:postgresql://localhost:5432/ics
spring.datasource.username=postgres
spring.datasource.password=postgres
```

### 3. Build the Project

```bash
./mvnw clean install
```

### 4. Run with Docker Compose

```bash
docker-compose up
```

## Vector Store Options

### SimpleVectorStore (Development)

- Stores embeddings in `vector_store.json`
- No additional infrastructure needed
- Ideal for development and small datasets
- Loads entire vector store into memory

### PGVectorStore (Production)

- Uses PostgreSQL with pgvector extension
- Better performance for large datasets
- Supports concurrent access
- Efficient similarity search with indexing
- Requires Docker for PostgreSQL instance

To switch between vector stores:

1. For SimpleVectorStore: Enable `VectorLoader.java` and comment out PG-related configs
2. For PGVectorStore: Enable `PGVectorLoader.java` and Docker Compose settings

## Project Structure

```
spring-ai/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └── dailycodebuffer/
│   │   │           └── spring_ai/
│   │   │               ├── controller/
│   │   │               │   ├── AudioController.java
│   │   │               │   ├── HelloController.java
│   │   │               │   ├── ICSController.java
│   │   │               │   ├── ImageController.java
│   │   │               │   └── PlayerController.java
│   │   │               ├── model/
│   │   │               ├── config/
│   │   │               │   ├── VectorLoader.java
│   │   │               │   └── PGVectorLoader.java
│   │   │               └── SpringAiApplication.java
│   │   └── resources/
│   │       ├── vector_store.json
│   │       └── India_Constitution.pdf
│   └── test/
├── docker-compose.yaml
├── pom.xml
└── README.md
```

# Spring AI: PDF-Powered RAG Knowledge Base

## Overview

This project demonstrates a powerful implementation of Retrieval Augmented Generation (RAG) using Spring AI. It creates an intelligent knowledge base by extracting information from PDF documents, storing it in vector databases (pgvector), and leveraging OpenAI's capabilities to provide context-aware responses. The system enhances AI responses with relevant information retrieved from document repositories, making it ideal for domain-specific question answering and information retrieval applications.

## Features

- Spring Boot 3.3.5 with Java 21
- Spring AI integration (version 1.0.0-M3)
- PDF document processing capabilities
- Vector storage using pgvector
- OpenAI integration
- Docker Compose support for easy deployment
- RESTful API endpoints for text, image, and audio AI processing
- Structured data extraction from AI responses

## API Endpoints and Functionality

### Vector Store and RAG (Retrieval Augmented Generation)

- **ICSController**
  - `GET /ics`: Answers questions about the Indian Constitution
  - `GET /ic`: Uses vector search to find relevant documents and provides more accurate answers

### Text Processing

- **HelloController**
  - `GET /`: Basic prompt endpoint that returns AI response for any message
  - `GET /celeb`: Get details about a celebrity using a template-based prompt
  - `GET /sports`: Get information about sports with rules and regulations

### Image Processing

- **ImageController**
  - `GET /image-to-text`: Analyzes an image and returns a textual description
  - `GET /image/{prompt}`: Generates an image based on the provided text prompt

### Audio Processing

- **AudioController**
  - `GET /audio-to-text`: Transcribes audio files to text
  - `GET /text-to-audio/{prompt}`: Converts text to speech and returns an MP3 file

### Structured Data Extraction

- **PlayerController**
  - `GET /player`: Retrieves sports player information with achievements as structured data
  - `GET /achievement/player`: Gets a list of achievements for a specific player

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
git clone [your-repository-url]
cd spring-ai
```

### 2. Configuration

Create an `application.properties` or `application.yml` file in `src/main/resources` and configure your OpenAI API key:

```properties
spring.ai.openai.api-key=your-api-key-here
```

### 3. Build the Project

```bash
./mvnw clean install
```

### 4. Run with Docker Compose

```bash
docker-compose up
```

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
│   │   │               └── SpringAiApplication.java
│   │   └── resources/
│   └── test/
├── docker-compose.yaml
├── pom.xml
└── README.md
```

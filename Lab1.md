# Lab 1 : Variant 9 - Message Search & History

## Functional Requirements

1. A user can send messages to another user.
2. Each message has a lifecycle (sent / delivered / read).
3. The system must support:
    * search through message history by keywords;
    * pagination for historical data (loading messages in chunks).
4. The system must:
    * store messages and index them for search,
    * deliver updates asynchronously,
    * ensure high performance for search queries without affecting message delivery.
5. Recipients may be online or offline.
6. The system must ensure consistency between the primary database and the search index.

## Part 1 - Component Diagram

A **component diagram** that shows the system architecture, responsibilities, and interactions:

### Required components

* Client (Web / Mobile)
* Backend API
* Message Service
* Search Service
* Database (SQL)
* Search Index (NoSQL/Elasticsearch)
* Delivery mechanism (Queue / WebSocket / Push)



```mermaid
graph LR
  Client[Client] --> API[Backend API]
  API --> MS[Message Service]
  MS --> DB[(Primary SQL DB)]
  MS --> Queue{Message Queue}
  
  Queue --> Indexer[Indexer Service]
  Indexer --> SI[(Search Index)]
  
  API --> SS[Search Service]
  SS --> SI
  
  Queue --> DS[Delivery Service]
  DS --> Client

### Component responsibilities
Client - displays messages and handles user search/pagination requests

Backend API - entry point for user actions (send/search)

Message Service - manages message state and persistence to SQL (using Repository pattern)

Search Service - handles complex keyword searches and pagination logic

Database - persists messages for transactional integrity and long-term storage

Search Index - stores optimized, searchable copies of messages (Inverted Index)

Queue & Delivery Service - asynchronously delivers updates and indexing tasks to recipients

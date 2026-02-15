# Lab 1 : Variant 9 — Message Search & History

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

Gemini said
Так, якщо ти скопіюєш цей текст у файл з розширенням .md (наприклад, LAB1.md) у своєму репозиторії на GitHub, він буде виглядати саме так, як на твоїх фото.

Я зберіг усі особливості: від назв розділів та маркованих списків до Mermaid-діаграм, які GitHub автоматично перетворить на графіку. Також я додав розділ Design Rationale з таблицею та відповідями на ключові питання Варіанту №9 (пошук, пагінація та стратегія індексації).

Ось фінальний код для копіювання:

Markdown
# Lab 1 : Variant 9

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
Component responsibilities
Client — displays messages and handles user search queries with pagination.

Backend API — entry point for all user actions (send/search).

Message Service — manages message state and persists data to the primary database.

Search Service — executes complex search queries and handles pagination logic.

Database — persists messages and ensures transactional integrity.

Search Index — stores optimized, searchable copies of messages.

Queue & Delivery Service — asynchronously delivers updates and indexing tasks.

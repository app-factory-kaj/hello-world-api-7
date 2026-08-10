# Hello World API — Design

## Overview

A single public Ballerina service, `hello-api`, exposes one HTTP endpoint that
returns a static "Hello, World!" greeting. There is no persistence, no
authentication, and no other component — the whole product is this one
service, reachable directly from the internet through the platform gateway.

## Context (C1)

```mermaid
graph TD
    consumer["API Consumer<br/>(developer / script / service)"]
    subgraph system["Hello World API"]
        api["hello-api service"]
    end

    consumer -->|"GET /greeting"| api
```

## Domain model (ER)

No persisted entities — the service is stateless and holds no data model. The
response is a transient value object only:

```mermaid
erDiagram
    GREETING {
        string message
    }
```

## Key flows

```mermaid
sequenceDiagram
    participant C as API Consumer
    participant A as hello-api

    C->>A: GET /greeting
    A-->>C: 200 OK { "message": "Hello, World!" }
```
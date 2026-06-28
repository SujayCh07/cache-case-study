# Platform Architecture

CacheAI is an AI recruitment platform built around a simple system boundary: candidates contribute structured evidence of their work, and recruiters evaluate that evidence through controlled search and matching workflows.

This document describes the architecture at a public-safe level. It does not include production source code, exact routes, full schemas, secrets, prompts, or scoring logic.

## Architecture Layers

```mermaid
flowchart TB
    subgraph surface["Product Surfaces"]
        candidate["Candidate experience"]
        recruiter["Recruiter experience"]
        messaging["Messaging integrations"]
    end

    subgraph application["Application Layer"]
        web["Next.js web app"]
        api["API and workflow services"]
        auth["Auth and role boundary"]
    end

    subgraph intelligence["Intelligence Layer"]
        extraction["Profile structuring"]
        embeddings["Embedding services"]
        matcher["Matching engine"]
    end

    subgraph persistence["Persistence Layer"]
        db["PostgreSQL"]
        files["Document storage"]
    end

    subgraph runtime["Runtime Layer"]
        containers["Containerized services"]
        cloud["Cloud deployment"]
    end

    surface --> web
    web --> api
    api --> auth
    api --> persistence
    api --> intelligence
    intelligence --> persistence
    api --> runtime
```

See also: [system-architecture.mmd](../diagrams/system-architecture.mmd), [tech-stack-map.mmd](../diagrams/tech-stack-map.mmd), and [deployment-runtime.mmd](../diagrams/deployment-runtime.mmd).

## Component Map

| Layer | Purpose | Public-safe technologies |
| --- | --- | --- |
| Product surfaces | Candidate and recruiter experiences, plus lightweight messaging entrypoints. | Next.js, React, messaging webhooks |
| Application layer | Coordinates workflows, permissions, and service boundaries. | Next.js API layer, Node.js |
| Auth boundary | Keeps candidate and recruiter access separated. | Supabase Auth, server-side role checks |
| Data layer | Stores structured recruiting data and documents. | PostgreSQL, Supabase, object storage patterns |
| Intelligence layer | Structures profile evidence and supports semantic matching. | Embeddings, AI-assisted parsing, matching services |
| Runtime layer | Runs the web app and supporting services. | Containers, cloud deployment patterns |

## System Design Goals

- Preserve candidate and recruiter separation throughout the platform.
- Turn unstructured student work into structured, searchable recruiting records.
- Combine deterministic filters with semantic matching rather than relying on one method.
- Keep sensitive logic behind server-side boundaries.
- Make the architecture explainable without exposing product-copyable details.

## Public-Safe Data Flow

```mermaid
flowchart LR
    input["Student work and profile inputs"]
    record["Structured candidate record"]
    enrich["AI-assisted enrichment"]
    index["Searchable profile index"]
    intent["Recruiter role intent"]
    match["Matching engine"]
    review["Ranked candidate review"]

    input --> record
    record --> enrich
    enrich --> index
    intent --> match
    index --> match
    match --> review
```

## What Is Abstracted

The public architecture intentionally abstracts implementation details that would make the production system easier to copy or attack: exact schemas, privileged service boundaries, API route shapes, prompts, vendor configuration, ranking weights, and operational runbooks.

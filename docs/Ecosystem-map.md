# Netlithic Ecosystem Map

## Overview

Netlithic is an AI-native, contributor-owned blockchain ecosystem where value flows to builders, validators, users, and autonomous agents.

```mermaid
flowchart TD
    N[Netlithic Protocol]

    U[Users]
    D[Developers]
    V[Validators]
    C[Contributors]
    A[AI Agents]
    G[Governance]
    T[Treasury]
    APPS[dApps & Tools]
    POC[Proof of Contribution]
    NLT[NLT Token]
    L[Fair Launch Module]
    M[Anti-Manipulation Layer]

    U --> APPS
    D --> APPS
    APPS --> N
    V --> N
    C --> POC
    D --> POC
    V --> POC
    A --> POC

    POC --> NLT
    L --> NLT
    M --> NLT

    NLT --> G
    NLT --> V
    NLT --> APPS
    NLT --> A

    G --> T
    G --> N
    T --> D
    T --> C
    T --> APPS

    N --> G
    N --> T
    N --> M

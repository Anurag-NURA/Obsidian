
## Layers: we currently have 3 layers in tRPC
```
Client (React)
   ↓
RPC layer (tRPC procedures)
   ↓
Data layer (Prisma / DB)
```

## What Prisma is

Prisma is:
> **A database ORM (data access layer)**

Example:
```ts
await prisma.project.findUnique(...)
```
- Runs ONLY on server
- Talks directly to DB
- No HTTP
- No serialization layer

## What RPC (tRPC) is

tRPC is:
> **A communication layer between client and server**

Example:
```ts
trpc.projects.getOne(...)
```
- Client calls it
- Server executes function
- Returns result

 **Why RPC exists ?**
- Client cannot access DB directly.

## REST vs RPC

REST:  
Client → axios → API → Prisma
RPC:  
Client → function call → Prisma

## Key Insight
Prisma = data layer  
tRPC = transport layer
### The Key Difference

| Concern    | Prisma      | tRPC                          |     |
| ---------- | ----------- | ----------------------------- | --- |
| Purpose    | DB access   | Client ↔ Server communication |     |
| Runs where | Server only | Client → Server               |     |
| Talks to   | Database    | Server functions              |     |
| Replaces   | SQL         | REST API                      |     |
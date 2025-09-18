### ❌ Problem Summary:

You're running:

```bash
npx prisma migrate dev --name user_schema_created
```

And you're getting this error:

> **ERROR: permission denied to create database**  
> **Error: P3014: Prisma Migrate could not create the shadow database**

### ✅ Why It Happens:

Prisma Migrate uses a **shadow database** behind the scenes to safely generate migration SQL. To do this, it **tries to create a new database**.

Your connection string uses the user:
`anurag:asrblaze`

But as shown in your earlier screenshot, the user `anurag` **does not have permission to create databases**.

### 🛠️ Solution Options:

#### ✅ Option 1: Grant CREATE DATABASE Privilege to `anurag`

Run the following SQL as a superuser (e.g., `postgres`):
```sql
ALTER ROLE anurag CREATEDB;
```

This will allow `anurag` to create databases — required for Prisma's shadow DB during development.
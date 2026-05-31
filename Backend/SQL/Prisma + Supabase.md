First install prisma for Node.js
```bash
bun add -D prisma
bun add @prisma/client
```

then install adapter for supabase
```bash
bun add @prisma/adapter-pg pg dotenv
bun add -D @types/pg
```

Then initiate prisma in your project:
```bash
bunx prisma init
```
or
```bash
prisma init
```

Now go to your project dashboard in supabase

Click on Connect button in the navbar
![[Pasted image 20260524220101.png]]

and Select ORM with Prisma
![[Pasted image 20260524220116.png]]

copy the .env file and paste it in your project's env file

**IMPORTANT:**
Go to the prisma.config.ts file
![[Pasted image 20260524220319.png]]
and change the .env variable name from DATABASE_URL to DIRECT_URL

Create a client.ts file and add the following
```typescript
import { PrismaClient } from "../generated/prisma/client";
import { PrismaPg } from "@prisma/adapter-pg";

const adapter = new PrismaPg({ connectionString: process.env.DATABASE_URL });
export const prisma = new PrismaClient({ adapter });

export async function checkConnection() {
  try {
    // Attempt to query any table or simply test the connection
    const result = await prisma.$queryRaw`SELECT 1`;
    console.log("✅ Successfully connected to Supabase!");
    console.log("Database Response:", result);
  } catch (error) {
    console.error("❌ Connection failed:");
    console.error(error);
  } finally {
    await prisma.$disconnect();
  }
}
```

Now add schema to your schema.prisma file
![[Pasted image 20260524220503.png]]

then execute this command in the terminal shell from your project root location:
```bash
bunx prisma generate
```

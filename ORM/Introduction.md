
[[Prisma]]

https://youtu.be/RebA5J-rlwg?si=JABWBgbwMEkK4TYP
# What is Prisma

Prisma is an open-source database toolkit that provides a modern and type-safe way to interact with databases in JavaScript, TypeScript, and Node.js applications. It acts as an Object-Relational Mapper (ORM), allowing developers to query and manipulate data more easily. Prisma is especially popular in full-stack and backend development because it simplifies database management and integrates seamlessly with the TypeScript ecosystem, providing autocomplete, type-checking, and other developer-friendly features.

### Key Components of Prisma

1. **Prisma Client**: A type-safe database client for reading and writing data. It is generated automatically based on the schema you define, making it easy to query and manipulate data in a type-safe way.

2. **Prisma Migrate**: A powerful database migration tool that helps keep your database schema in sync with the Prisma schema. It allows you to create, apply, and track schema changes, making it easy to evolve the database schema as the application grows.

3. **Prisma Studio**: A GUI for browsing and managing the data in your database. It’s helpful for testing and exploring your data directly from the browser.

### How Prisma Works

To use Prisma, you define a schema in the **Prisma Schema file (`schema.prisma`)**. This schema describes your data models, relationships, and database configuration. Once defined, Prisma generates a custom client based on your schema, which you can use in your application to interact with the database directly.

### Advantages of Using Prisma

- **Type-Safety**: Integrates well with TypeScript, providing complete type safety across all database queries.
- **Data Modeling and Migrations**: Prisma Migrate makes it easy to maintain your database schema, allowing version control for database structure.
- **Supports Multiple Databases**: Compatible with popular databases like PostgreSQL, MySQL, SQLite, MongoDB (preview), and SQL Server.
- **Developer Experience**: Autocompletion, error handling, and visual data management tools improve the development workflow.

Prisma is a powerful tool that streamlines database operations, especially suited for modern applications that use TypeScript and work with relational and NoSQL databases.

# Initialising

```
npm init -y
npm i --save-dev prisma typescript ts-node
npx prisma init --datasource-provider <db name>
```

To provide a detailed summary focusing on migrations, functions, and syntaxes as explained in the video "Learn Prisma In 60 Minutes," here's an expanded walkthrough:

---
----
To generate the prisma
```prisma
npx prisma generate
npx prisma migrate dev //generates migrations
```

To connect auth with prisma
```bash
npm install @auth/prisma-adapter
```

and in the auth.ts
```ts
import NextAuth from "next-auth";
import GoogleProvider from "next-auth/providers/google";
import { PrismaAdapter } from "@auth/prisma-adapter";
import { PrismaClient } from "@prisma/client";

const prisma = new PrismaClient();

export const authOptions = {
  providers: [
    GoogleProvider({
      clientId: process.env.GOOGLE_CLIENT_ID!,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET!,
    }),
  ],
  adapter:PrismaAdapter(prisma)
};

const handler = NextAuth(authOptions);
export { handler as GET, handler as POST };
```

```
npx prisma db push
```


[[Prisma]]

Let's dive deeper into **Prisma relationships**, the `@` annotations, and other syntax elements in the Prisma schema. These features provide powerful tools for defining and working with database relationships and constraints.

---

### **1. Relationships in Prisma**

Relationships define how tables (or models) relate to each other. The main types are:

#### **a. One-to-Many Relationship**

- Example:
    
    ```prisma
    model User {
      id    Int    @id @default(autoincrement())
      name  String
      posts Post[] // A user can have multiple posts
    }
    
    model Post {
      id       Int    @id @default(autoincrement())
      title    String
      content  String?
      author   User   @relation(fields: [authorId], references: [id])
      authorId Int
    }
    ```
    
    - **Explanation**:
        - `Post` references the `User` model through the `authorId` field.
        - `@relation(fields: [authorId], references: [id])`:
            - `fields`: Specifies the foreign key in the `Post` model (`authorId`).
            - `references`: Specifies which field in the related model (`User`) is being referenced (usually the `id` field).
        - `Post[]` in the `User` model indicates a one-to-many relationship (one user can have many posts).

---

#### **b. One-to-One Relationship**

- Example:
    
    ```prisma
    model User {
      id      Int      @id @default(autoincrement())
      name    String
      profile Profile?
    }
    
    model Profile {
      id     Int    @id @default(autoincrement())
      bio    String
      user   User   @relation(fields: [userId], references: [id])
      userId Int    @unique
    }
    ```
    
    - **Explanation**:
        - The `Profile` model references the `User` model using a foreign key (`userId`).
        - `@unique` on `userId` ensures each user can have only one profile.
        - The `Profile?` in the `User` model indicates an optional one-to-one relationship (a user may or may not have a profile).

---

#### **c. Many-to-Many Relationship**

- Example:
    
    ```prisma
    model User {
      id       Int      @id @default(autoincrement())
      name     String
      projects Project[] @relation("UserProjects")
    }
    
    model Project {
      id       Int      @id @default(autoincrement())
      title    String
      members  User[]   @relation("UserProjects")
    }
    ```
    
    - **Explanation**:
        
        - Many users can be part of many projects.
        - Prisma automatically creates a join table for this relationship under the hood.
    - **Custom Join Table**:
        
        - If you want more control over the join table, define it explicitly:
            
            ```prisma
            model User {
              id       Int       @id @default(autoincrement())
              name     String
              userProjects UserProject[]
            }
            
            model Project {
              id       Int       @id @default(autoincrement())
              title    String
              userProjects UserProject[]
            }
            
            model UserProject {
              userId   Int
              projectId Int
              user     User     @relation(fields: [userId], references: [id])
              project  Project  @relation(fields: [projectId], references: [id])
              @@id([userId, projectId]) // Composite primary key
            }
            ```
            

---

### **2. `@` Annotations**

Prisma uses annotations to define constraints and behaviors for fields. Here are the key ones:

#### **a. Primary Key**

- Mark a field as the primary key using `@id`:
    
    ```prisma
    id Int @id
    ```
    

#### **b. Default Values**

- Use `@default` to set a default value:
    - Autoincrementing IDs:
        
        ```prisma
        id Int @id @default(autoincrement())
        ```
        
    - Timestamps:
        
        ```prisma
        createdAt DateTime @default(now())
        ```
        

#### **c. Unique Constraints**

- Ensure field values are unique:
    
    ```prisma
    email String @unique
    ```
    

#### **d. Composite Unique Constraints**

- Create a unique combination of multiple fields:
    
    ```prisma
    @@unique([firstName, lastName])
    ```
    

#### **e. Optional Fields**

- Use `?` to make a field optional:
    
    ```prisma
    bio String? // This field can be null
    ```
    

#### **f. Enums**

- Define a finite set of possible values:
    
    ```prisma
    enum Role {
      USER
      ADMIN
    }
    
    model User {
      id   Int   @id @default(autoincrement())
      role Role
    }
    ```
    

#### **g. Indexes**

- Add an index for faster lookups:
    
    ```prisma
    @@index([email])
    ```
    

---

### **3. Other Features**

#### **a. Cascading Deletes**

- Automatically delete related records:
    
    ```prisma
    model User {
      id    Int    @id @default(autoincrement())
      posts Post[] @relation(onDelete: Cascade)
    }
    
    model Post {
      id       Int   @id @default(autoincrement())
      userId   Int
      user     User  @relation(fields: [userId], references: [id])
    }
    ```
    

#### **b. Scalar Types**

- Supported types include:
    - **String**: Text values
    - **Int**: Integers
    - **Float**: Decimal numbers
    - **Boolean**: True/false
    - **DateTime**: Timestamps
    - **Json**: Arbitrary JSON data

#### **c. Advanced Filtering**

- Prisma supports advanced queries:
    
    ```javascript
    const users = await prisma.user.findMany({
      where: {
        AND: [
          { email: { contains: "example" } },
          { name: { startsWith: "J" } },
        ],
      },
    });
    ```
    

---

Would you like me to explore a specific concept further or explain its application in more detail?


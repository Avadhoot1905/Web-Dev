[[Nextjs|Nextjs]]
To initialize a Next.js project, follow these steps:

### **1. Install Node.js (if not already installed)**

Ensure you have **Node.js (LTS version recommended)** installed. You can check by running:

```sh
node -v
```

If not installed, download it from [Node.js official site](https://nodejs.org/).

### **2. Create a New Next.js App**

Run the following command in your terminal:

```sh
npx create-next-app@latest my-next-app
```

or using **yarn**:

```sh
yarn create next-app my-next-app
```

or using **pnpm**:

```sh
pnpm create next-app my-next-app
```

Replace `my-next-app` with your project name.

### **3. Navigate to the Project Directory**

```sh
cd my-next-app
```

### **4. Start the Development Server**

```sh
npm run dev
```

or

```sh
yarn dev
```

or

```sh
pnpm dev
```

The app will be available at **[http://localhost:3000](http://localhost:3000/)**.

### **5. Open the Project in a Code Editor**

```sh
code .
```

(If you have VS Code installed.)

### **6. (Optional) Setup Git Repository**

```sh
git init
git add .
git commit -m "Initial commit"
```

### **7. Configure Environment Variables (if needed)**

Create a `.env.local` file for storing API keys and other sensitive information.

Now, you're ready to build with **Next.js! 🚀**
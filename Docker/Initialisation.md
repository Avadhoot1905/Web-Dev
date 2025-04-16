[[ORM|ORM]]
## 📁 Let's say you have a Next.js project

Your project folder looks like this:

```
my-next-app/
├── pages/
├── public/
├── styles/
├── package.json
├── next.config.js
└── ...
```

---

## 🧾 Step 1: Create a Dockerfile (the **recipe**)

Inside `my-next-app/`, create a file named **`Dockerfile`**:

```Dockerfile
# 1. Use an official Node.js image
FROM node:18-alpine

# 2. Set the working directory in the container
WORKDIR /app

# 3. Copy package.json and install dependencies
COPY package.json package-lock.json ./
RUN npm install

# 4. Copy the rest of the app’s code
COPY . .

# 5. Build the Next.js app
RUN npm run build

# 6. Expose the port Next.js runs on
EXPOSE 3000

# 7. Run the Next.js app
CMD ["npm", "start"]
```

---

## 🖼️ Step 2: Build the Docker **Image**

From the terminal, go to the project directory and run:

```bash
docker build -t my-next-app .
```

- This creates an image called `my-next-app`.
    
- It packages **Node.js**, your **Next.js code**, and all **dependencies**.
    

🧠 You now have a Docker **image** — like a frozen meal, ready to cook.

---

## 📦 Step 3: Run the Docker **Container**

Now launch the app using the image:

```bash
docker run -p 3000:3000 my-next-app
```

- This runs the app **inside a container**
    
- It maps your local port `3000` to the container’s port `3000`
    

🌐 Go to `http://localhost:3000` and you’ll see your Next.js app running!

🧠 The **container** is like a microwave oven that’s cooking and serving your frozen meal (image). When you stop it, the app is gone — but the image remains, ready to be reused.

---

## 🧁 Summary in Cake Terms:

| Concept          | Cake Analogy                | Docker Example              |
| ---------------- | --------------------------- | --------------------------- |
| `Dockerfile`     | Recipe steps                | Instructions to build image |
| Docker Image     | Recipe card (ready to cook) | `my-next-app` image         |
| Docker Container | Cooked meal                 | Running Next.js app         |

---
# Debugging

```bash
doker scout review
```

Gives you all of the bugs and issues
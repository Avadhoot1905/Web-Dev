
[[Node JS]]

## ⚙️ 1. `npm run dev`

> **"Start the app in development mode"**

- Runs: `next dev`
    
- Used while **developing your app**
    
- Enables:
    
    - **Hot reload** (auto reload when you save)
        
    - **Detailed error messages**
        
    - **Faster build times** (not optimized)
        
- **Not optimized for performance**
    
- **Not meant for deployment**
    

🛠 Example: You’re coding your site and want to see changes live.

```bash
npm run dev
```

🌐 Visit: `http://localhost:3000`

---

## 🧱 2. `npm run build`

> **"Build the app for production"**

- Runs: `next build`
    
- **Compiles** and **optimizes** your app:
    
    - Minifies JavaScript
        
    - Pre-renders pages (SSG/SSR)
        
    - Analyzes routes and assets
        
- **Creates a `.next` folder** containing everything needed to run in production.
    

⚠️ This doesn’t start the app — it just prepares it for deployment.

```bash
npm run build
```

📁 Output: a ready-to-deploy `.next` directory.

---

## 🚀 3. `npm start`

> **"Start the production server"**

- Runs: `next start`
    
- Serves the app built with `npm run build`
    
- **Does NOT** support hot reload or development features
    
- Used to serve your app in **production environments**
    

```bash
npm start
```

📝 You must run `npm run build` first, or this will fail.

---

## 💡 Quick Summary Table:

|Command|Purpose|Environment|Hot Reload|Optimized|
|---|---|---|---|---|
|`npm run dev`|Start dev server|Development|✅|❌|
|`npm run build`|Compile & optimize app|Pre-production|❌|✅|
|`npm start`|Run optimized app in production|Production|❌|✅|

---

## 👨‍💻 Real-World Analogy

Let’s say you’re writing a book:

- ✍️ **`npm run dev`** = You’re typing in Google Docs, editing, auto-saving, seeing errors.
    
- 🖨️ **`npm run build`** = You export the final PDF version, formatted and print-ready.
    
- 📦 **`npm start`** = You publish and distribute the PDF to readers.
    

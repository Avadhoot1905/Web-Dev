[[Directory Structure]]
## **1️⃣ Static Routes**

These are simple pages that map directly to a URL.

📂 **Example:**

```
pages/
├── index.js        // Maps to "/"
├── about.js        // Maps to "/about"
├── contact.js      // Maps to "/contact"
```

---

## **2️⃣ Dynamic Routes (`[param]`)**

Used when a part of the URL is **dynamic** (e.g., blog posts, user profiles).

📂 **Example:**

```
pages/
└── blog/
    ├── index.js   // "/blog" (static page)
    ├── [id].js    // "/blog/:id" (dynamic, e.g., "/blog/123")
```

📌 **Usage in Code (`blog/[id].js`):**

```jsx
import { useRouter } from "next/router";

export default function BlogPost() {
  const router = useRouter();
  const { id } = router.query;

  return <h1>Blog Post ID: {id}</h1>;
}
```

**Route Examples:**

- `/blog/1`
- `/blog/nextjs-routing`

---

## **3️⃣ Catch-All Routes (`[...param]`)**

Used when you **don't know** how many segments a URL might have.

📂 **Example:**

```
pages/
└── docs/
    ├── [...slug].js   // Matches "/docs/a", "/docs/a/b", "/docs/a/b/c"
```

📌 **Usage in Code (`docs/[...slug].js`):**

```jsx
import { useRouter } from "next/router";

export default function Docs() {
  const router = useRouter();
  const { slug } = router.query;

  return <h1>Docs Path: {slug ? slug.join("/") : "Home"}</h1>;
}
```

**Route Examples:**

- `/docs/intro`
- `/docs/setup/installation`
- `/docs/setup/configuration/tools`

✅ **Tip:** To match an optional segment, use `[...[slug]]` (prefix with `...`).

---

## **4️⃣ Route Groups (`(folder)`) - App Router Only**

Used to **organize** routes without affecting the URL structure (introduced in Next.js 13 with the App Router).

📂 **Example (App Router `/app` directory):**

```
app/
├── (marketing)/
│   ├── about/page.js   // "/about"
│   ├── pricing/page.js // "/pricing"
├── (dashboard)/
│   ├── settings/page.js // "/settings"
```

📝 **Explanation:**

- The `(marketing)` and `(dashboard)` folders **do not appear in the URL**.
- `about/page.js` maps to `/about`, not `/marketing/about`.

---

## **5️⃣ Layouts (`layout.js`) - App Router Only**

Defines shared UI structure across multiple pages.

📂 **Example:**

```
app/
├── layout.js        // Global layout
├── dashboard/
│   ├── layout.js    // Nested layout for dashboard
│   ├── page.js      // "/dashboard"
│   ├── settings/page.js // "/dashboard/settings"
```

📌 **Usage in Code (`layout.js`):**

```jsx
export default function Layout({ children }) {
  return (
    <div>
      <Navbar />
      {children}
      <Footer />
    </div>
  );
}
```

---

## **6️⃣ API Routes (`/api/*`)**

Used to create backend API endpoints inside Next.js.

📂 **Example:**

```
pages/
└── api/
    ├── hello.js   // API endpoint at "/api/hello"
```

📌 **Usage in Code (`api/hello.js`):**

```jsx
export default function handler(req, res) {
  res.status(200).json({ message: "Hello, API!" });
}
```

✅ **Tip:** You can create dynamic API routes like `/api/user/[id].js`.

---

## **7️⃣ Middleware (`middleware.js`)**

Used to **modify requests before they reach the destination** (e.g., authentication, redirects).

📂 **Example:**

```
middleware.js
```

📌 **Usage in Code (`middleware.js`):**

```jsx
import { NextResponse } from "next/server";

export function middleware(req) {
  const url = req.nextUrl.clone();
  if (!req.cookies.token) {
    url.pathname = "/login";
    return NextResponse.redirect(url);
  }
  return NextResponse.next();
}
```

✅ **Tip:** Middleware runs **before the request** reaches a route.

---

### **Summary Table 📌**

|Syntax|Type|Description|Example Path|
|---|---|---|---|
|`/page.js`|Static|Regular route|`/about`, `/contact`|
|`[id].js`|Dynamic|URL segment as variable|`/blog/123`|
|`[...slug].js`|Catch-All|Matches multiple segments|`/docs/setup/configuration`|
|`(folder)/`|Route Group|Organize routes without affecting URL|`/about` (from `(marketing)/about`)|
|`layout.js`|Layout|Shared UI across pages|Wrapping `dashboard/page.js`|
|`/api/hello.js`|API|Backend API route|`/api/hello`|
|`middleware.js`|Middleware|Runs before requests reach pages|Redirect unauthorized users|


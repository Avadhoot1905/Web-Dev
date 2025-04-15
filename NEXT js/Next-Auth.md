[[TypeScript]]
[[OAuth|OAuth]]
[Tutorial](https://youtu.be/md65iBX5Gxg?si=iORQQBGf5G94aCkR)
[[Prisma]]
[Next-Auth and its relation to Prisma](https://youtu.be/vo2uq1cJV6w?si=GfnJThGYWPkSaSHF)
[Backend chat with ChatGPT](https://chatgpt.com/share/67ab1d6e-bd24-800c-9ec1-047f7787a7a7)
### **1. Install and Set Up NextAuth**

- First, install NextAuth:
    
    ```bash
    npm install next-auth
    ```
    
- Create an **auth configuration** file in `app/api/auth/[...nextauth]/route.js` (or `.ts` for TypeScript).
- Configure NextAuth to use **GitHub authentication**:
    
    ```typescript
    import NextAuth from "next-auth";
    import GitHubProvider from "next-auth/providers/github";
    
    export const authOptions = {
      providers: [
        GitHubProvider({
          clientId: process.env.GITHUB_CLIENT_ID,
          clientSecret: process.env.GITHUB_CLIENT_SECRET,
        }),
      ],
    };
    
    const handler = NextAuth(authOptions);
    export { handler as GET, handler as POST };
    ```
    
- Add **environment variables** in `.env.local`:
    
    ```env
    GITHUB_CLIENT_ID=your_client_id
    GITHUB_CLIENT_SECRET=your_client_secret
    NEXTAUTH_SECRET=your_secret_key
    ```

Generate `NEXTAUTH_SECRET` using:

```bash
openssl rand -base64 32
```

    These ensure that sensitive data isn't exposed in your code.

---

### **2. Create a Login and Logout Button**

- You need buttons to **log in and log out** in your app.
- NextAuth provides a `signIn()` and `signOut()` function that you can use in your UI components:
    
    ```javascript
    "use client";
    import { signIn, signOut, useSession } from "next-auth/react";
    
    export default function AuthButton() {
      const { data: session } = useSession();
    
      if (session) {
        return (
          <div>
            <p>Welcome, {session.user.name}</p>
            <button onClick={() => signOut()}>Log out</button>
          </div>
        );
      }
    
      return <button onClick={() => signIn("github")}>Log in with GitHub</button>;
    }
    ```
    
- This component:
    - **Shows the user’s name if they’re logged in.**
    - **Displays a "Log out" button when authenticated.**
    - **Shows a "Log in with GitHub" button when not authenticated.**

---

### **3. Protecting Pages (Only Allowing Logged-In Users)**

- To make a page accessible **only to logged-in users**, check for authentication before showing content.
- Example in a **server component**:
    
    ```javascript
    import { getServerSession } from "next-auth";
    import { authOptions } from "@/app/api/auth/[...nextauth]/route";
    
    export default async function ProtectedPage() {
      const session = await getServerSession(authOptions);
    
      if (!session) {
        return <p>You need to be logged in to access this page.</p>;
      }
    
      return <p>Welcome, {session.user.name}!</p>;
    }
    ```
    
- If the user **isn’t logged in**, they see a message telling them to log in.
- If they **are logged in**, they can access the page.

---

### **4. Using Server Actions to Get Session Data**

- Sometimes, you need **user session data on the server**.
- You can do this using `getServerSession()`, as shown above.
- This is useful for things like:
    - Customizing the UI for logged-in users.
    - Fetching user-specific data from a database.

---

### **5. Using API Routes with Authentication**

- API routes can also check authentication.
- Example: A protected API route that only allows authenticated users:
    
    ```javascript
    import { getServerSession } from "next-auth";
    import { authOptions } from "@/app/api/auth/[...nextauth]/route";
    import { NextResponse } from "next/server";
    
    export async function GET() {
      const session = await getServerSession(authOptions);
    
      if (!session) {
        return NextResponse.json({ error: "Unauthorized" }, { status: 401 });
      }
    
      return NextResponse.json({ message: "Protected content" });
    }
    ```
    
- If a user **is logged in**, they get the **protected content**.
- If not, they receive an **unauthorized (401) error**.

---

### **6. Fetching API Data on the Client**

- On the frontend, you can fetch this protected API route **only if the user is logged in**:
    
    ```javascript
    "use client";
    import { useSession } from "next-auth/react";
    import { useEffect, useState } from "react";
    
    export default function ProtectedData() {
      const { data: session } = useSession();
      const [data, setData] = useState(null);
    
      useEffect(() => {
        if (session) {
          fetch("/api/protected")
            .then((res) => res.json())
            .then((data) => setData(data.message));
        }
      }, [session]);
    
      if (!session) return <p>Please log in to see protected data.</p>;
    
      return <p>Data: {data}</p>;
    }
    ```
    
- This **fetches protected data** from an API only **if the user is logged in**.

---

### **Summary**

By following these steps, you:  
✅ Install and set up NextAuth with GitHub login.  
✅ Create a login/logout button.  
✅ Protect certain pages so only logged-in users can access them.  
✅ Use server actions to get user session data.  
✅ Secure API routes so only authenticated users can fetch data.

This helps **easily add authentication** to a Next.js app! 🚀
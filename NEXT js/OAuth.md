[[Server side and Client Side]]
[Video Tutorial](https://youtu.be/ot9yuKg15iA?si=aFRnEKuUrHwRvx5U)

## **OAuth for Beginners – A Simple Guide 🚀**

### **1️⃣ What is OAuth & OAuth 2.0?**

OAuth (Open Authorization) is a **secure way for apps to access user data** from another service **without needing passwords**.

🔹 Example: When you **log in to a website using Google or GitHub**, you are using OAuth!

**OAuth 2.0** is the **latest version** of OAuth. It is simpler, more secure, and widely used by services like Google, Facebook, GitHub, etc.

---

### **2️⃣ Why is OAuth Used?**

🔹 **No need to share passwords** – Keeps your login credentials private.  
🔹 **Allows controlled access** – Apps can request only specific permissions (e.g., read-only access to emails).  
🔹 **Works across different platforms** – Websites, mobile apps, smart devices.

🔹 **Real-Life Example:**

1. You visit a website that asks you to **Sign in with Google**.
2. Instead of entering your Google password, the website redirects you to **Google’s login page**.
3. Once you approve, the website gets **temporary access** to your Google account (without knowing your password).

---

### **3️⃣ How is OAuth Different from Other Auth Methods?**

|Method|What It Does|Example|
|---|---|---|
|**Basic Authentication**|Username + Password|Logging into an email account|
|**Session-Based Auth**|Stores login info in cookies|Websites that keep you logged in|
|**Token-Based Auth (OAuth)**|Uses access tokens instead of passwords|"Sign in with Google"|
|**OpenID Connect (OIDC)**|Adds user identity on top of OAuth|Used for logging in (e.g., Google Sign-In)|

✅ **OAuth is for authorization** (granting access to data).  
✅ **OIDC is for authentication** (verifying who you are).

---

### **4️⃣ How OAuth Works – The 4 Simple Steps**

OAuth works by issuing **access tokens** instead of passwords. The process involves 4 key steps:

#### **🔹 Step 1: The App Requests Access**

The website/app asks for permission to access your account.  
✅ Example: "This app wants to read your Google contacts."

#### **🔹 Step 2: The User Approves Access**

You are redirected to the service (e.g., Google), where you log in and approve the request.

#### **🔹 Step 3: The App Gets a Token**

Once approved, the app gets an **access token** (a secret key) from Google.

#### **🔹 Step 4: The App Uses the Token**

The app uses this token to access Google’s API **without needing your password**.

---

### **5️⃣ How is OAuth Implemented? (Simple Example)**

**Example:** Implementing Google OAuth in a Next.js app

#### **Step 1: Install NextAuth.js**

```bash
npm install next-auth
```

#### **Step 2: Create an API Route (`pages/api/auth/[...nextauth].js`)**

```javascript
import NextAuth from "next-auth";
import GoogleProvider from "next-auth/providers/google";

export default NextAuth({
  providers: [
    GoogleProvider({
      clientId: process.env.GOOGLE_CLIENT_ID,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET,
    }),
  ],
});
```

#### **Step 3: Use the Sign-In Button in Your App**

```javascript
import { signIn, signOut, useSession } from "next-auth/react";

export default function AuthButton() {
  const { data: session } = useSession();

  return session ? (
    <button onClick={() => signOut()}>Sign out</button>
  ) : (
    <button onClick={() => signIn("google")}>Sign in with Google</button>
  );
}
```

✅ Now, your app supports **Google login** using OAuth! 🎉

---

### **6️⃣ Summary**

✅ OAuth allows apps to access user data **securely** without passwords.  
✅ OAuth 2.0 uses **access tokens** to grant limited permissions.  
✅ It follows **4 simple steps**: Request → Approve → Get Token → Use Token.  
✅ It's widely used in Google, GitHub, Facebook, and other services.  
✅ Easy to implement in web apps using **NextAuth.js** (Next.js).

Want a step-by-step guide for any specific service (Google, GitHub, etc.)? 🚀

----

##### Origins URL: 

```
http://localhost:3000
```

or a valid deployment url

##### Redirect URL:

```
http://localhost:3000/api/auth/callback/google
```

google can be changed as per use case and requirements
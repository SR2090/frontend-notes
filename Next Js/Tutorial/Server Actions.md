Methods / functions that will execute on server. Can be invoked by both client and server components.
### ✅ What is a **Server Action** in Next.js?

**Server Actions** are a new feature in **Next.js 13+ (with the App Router)** that lets you run **server-side logic directly from a Client Component**, **without manually writing API routes**.

Think of it as:

> 🔁 **Calling a server function from a form or a button, without setting up an API endpoint.**

---

### 🧠 Why It's Useful

- You **write one function**.
    
- That function **runs on the server**.
    
- You can **call it from a Client Component**, and the data stays safe (e.g., DB access, secrets).
    
- It's **typed**, **secure**, and integrates well with **forms** and **mutations**.
    

---

### 📦 Basic Example

#### 1. **Define a Server Action**

```ts
// app/actions/todo.ts
'use server';

import { db } from '@/lib/db';

export async function addTodo(formData: FormData) {
  const title = formData.get('title') as string;
  await db.todo.create({ data: { title } });
}
```

Note:

- The `'use server'` directive tells Next.js: this function should run on the server.
    

---

#### 2. **Use It in a Client Component**

```tsx
// app/page.tsx or any Client Component
import { addTodo } from './actions/todo';

export default function Page() {
  return (
    <form action={addTodo}>
      <input name="title" type="text" />
      <button type="submit">Add Todo</button>
    </form>
  );
}
```

No `fetch`, no `POST`, no `onSubmit` — just form + action.

---

### 🔄 For More Control (Client-Side Trigger)

You can also call Server Actions programmatically:

```tsx
'use client';

import { addTodo } from '@/app/actions/todo';

const AddTodoButton = () => {
  const handleClick = async () => {
    await addTodo(new FormData(document.querySelector('form')!));
  };

  return <button onClick={handleClick}>Add Todo</button>;
};
```

---

### ⚠️ Limitations

- Only works in **App Router** (not Pages Router).
    
- Can’t be used inside `useEffect` or passed to external libraries.
    
- Data passed to Server Actions must be serializable (`FormData`, primitives, etc.).
    

---

### 🔐 Security Benefit

Since Server Actions run **on the server**, your DB queries, tokens, and secrets **never go to the client** — unlike `fetch('/api/xyz')`.

---

### ✅ Use Case Summary

|Use Case|Better with|
|---|---|
|Submitting forms|✅ Server Actions|
|Securely mutating data|✅ Server Actions|
|Fine-grained control|✅ Manual `fetch` with API routes|

---

Would you like me to show you how to convert an existing API call or form submission into a Server Action?
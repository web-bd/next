## ✅ Summary of the Two Approaches

### **Option 1: Server Component (`page.tsx`) + Client Component (`Counter.tsx`)**

```tsx
// page.tsx (Server)
import Counter from './Counter';

export default function Page({ params }: { params: { slug: string } }) {
  return <Counter initialValue={parseInt(params.slug) || 0} />;
}

// Counter.tsx (Client)
'use client';
import { useState } from 'react';

export default function Counter({ initialValue }: { initialValue: number }) {
  const [count, setCount] = useState(initialValue);
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```

✅ **Pros:**

* Leverages **server-side rendering** where possible.
* Keeps **client code minimal** — only interactive logic goes to client.
* Better **performance** (less JavaScript sent to the browser).
* You get the benefit of `params` available directly in server context (no need to `useParams()`).

---

### **Option 2: Entirely Client Component (`page.tsx`)**

```tsx
'use client';

import { useParams } from 'next/navigation';
import { useState } from 'react';

export default function Counter() {
  const params = useParams();
  const [count, setCount] = useState(parseInt(params.slug as string) || 0);
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```

✅ **Pros:**

* Simpler in small apps.
* Dynamic params are available via `useParams()` without prop passing.

❌ **Cons:**

* The entire route is now a **client component**, which:

  * Disables server-side rendering for that page.
  * Increases JavaScript bundle size.
  * Might affect SEO and performance.
* You must handle `useParams()` manually (less efficient than server-rendered `params`).

---

## 🏆 **Recommended Approach**

> ✅ **Use Option 1** — **Server + Client split** — for performance, scalability, and clean architecture.

It follows Next.js best practices:

* Server-first rendering
* Minimal client hydration
* Easier to manage large projects with separation of concerns

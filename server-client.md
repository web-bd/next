## Next.js Code for Server & Client Components
* Server Components (page.tsx) with Client module (Counter.tsx)

```tsx
  // Server Component (e.g., page.tsx)
import Counter from './Counter';

export default function Page({params}: { params: { slug: string } }) {
    return <Counter initialValue={parseInt(params.slug) || 0}/>;
}
```
```tsx
// Client Component (Counter.tsx)
'use client';

import { useState } from 'react';

export default function Counter({ initialValue }: { initialValue: number }) {
    const [count, setCount] = useState(initialValue);
    return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```

* Client Component (page.tsx)
```tsx
'use client'; // 👈 Must be the first line

import {useState} from 'react';
import {useParams} from "next/navigation";

export default function Counter() {

    const params = useParams(); // returns an object

    const [count, setCount] = useState(parseInt(params.slug as string) || 0);
    return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```

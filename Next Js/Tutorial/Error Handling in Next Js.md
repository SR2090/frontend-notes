Error is handled by a special file called error.tsx for a route segment
for /dashboard/invoices we can create an error.tsx file in which all the possible will be handled.
```tsx
'use client';
 
import { useEffect } from 'react';
 
export default function Error({
  error,
  reset,
}: {
  error: Error & { digest?: string };
  reset: () => void;
}) {
  useEffect(() => {
    // Optionally log the error to an error reporting service
    console.error(error);
  }, [error]);
 
  return (
    <main className="flex h-full flex-col items-center justify-center">
      <h2 className="text-center">Something went wrong!</h2>
      <button
        className="mt-4 rounded-md bg-blue-500 px-4 py-2 text-sm text-white transition-colors hover:bg-blue-400"
        onClick={
          // Attempt to recover by trying to re-render the invoices route
          () => reset()
        }
      >
        Try again
      </button>
    </main>
  );
}
```

![[Pasted image 20250503034046.png]]
This reset is provided by next js.
## Not found error
- Uncaught exceptions can be handled using error.tsx
- notfound should be used when the url is not available. The corresponding UI will be defined in the not-found.tsx file

`notFound` will take precedence over `error.tsx`, so you can reach out for it when you want to handle more specific errors!



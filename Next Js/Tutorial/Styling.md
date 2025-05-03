![[Pasted image 20250429194930.png]]

Index:
Styling with tailwind

![[Pasted image 20250429195034.png]]

The global.css file is responsible for styling all the routes. Hence, all the common styles are to be defined in this file. This does not happen automatically we need to go to the layout.tsx present in the UI folder and thenimportthisglobal.css .
![[Pasted image 20250429195358.png]]



### Ways to add styling
1. Using tailwind - install during setup or later, use the classes there will be no collisions
2. CSS Modules
3.  Conditional Styling

## 2. CSS Modules
- Scope css to a component automatically creates unique class name, prevents style collisions.
- ![[Pasted image 20250429202242.png]]
- Usage ![[Pasted image 20250429202639.png]]
- 
- Provide a way to make CSS classes locally scoped to components by default, reducing the risk of styling conflicts.

## 3. Conditional Styling
- clsx Library used for conditional styling
- Usage![[Pasted image 20250429202910.png]]
```tsx
import { CheckIcon, ClockIcon } from '@heroicons/react/24/outline';

import clsx from 'clsx';

  

export default function InvoiceStatus({ status }: { status: string }) {

  return (

    <span

      className={clsx(

        'inline-flex items-center rounded-full px-2 py-1 text-xs',

        {

          'bg-gray-100 text-gray-500': status === 'pending',

          'bg-green-500 text-white': status === 'paid',

        },

      )}

    >

      {status === 'pending' ? (

        <>

          Pending

          <ClockIcon className="ml-1 w-4 text-gray-500" />

        </>

      ) : null}

      {status === 'paid' ? (

        <>

          Paid

          <CheckIcon className="ml-1 w-4 text-white" />

        </>

      ) : null}

    </span>

  );

}
```

## Other ways to apply styling
![[Pasted image 20250429203141.png]]
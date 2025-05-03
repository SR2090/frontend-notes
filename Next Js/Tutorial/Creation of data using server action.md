## Creating an invoice
API Path creation 
![[Pasted image 20250503010848.png]]


## Creating server action file

By adding the `'use server'`, you mark all the exported functions within the file as Server Actions. These server functions can then be imported and used in Client and Server components. Any functions included in this file that are _not_ used will be automatically removed from the final application bundle.

![[Pasted image 20250503013531.png]] #nextlearn

The server action is being called via a post request.

```tsx
<form action={serveraction}></form>

// server action
```

### Server Action
```ts
"use server"

  

export async function createInvoice(formData: FormData) {

    console.log("called")

    const rawFormData = {

        customerId: formData.get('customerId'),

        amount: formData.get('amount'),

        status: formData.get('status'),

      };

      // Test it out:

      console.log(rawFormData);

}
```

![[Pasted image 20250503014209.png]]



### Validating form content using zod

```ts
"use server"

import { z } from "zod"

const FormSchema = z.object({

    id: z.string(),

    customerId: z.string(),

    amount: z.coerce.number(),

    status: z.enum(['pending', 'paid']),

    date: z.string(),

});

  

const CreateInvoice = FormSchema.omit({ id: true, date: true });

export async function createInvoice(formData: FormData) {

    const { customerId, amount, status } = CreateInvoice.parse({

        customerId: formData.get('customerId'),

        amount: formData.get('amount'),

        status: formData.get('status'),

    });

    const amountInCents = amount * 100;

    const date = new Date().toISOString().split('T')[0];

}
```


### Inserting into database from server action
```ts
"use server"

import postgres from 'postgres';

const sql = postgres(process.env.POSTGRES_URL!, { ssl: 'require' });

export async function createInvoice(formData: FormData) {

    await sql`

    INSERT INTO invoices (customer_id, amount, status, date)

    VALUES (${customerId}, ${amountInCents}, ${status}, ${date})

  `;

  

}
```


### Caching
Client side routing ensure that the app is responsive with minimal requests to the server.

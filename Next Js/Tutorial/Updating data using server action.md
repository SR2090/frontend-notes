![[Pasted image 20250503020620.png]]
for this specific scenario


## Accepting dynamic url path
- Accept id of the invoice that we will get from the table item.
- ![[Pasted image 20250503021145.png]]

- Each table has an icon associated with it that can invoke the endpoint![[Pasted image 20250503022617.png]]
- Accessing id inside the server component
```tsx
import Form from '@/app/ui/invoices/edit-form';

import Breadcrumbs from '@/app/ui/invoices/breadcrumbs';

import { fetchInvoiceById, fetchCustomers } from '@/app/lib/data';

export default async function Page(props: { params: Promise<{ id: string }> }) {

    const params = await props.params;

    const id = params.id;

    const [invoice, customers] = await Promise.all([

        fetchInvoiceById(id),

        fetchCustomers(),

      ]);

  return (

    <main>

      <Breadcrumbs

        breadcrumbs={[

          { label: 'Invoices', href: '/dashboard/invoices' },

          {

            label: 'Edit Invoice',

            href: `/dashboard/invoices/${id}/edit`,

            active: true,

          },

        ]}

      />

      <Form invoice={invoice} customers={customers} />

    </main>

  );

}
```


## Passing id to server action

```tsx
const UpdateInvoice = FormSchema.omit({ id: true, date: true });

export async function updateInvoice(id: string, formData: FormData) {

    const { customerId, amount, status } = UpdateInvoice.parse({

        customerId: formData.get('customerId'),

        amount: formData.get('amount'),

        status: formData.get('status'),

    });

  

    const amountInCents = amount * 100;

  

    await sql`

        UPDATE invoices

        SET customer_id = ${customerId}, amount = ${amountInCents}, status = ${status}

        WHERE id = ${id}

      `;

  

    revalidatePath('/dashboard/invoices');

    redirect('/dashboard/invoices');

}
```


### Delete Invoice 
```tsx
export function DeleteInvoice({ id }: { id: string }) {

// this is necessary if the server action is going to accept id
  const deleteInvoiceWithId =  deleteInvoice.bind(null, id);

  return (

    <form action={deleteInvoiceWithId}>

      <button type="submit" className="rounded-md border p-2 hover:bg-gray-100">

        <span className="sr-only">Delete</span>

        <TrashIcon className="w-5" />

      </button>

    </form>

  );

}
```
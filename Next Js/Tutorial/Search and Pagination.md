## Query Parameters Client and Server
![[Pasted image 20250503001328.png]]

Important hooks
1. [[usePathname]]
2. [[useSearchParams]]
3. [[useRouter]]
4. [[URLSearchParams]]

Code on which it will be implemented
```tsx
import Pagination from '@/app/ui/invoices/pagination';
import Search from '@/app/ui/search';
import Table from '@/app/ui/invoices/table';
import { CreateInvoice } from '@/app/ui/invoices/buttons';
import { lusitana } from '@/app/ui/fonts';
import { InvoicesTableSkeleton } from '@/app/ui/skeletons';
import { Suspense } from 'react';
 
export default async function Page() {
  return (
    <div className="w-full">
      <div className="flex w-full items-center justify-between">
        <h1 className={`${lusitana.className} text-2xl`}>Invoices</h1>
      </div>
      <div className="mt-4 flex items-center justify-between gap-2 md:mt-8">
        <Search placeholder="Search invoices..." />
        <CreateInvoice />
      </div>
      {/*  <Suspense key={query + currentPage} fallback={<InvoicesTableSkeleton />}>
        <Table query={query} currentPage={currentPage} />
      </Suspense> */}
      <div className="mt-5 flex w-full justify-center">
        {/* <Pagination totalPages={totalPages} /> */}
      </div>
    </div>
  );
}
```

![[Pasted image 20250502200612.png]]


## Flow of code (Implemenation)
Query key is obtained from the url parameter. 
It is passed onto the URLSearchParams to access that key values. 
This returns us an object whose value we can access. 


Till this point you have the query parameter, and the associated object generated from query params.
useRouter and usePathname can now be used to update the url.

Two way mapping can be done by setting default value in the input field



## Accepting query parameters from server
- Instead of using the hook [[useSearchParams]] we will use the prop.
```tsx
import Pagination from '@/app/ui/invoices/pagination';

import Search from '@/app/ui/search';

import Table from '@/app/ui/invoices/table';

import { CreateInvoice } from '@/app/ui/invoices/buttons';

import { lusitana } from '@/app/ui/fonts';

import { InvoicesTableSkeleton } from '@/app/ui/skeletons';

import { Suspense } from 'react';

export default async function Page(

  props: {

    searchParams?: Promise<{

      query?: string;

      page?: string;

    }>;

  }

) {

  const searchParams = await props.searchParams;

  const query = searchParams?.query || '';

  const currentPage = Number(searchParams?.page) || 1;

  

  return (

    <div className="w-full">

      <div className="flex w-full items-center justify-between">

        <h1 className={`${lusitana.className} text-2xl`}>Invoices</h1>

      </div>

      <div className="mt-4 flex items-center justify-between gap-2 md:mt-8">

        <Search placeholder="Search invoices..." />

        <CreateInvoice />

      </div>

       <Suspense key={query + currentPage} fallback={<InvoicesTableSkeleton />}>

        <Table query={query} currentPage={currentPage} />

      </Suspense>

      <div className="mt-5 flex w-full justify-center">

        {/* <Pagination totalPages={totalPages} /> */}

      </div>

    </div>

  );

}
```

The search component is updating the query url. We want the updates to reach to the table component as well which is why we are using the props on the parent component to read it from url.



# Pagination

The url parameter is going to be updated with a page query and the corresponding value for that page. This updated url is going to query the backend for the data.
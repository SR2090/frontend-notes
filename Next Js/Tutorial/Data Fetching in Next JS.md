1. Creation of database
2. Linking to that data base using env file
3. Just checkout the code in seeding data base Chapter 6 tutorial

## Understanding request water fall #nextjslearn 
```ts
  const revenue = await fetchRevenue();

  const latestInvoices = await fetchLatestInvoices();

  const {

    numberOfCustomers,

    numberOfInvoices,

    totalPaidInvoices,

    totalPendingInvoices,

  } = await fetchCardData()
```

We are making request one after the another. The line gets only executed if the previous has done executing


This is useful in situation where i want to wait for result from previous values and then use it to make new request. Otherwise this will impact performance.


### Solution: Parallel data fetching
#nextjslearn 
Using builtin javascript method such as Promise.all or allSettled.

```ts
    // You can probably combine these into a single SQL query

    // However, we are intentionally splitting them to demonstrate

    // how to initialize multiple queries in parallel with JS.

    const invoiceCountPromise = sql`SELECT COUNT(*) FROM invoices`;

    const customerCountPromise = sql`SELECT COUNT(*) FROM customers`;

    const invoiceStatusPromise = sql`SELECT

         SUM(CASE WHEN status = 'paid' THEN amount ELSE 0 END) AS "paid",

         SUM(CASE WHEN status = 'pending' THEN amount ELSE 0 END) AS "pending"

         FROM invoices`;

  

    const data = await Promise.all([

      invoiceCountPromise,

      customerCountPromise,

      invoiceStatusPromise,

    ]);
```
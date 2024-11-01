const {
  data,
  dataUpdatedAt,
  error,
  errorUpdateCount,
  errorUpdatedAt,
  failureCount,
  failureReason,
  fetchStatus,
  isError,
  isFetched,
  isFetchedAfterMount,
  isFetching,
  isInitialLoading,
  isLoading,
  isLoadingError,
  isPaused,
  isPlaceholderData,
  isPreviousData,
  isRefetchError,
  isRefetching,
  isStale,
  isSuccess,
  refetch,
  remove,
  status,
} = useQuery({
  queryKey,
  queryFn,
  cacheTime,
  enabled,
  networkMode,
  initialData,
  initialDataUpdatedAt,
  keepPreviousData,
  meta,
  notifyOnChangeProps,
  onError,
  onSettled,
  onSuccess,
  placeholderData,
  queryKeyHashFn,
  refetchInterval,
  refetchIntervalInBackground,
  refetchOnMount,
  refetchOnReconnect,
  refetchOnWindowFocus,
  retry,
  retryOnMount,
  retryDelay,
  select,
  staleTime,
  structuralSharing,
  suspense,
  useErrorBoundary,
})

Requries a function that return promise
![[Pasted image 20241010121410.png]]
In this case queryFn will accept the api callout method.


Caching of data
![[Pasted image 20241010121522.png]]
![[Pasted image 20241010121647.png]]
QueryKey is like an identifier that will be obtain the cached data from the api response.


For IsError to work the fetch code should throw an error as mentioned below:![[Pasted image 20241010121922.png]]
There is a refetch function that can be used to resed the query. So, i can make it available on a button click.


To use react query we need to wrap our App with QueryClientProvider.
```js
import {

  Navigate,

  RouterProvider,

  createBrowserRouter,

} from 'react-router-dom';

import { QueryClientProvider, QueryClient } from '@tanstack/react-query';

import Events from './components/Events/Events.jsx';

import EventDetails from './components/Events/EventDetails.jsx';

import NewEvent from './components/Events/NewEvent.jsx';

import EditEvent from './components/Events/EditEvent.jsx';

  

const router = createBrowserRouter([

  {

    path: '/',

    element: <Navigate to="/events" />,

  },

  {

    path: '/events',

    element: <Events />,

  

    children: [

      {

        path: '/events/new',

        element: <NewEvent />,

      },

    ],

  },

  {

    path: '/events/:id',

    element: <EventDetails />,

    children: [

      {

        path: '/events/:id/edit',

        element: <EditEvent />,

      },

    ],

  },

]);

// Configuration object

const queryClient = new QueryClient();

function App() {

  return <QueryClientProvider client={queryClient}>

    <RouterProvider router={router} />

  </QueryClientProvider>;

}

  

export default App;
```


Wrapping Code snippet
```js
const queryClient = new QueryClient();

function App() {

  return <QueryClientProvider client={queryClient}>

    <RouterProvider router={router} />

  </QueryClientProvider>;

}

```


### Caching
By default caching is taking place.
```js
  const { data, isPending, isError, error, refetch } = useQuery({ queryKey: ['fetchEvents'], queryFn: fetchEvents })

```

Each time i come back to page the fetchEvents method is executed. I can however delay its execution for a stipulated time provided by the staleTime key.

```js
  const { data, isPending, isError, error, refetch } = useQuery({ queryKey: ['fetchEvents'], queryFn: fetchEvents, staleTime: 10000 })
```
It means that if a user goes to another page and stays there less than 10 seconds to finally return back to the initial page where this code is written then the fetchEvents won't be executed.

#### How long to keep cache in memory:

```js
 const { data, isPending, isError, error, refetch } = useQuery({ queryKey: ['fetchEvents'], queryFn: fetchEvents, staleTime: 10000, gcTime: 30000 })
```
gcTime: 30000 this make the cache get wiped out by garbage collector after 30 seconds.

If the cache doesn't exist then api will be refetched.


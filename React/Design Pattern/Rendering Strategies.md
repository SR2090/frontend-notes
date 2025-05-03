
The 4 main rendering strategies:
## 1. Server-Side Rendering (SSR)

**What it is**  
On each request, the server builds the HTML by running your React components, then sends that HTML to the client. Hydration on the client “wakes up” the page so React can take over.

**How it works (Next.js example)**

```js
// pages/dashboard.js
export async function getServerSideProps(context) {
  const data = await fetchUserData(context.params.userId)
  return { props: { data } }
}

export default function Dashboard({ data }) {
  return <UserDashboard initialData={data} />
}
```

- **Pros**
    
    - Always-fresh data on every request
        
    - Excellent for dynamic, user-specific content (dashboards, admin panels)
        
    - Great SEO, since crawlers see full HTML
        
- **Cons**
    
    - Higher TTFB (time to first byte)—the server must render on each request
        
    - Can’t cache as aggressively
        

**When to use**

- Personalized pages (user profiles, admin UIs)
    
- SEO-sensitive pages that change on every request
    

---

## 2. Client-Side Rendering (CSR)

**What it is**  
The server sends a mostly empty HTML shell plus your JS bundle. The browser runs the JS, fetches data via API calls, and renders everything in the client.

**How it works (plain React or Next.js fallback)**

```js
// pages/profile.js
export default function Profile() {
  const [user, setUser] = useState(null)
  useEffect(() => {
    fetch('/api/user').then(res => res.json()).then(setUser)
  }, [])
  if (!user) return <LoadingSpinner />
  return <ProfileDetails data={user} />
}
```

- **Pros**
    
    - Super snappy interactions once loaded
        
    - Lower server load (just serves static assets)
        
    - Good DX for very dynamic UIs
        
- **Cons**
    
    - Poorer SEO (content isn’t in initial HTML)
        
    - Slower time-to-interactive on slow networks
        

**When to use**

- Internal apps behind auth (SEO not critical)
    
- Highly interactive dashboards or games where initial load isn’t content-centric
    

---

## 3. Static Site Generation (SSG / “ISG”)

> **Note:** Some docs abbreviate _Incremental Static Generation_ as ISG, but the core idea is build-time generation of HTML.

**What it is**  
All pages are rendered to HTML at build time. The HTML (and JSON data) is deployed to a CDN, so serving is lightning-fast.

**How it works (Next.js)**

```js
// pages/posts/[id].js
export async function getStaticPaths() {
  const posts = await fetchAllPosts()
  return { paths: posts.map(p => ({ params: { id: p.id } })), fallback: false }
}

export async function getStaticProps({ params }) {
  const post = await fetchPost(params.id)
  return { props: { post } }
}

export default function Post({ post }) {
  return <ArticleContent {...post} />
}
```

- **Pros**
    
    - Fastest performance: CDN-served HTML
        
    - Excellent SEO
        
    - Minimal server cost
        
- **Cons**
    
    - Build times grow with number of pages
        
    - Data is frozen at build time—stale until next build
        

**When to use**

- Blog posts, marketing pages, docs—content that changes infrequently
    
- Sites with a finite set of routes you can rebuild nightly or on-demand
    

---

## 4. Incremental Static Regeneration (ISR)

**What it is**  
A hybrid: pages are statically generated at build time, but you can tell Next.js to “re-generate” them on the server in the background after a set interval. The old page stays live until the new one is ready.

**How it works (Next.js)**

```js
export async function getStaticProps() {
  const data = await fetchTrending()
  return {
    props: { data },
    revalidate: 60, // regenerate at most once every 60s
  }
}

export default function Trending({ data }) {
  return <TrendList items={data} />
}
```

- **Pros**
    
    - Combines SSG’s performance with SSR’s freshness
        
    - Automatic background updates—no full rebuilds
        
    - Stale-while-revalidate removes downtime
        
- **Cons**
    
    - Slightly more complex cache invalidation
        
    - “Stale” page until revalidation runs
        

**When to use**

- Content that updates regularly but not every request (e.g. product listings, news feeds)
    
- Large sites where full rebuilds are impractical
    

---

## Quick Comparison

|Strategy|When HTML Generated|Freshness|SEO|Perf (TTFB)|Typical Use Case|
|---|---|---|---|---|---|
|**SSR**|On each request|Always fresh|✅|Medium–High|Dashboards, user-specific pages|
|**CSR**|On client (JS runtime)|Depends on client|⚠️|High (slow FCP)|SPAs, apps behind auth|
|**SSG**|Build time|Frozen until build|✅|Very Low|Blogs, docs, landing pages|
|**ISR**|Build time + on interval|Near-fresh|✅|Very Low|Catalogs, changing content w/o rebuild|

---

### Choosing the Right One

1. **SEO & initial load matter?**  
    – Go SSG or ISR for best performance.  
    – Use SSR if data truly must be fresh per request.
    
2. **Highly interactive, logged-in UI?**  
    – CSR or SSR (if you need SEO).  
    – CSR alone if SEO isn’t a concern.
    
3. **Content updates frequently but not per request?**  
    – ISR gives you static speed with periodic updates.
    
4. **Build time too long?**  
    – ISR lets you avoid full rebuilds by re-generating only stale pages.
    



### Extras
[Cumulative Layout Shift](https://vercel.com/blog/how-core-web-vitals-affect-seo)
9

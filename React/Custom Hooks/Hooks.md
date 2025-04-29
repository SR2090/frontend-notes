React **hooks must always be called at the top level** of a component — you **cannot call hooks conditionally or inside functions like `handleSubmit`**.

---

### ✅ Solution: Move the hook's `url` dependency based on button click

You can control the hook’s behavior by changing the `url` **only when the user clicks the button**.

### Here's how you can do it:

#### 1. Move the `url` to a state variable.

#### 2. Update the `url` in `handleSubmit` to trigger the `useFetch` call.

```js
import { useEffect, useState } from "react";
import useFetch from "./customHook/useFetch"; // no curly braces if default export

function App() {
  const [value, setValue] = useState("");
  const [fetchUrl, setFetchUrl] = useState(null); // url to trigger fetch

  const { data, loading, error } = useFetch(fetchUrl); // fetch only when fetchUrl is set

  const handleSubmit = () => {
    if (value.trim() !== "") {
      setFetchUrl(`https://dummyjson.com/recipes/search?q=${value}`);
    }
  };

  return (
    <div>
      <div style={{ display: "flex", gap: "10px" }}>
        <input value={value} onChange={(e) => setValue(e.target.value)} />
        <button onClick={handleSubmit}>Fetch Data</button>
      </div>
      <div>
        {loading && <p>Loading...</p>}
        {error && <p>{error}</p>}
        {data && (
          <pre>{JSON.stringify(data, null, 2)}</pre>
        )}
      </div>
    </div>
  );
}

export default App;
```

---

### 🔁 In your custom hook (`useFetch`), make sure to handle `null` or empty `url`:

```js
useEffect(() => {
  if (!url) return; // skip if url is null or undefined

  const fetchData = async () => {
    setLoading(true);
    try {
      const response = await fetch(url);
      if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);
      const data = await response.json();
      setData(data);
    } catch (e) {
      setError("API has failed: " + e.message);
    } finally {
      setLoading(false);
    }
  };

  fetchData();
}, [url]);
```


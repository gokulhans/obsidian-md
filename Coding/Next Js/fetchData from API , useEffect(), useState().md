
## Fetch from Client side

```js
"use client";

import { useState, useEffect } from "react";

const Home = () => {

  const [posts, setPosts] = useState([]);
  
  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await fetch(
          "https://jsonplaceholder.typicode.com/posts"
        );
        const data = await response.json();
        setPosts(data);
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    };
    fetchData();
  }, []);

  return (
    <div>
      <ul>
        {posts.map((post) => (
          <li className="border m-3 py-2 px-4 rounded" key={post.id}>{post.title}</li>
        ))}
      </ul>
    </div>
  );
};

export default Home;
```

## Fetch from Server side

```js
const fetchData = async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/posts");
    const data = await response.json();
    return data;
  } catch (error) {
    console.error("Error fetching data:", error);
  }
};

const Home = async () => {
  let posts = await fetchData();
  console.log(posts[0]);
  return (
    <div>
      <ul>
        {posts.map((post) => (
          <li key={post.id}> {post.title </li>
        ))}
      </ul>
    </div>
  );
};

export default Home;
```


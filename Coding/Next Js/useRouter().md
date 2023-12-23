
**How to Navigate Between Pages**

```js
"use client";
import Link from "next/link";
import React from "react";
import { useRouter } from "next/navigation";

const Navbar = () => {
  const router = useRouter();
  return (
    <>
      <nav>
        Navbar
        <div>
          <Link href="/">Home</Link>
          <button onClick={()=>router.push("users")}>Users</button>
          <Link href="users/about">About</Link>
        </div>
      </nav>
    </>
  );
};
export default Navbar;
```




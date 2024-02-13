
Edit App.jsx

```js
<Route path="/view" element={<View isUser={isUser} />} />
```

Create pages/View/View.jsx

```js
import React, { useEffect, useState } from "react";
import { useQuery } from "@tanstack/react-query";
import axiosClient from "@/util/axios";

const View = () => {
  const fetchExamples = async () => {
    const token = localStorage.getItem("token"); // Retrieve the JWT token from localStorage
    const headers = {
      Authorization: `Bearer ${token}`, // Include the token in the Authorization header
    };
    const response = await axiosClient.get("/example", { headers });
    return response.data.data;
  };

  const {
    data: examples,
    isLoading,
    isError,
    error,
  } = useQuery({
    queryKey: ["examples"],
    queryFn: fetchExamples,
  });

  if (isLoading) {
    return (
      <>
        <div className="w-full max-w-3xl sm:pt-8 p-4 pt-6 sm:px-0">Loading</div>
      </>
    );
  }

  if (isError) {
    return <div>Error: {error.message}</div>;
  }

  return (
    <>
      <div className="flex align-center justify-self-center w-full">
        {examples.map((example) => (
          <div key={example._id}>
            <h1>
              {example.name} <br />
            </h1>
          </div>
        ))}
      </div>
    </>
  );
};

export default View;
```

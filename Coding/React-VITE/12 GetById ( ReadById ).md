
Edit App.jsx File

```jsx
<Route path="/view/:id" element={<ViewOne isUser={isUser} />} />
```

Create pages/ViewOne/ViewOne.jsx

```jsx
import React, { useEffect, useState } from "react";
import { useQuery } from "@tanstack/react-query";
import axiosClient from "@/util/axios";
import { useParams } from "react-router-dom";

const ViewOne = () => {
  const { id } = useParams();

  const fetchExample = async () => {
    const token = localStorage.getItem("token"); // Retrieve the JWT token from localStorage
    const headers = {
      Authorization: `Bearer ${token}`, // Include the token in the Authorization header
    };
    const response = await axiosClient.get(`/example/${id}`, { headers });
    return response.data.data;
  };

  const {
    data: example,
    isLoading,
    isError,
    error,
  } = useQuery({
    queryKey: ["example", id],
    queryFn: fetchExample,
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
      <div className="flex align-center justify-center w-full">
        {example.name}
      </div>
    </>
  );
};

export default ViewOne;
```
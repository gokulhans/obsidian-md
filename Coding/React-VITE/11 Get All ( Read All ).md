Edit App.jsx

```jsx
<Route path="/view" element={<View isUser={isUser} />} />
```

Create pages/View/View.jsx

```jsx
import React, { useEffect, useState } from "react";
import { useQuery, useQueryClient, useMutation } from "@tanstack/react-query";
import axiosClient from "@/util/axios";
import toast from "react-hot-toast";

const View = () => {
  const queryClient = useQueryClient();

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

  const { mutateAsync } = useMutation({
    mutationFn: (id) => {
      const token = localStorage.getItem("token");
      const headers = {
        Authorization: `Bearer ${token}`,
      };
      return axiosClient.delete(`/example/${id}`, { headers });
    },
    onSuccess: () => {
      // Invalidate and refetch queries related to the updated data
      toast.success("Deleted Successfully!");
      queryClient.invalidateQueries("examples");
    },
  });

  const handleDelete = async (id) => {
    const isConfirmed = window.confirm("Are you sure you want to delete ?");
    if (isConfirmed) {
      mutateAsync(id);
    }
  };

  if (isLoading) {
    return (
      <>
        <div className="w-full max-w-3xl sm:pt-8 p-4 pt-6 sm:px-0 flex justify-center">
          Loading
        </div>
      </>
    );
  }

  if (isError) {
    return <div>Error: {error.message}</div>;
  }

  return (
    <>
      <div className="flex align-center justify-center w-full">
        {examples.length != 0 ? (
          examples.map((example) => (
            <div key={example._id} className="block m-5">
              <h1>
                {example.name} <br />
              </h1>
              <button
                className="text-red-700"
                onClick={() => handleDelete(example._id)}
              >
                Delete
              </button>
            </div>
          ))
        ) : (
          <div className="w-full max-w-3xl sm:pt-8 p-4 pt-6 sm:px-0 flex justify-center">
            No Data Found
          </div>
        )}
      </div>
    </>
  );
};

export default View;
```

Edit App.jsx

```js
<Route path="/edit/:id" element={<Edit isUser={isUser} />} />
```

Create pages/edit/edit.jsx

```js
import React, { useState, useEffect } from "react";
import { useForm } from "react-hook-form";
import * as yup from "yup";
import { yupResolver } from "@hookform/resolvers/yup";
import { useMutation, useQuery, useQueryClient } from "@tanstack/react-query";
import { useNavigate, useParams } from "react-router-dom";
import toast from "react-hot-toast";
import axiosClient from "@/util/axios";

const Edit = () => {
  const { id } = useParams();
  const navigate = useNavigate();
  const queryClient = useQueryClient();

  const [isLoading, setIsLoading] = useState(false);
  const [showError, setShowError] = useState(null);

  const schema = yup.object().shape({
    name: yup.string().required(),
  });

  const {
    register,
    handleSubmit,
    formState: { errors },
    setValue,
  } = useForm({
    resolver: yupResolver(schema),
  });

  const fetchExample = async () => {
    const token = localStorage.getItem("token"); // Retrieve the JWT token from localStorage
    const headers = {
      Authorization: `Bearer ${token}`, // Include the token in the Authorization header
    };
    const response = await axiosClient.get(`/example/${id}`, { headers });
    return response.data;
  };

  const postExample = async (data) => {
    const token = localStorage.getItem("token"); // Retrieve the JWT token from localStorage
    const headers = {
      Authorization: `Bearer ${token}`, // Include the token in the Authorization header
    };
    return axiosClient.put(`/example/${id}`, data, { headers });
  };

  const { data: exampleData } = useQuery({
    queryKey: ["example", id],
    queryFn: fetchExample,
  });

  useEffect(() => {
    if (exampleData) {
      setValue("name", exampleData.data.name);
    }
  }, [exampleData, setValue]);

  const { mutateAsync } = useMutation({
    mutationFn: (data) => {
      postExample(data);
    },
    onSuccess: (data) => {
      navigate("/");
      toast.success("Data Updated Successfully!");
      queryClient.refetchQueries(["example", id]); // Refetch the query after successful update
    },
    onError: (error) => {
      setShowError(error.response.data.error);
      setIsLoading(false);
    },
  });

  const onSubmit = (data) => {
    setIsLoading(true);
    mutateAsync(data);
  };

  return (
    <main className="w-full max-w-md mx-auto p-6">
      <div className="mt-7 bg-white border border-gray-200 rounded-xl shadow-sm dark:bg-gray-900 dark:border-gray-700">
        <div className="p-4 sm:p-7">
          <div className="text-center">
            <h1 className="block text-2xl font-bold text-gray-900 dark:text-white">
              Update Data
            </h1>
          </div>
          <div className="mt-5">
            {/* Form */}
            <form onSubmit={handleSubmit(onSubmit)}>
              <div className="grid gap-y-4">
                {/* Form Group */}
                <div>
                  <label
                    htmlFor="name"
                    className="block text-sm mb-2 dark:text-white"
                  >
                    Name
                  </label>
                  <div className="relative">
                    <input
                      type="text"
                      id="name"
                      name="name"
                      className="border py-3 px-4 block w-full border-gray-200 rounded-md text-sm focus:border-blue-500 focus:ring-blue-500 dark:bg-gray-900 dark:border-gray-700 dark:text-gray-400"
                      {...register("name")}
                    />
                  </div>
                  <p className="text-xs text-red-600 dark:text-red-500 mt-2">
                    {errors.name?.message}
                  </p>
                </div>
                {/* End Form Group */}

                <input
                  type="submit"
                  value={isLoading ? "Loading.." : "Submit"}
                  disabled={isLoading}
                  className="cursor-pointer py-3 px-4 inline-flex justify-center items-center gap-2 rounded-md border border-transparent font-semibold bg-blue-500 text-white hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2 transition-all text-sm dark:focus:ring-offset-gray-900"
                />
                {showError && (
                  <p className="text-xs text-red-600 dark:text-red-500 mt-2">
                    {showError}
                  </p>
                )}
              </div>
            </form>
            {/* End Form */}
          </div>
        </div>
      </div>
    </main>
  );
};

export default Edit;
```


Chat GPT

```
create an edit product page

<<< PASTE ADD PRODUCT >>>

SYNTAX

import React, { useState, useEffect } from "react";
import { useForm } from "react-hook-form";
import * as yup from "yup";
import { yupResolver } from "@hookform/resolvers/yup";
import { useMutation, useQuery, useQueryClient } from "@tanstack/react-query";
import { useNavigate, useParams } from "react-router-dom";
import toast from "react-hot-toast";
import axiosClient from "@/util/axios";
import { Button } from "@/components/ui/button";

const EditCategory = () => {
  const { id } = useParams();
  const navigate = useNavigate();
  const queryClient = useQueryClient();

  const [isLoading, setIsLoading] = useState(false);
  const [showError, setShowError] = useState(null);

  const schema = yup.object().shape({
    categoryname: yup.string().required(),
  });

  const {
    register,
    handleSubmit,
    formState: { errors },
    setValue,
  } = useForm({
    resolver: yupResolver(schema),
  });

  const fetchCategory = async () => {
    const token = localStorage.getItem("token"); // Retrieve the JWT token from localStorage
    const headers = {
      Authorization: `Bearer ${token}`, // Include the token in the Authorization header
    };
    const response = await axiosClient.get(`/category/${id}`, { headers });
    return response.data;
  };

  const updateCategory = async (data) => {
    const token = localStorage.getItem("token"); // Retrieve the JWT token from localStorage
    const headers = {
      Authorization: `Bearer ${token}`, // Include the token in the Authorization header
    };
    return axiosClient.put(`/category/${id}`, data, { headers });
  };

  const { data: categoryData } = useQuery({
    queryKey: ["category", id],
    queryFn: fetchCategory,
  });

  useEffect(() => {
    if (categoryData) {
      setValue("categoryname", categoryData.data.categoryname);
    }
  }, [categoryData, setValue]);

  const { mutateAsync } = useMutation({
    mutationFn: (data) => {
      updateCategory(data);
    },
    onSuccess: (data) => {
      navigate("/");
      toast.success("Category Updated Successfully!");
      queryClient.refetchQueries(["category", id]); // Refetch the query after successful update
    },
    onError: (error) => {
      setShowError(error.response.data.error);
      setIsLoading(false);
    },
  });

  const onSubmit = (data) => {
    setIsLoading(true);
    mutateAsync(data);
  };

  return (
    <main className="w-full max-w-md mx-auto p-6">
      <div className="mt-7 bg-white border border-gray-200 rounded-xl shadow-sm dark:bg-gray-900 dark:border-gray-700">
        <div className="p-4 sm:p-7">
          <div className="text-center">
            <h1 className="block text-2xl font-bold text-gray-900 dark:text-white">
              Edit Category
            </h1>
          </div>
          <div className="mt-5">
            {/* Form */}
            <form onSubmit={handleSubmit(onSubmit)}>
              <div className="grid gap-y-4">
                {/* Form Group */}
                <div>
                  <label
                    htmlFor="categoryname"
                    className="block text-sm mb-2 dark:text-white"
                  >
                    Category Name
                  </label>
                  <div className="relative">
                    <input
                      type="text"
                      id="categoryname"
                      name="categoryname"
                      className="border py-3 px-4 block w-full border-gray-200 rounded-md text-sm focus:border-blue-500 focus:ring-blue-500 dark:bg-gray-900 dark:border-gray-700 dark:text-gray-400"
                      {...register("categoryname")}
                    />
                  </div>
                  <p className="text-xs text-red-600 dark:text-red-500 mt-2">
                    {errors.categoryname?.message}
                  </p>
                </div>
                {/* End Form Group */}

                <Button type="submit" disabled={isLoading}>
                  {isLoading ? "Loading.." : "Submit"}
                </Button>
                {showError && (
                  <p className="text-xs text-red-600 dark:text-red-500 mt-2">
                    {showError}
                  </p>
                )}
              </div>
            </form>
            {/* End Form */}
          </div>
        </div>
      </div>
    </main>
  );
};

export default EditCategory;
```
Edit App.jsx

```js
<Route path="/create" element={<PostData isUser={isUser} />} />
```

Post Form

```jsx
import React, { useState } from "react";
import { useForm } from "react-hook-form";
import * as yup from "yup";
import { yupResolver } from "@hookform/resolvers/yup";
import { useMutation } from "@tanstack/react-query";
import { useNavigate } from "react-router-dom";
import toast from "react-hot-toast";
import axiosClient from "@/util/axios";

const Create = () => {
  const [isLoading, setIsLoading] = useState(false);
  const [showError, setShowError] = useState(null);
  const navigate = useNavigate();

  const schema = yup.object().shape({
    name: yup.string().required(),
  });

  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm({
    resolver: yupResolver(schema),
  });

  const postExample = async (data) => {
    const token = localStorage.getItem("token"); // Retrieve the JWT token from localStorage
    const headers = {
      Authorization: `Bearer ${token}`, // Include the token in the Authorization header
    };
    return axiosClient.post("/example/", data, { headers });
  };

  const { mutateAsync } = useMutation({
    mutationFn: (data) => {
      postExample(data);
    },
    onSuccess: (data) => {
      navigate("/");
      toast.success("Data Added Successfully!");
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
              Add Data
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

export default Create;

```

```jsx
  const queryClient = useQueryClient();

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
```


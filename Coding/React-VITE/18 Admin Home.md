
src/Admin/AdminHome/AdminHome.jsx

```jsx
import React, { useState } from "react";
import { Link } from "react-router-dom";
import { Button } from "@/components/ui/button";
import AdminProducts from "../AdminProducts/AdminProducts";
import AdminUsers from "../AdminUsers/AdminUsers";

const AdminHome = () => {
  const [currentComponent, setCurrentComponent] = useState("products");

  const handleNavigation = (component) => {
    setCurrentComponent(component);
  };

  return (
    <div className="grid min-h-screen w-full bg-gray-100/40 lg:grid-cols-[200px_1fr] dark:bg-gray-800/40">
      <div className="hidden border-r dark:border-gray-700 bg-gray-100/40 lg:block dark:bg-gray-800/40">
        <div className="flex h-full max-h-screen flex-col gap-2">
          <div className="flex h-[60px] items-center border-b dark:border-gray-700 px-6">
            <Link className="flex items-center gap-2 font-semibold" href="#">
              {/* <Package2Icon className="h-6 w-6" /> */}
              <span className="">Admin</span>
            </Link>
            <Button className="ml-auto h-8 w-8" size="icon" variant="outline">
              <BellIcon className="h-4 w-4" />
              <span className="sr-only">Toggle notifications</span>
            </Button>
          </div>
          <div className="flex-1 overflow-auto py-2">
            <nav className="grid items-start px-4 text-sm font-medium">
              <button
                className={`flex items-center gap-3 rounded-lg px-3 py-2 border-2 my-1 dark:border-gray-700  ${
                  currentComponent === "products"
                    ? "bg-gray-100 dark:bg-gray-700 text-gray-900 border-gray-700 dark:border-gray-600 "
                    : "text-gray-900"
                } transition-all hover:text-gray-900 dark:text-gray-400 dark:hover:text-gray-50`}
                onClick={() => handleNavigation("products")}
              >
                Products
              </button>
              <button
                className={`flex items-center gap-3 rounded-lg px-3 py-2 border-2 my-1 dark:border-gray-700  ${
                  currentComponent === "users"
                    ? "bg-gray-100 dark:bg-gray-700 text-gray-900 border-gray-700 dark:border-gray-600 "
                    : "text-gray-900"
                } transition-all hover:text-gray-900 dark:text-gray-400 dark:hover:text-gray-50`}
                onClick={() => handleNavigation("users")}
              >
                Users
              </button>
              {/* Add more buttons for additional sections as needed */}
            </nav>
          </div>
        </div>
      </div>
      <div className="flex flex-col">
        {currentComponent === "products" && <AdminProducts />}
        {currentComponent === "users" && <AdminUsers />}
      </div>
    </div>
  );
};

export default AdminHome;

function BellIcon(props) {
  return (
    <svg
      {...props}
      xmlns="http://www.w3.org/2000/svg"
      width="24"
      height="24"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      strokeWidth="2"
      strokeLinecap="round"
      strokeLinejoin="round"
    >
      <path d="M6 8a6 6 0 0 1 12 0c0 7 3 9 3 9H3s3-2 3-9" />
      <path d="M10.3 21a1.94 1.94 0 0 0 3.4 0" />
    </svg>
  );
}

function HomeIcon(props) {
  return (
    <svg
      {...props}
      xmlns="http://www.w3.org/2000/svg"
      width="24"
      height="24"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      strokeWidth="2"
      strokeLinecap="round"
      strokeLinejoin="round"
    >
      <path d="m3 9 9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z" />
      <polyline points="9 22 9 12 15 12 15 22" />
    </svg>
  );
}

function LineChartIcon(props) {
  return (
    <svg
      {...props}
      xmlns="http://www.w3.org/2000/svg"
      width="24"
      height="24"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      strokeWidth="2"
      strokeLinecap="round"
      strokeLinejoin="round"
    >
      <path d="M3 3v18h18" />
      <path d="m19 9-5 5-4-4-3 3" />
    </svg>
  );
}

function Package2Icon(props) {
  return (
    <svg
      {...props}
      xmlns="http://www.w3.org/2000/svg"
      width="24"
      height="24"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      strokeWidth="2"
      strokeLinecap="round"
      strokeLinejoin="round"
    >
      <path d="M3 9h18v10a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V9Z" />
      <path d="m3 9 2.45-4.9A2 2 0 0 1 7.24 3h9.52a2 2 0 0 1 1.8 1.1L21 9" />
      <path d="M12 3v6" />
    </svg>
  );
}

function PackageIcon(props) {
  return (
    <svg
      {...props}
      xmlns="http://www.w3.org/2000/svg"
      width="24"
      height="24"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      strokeWidth="2"
      strokeLinecap="round"
      strokeLinejoin="round"
    >
      <path d="m7.5 4.27 9 5.15" />
      <path d="M21 8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16Z" />
      <path d="m3.3 7 8.7 5 8.7-5" />
      <path d="M12 22V12" />
    </svg>
  );
}

function ShoppingCartIcon(props) {
  return (
    <svg
      {...props}
      xmlns="http://www.w3.org/2000/svg"
      width="24"
      height="24"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      strokeWidth="2"
      strokeLinecap="round"
      strokeLinejoin="round"
    >
      <circle cx="8" cy="21" r="1" />
      <circle cx="19" cy="21" r="1" />
      <path d="M2.05 2.05h2l2.66 12.42a2 2 0 0 0 2 1.58h9.78a2 2 0 0 0 1.95-1.57l1.65-7.43H5.12" />
    </svg>
  );
}

function UsersIcon(props) {
  return (
    <svg
      {...props}
      xmlns="http://www.w3.org/2000/svg"
      width="24"
      height="24"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      strokeWidth="2"
      strokeLinecap="round"
      strokeLinejoin="round"
    >
      <path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2" />
      <circle cx="9" cy="7" r="4" />
      <path d="M22 21v-2a4 4 0 0 0-3-3.87" />
      <path d="M16 3.13a4 4 0 0 1 0 7.75" />
    </svg>
  );
}
```

Create File src/Admin/AdminProducts/AdminProducts.jsx.

```jsx
import React, { useState, useEffect } from "react";
import {
  TableHead,
  TableRow,
  TableHeader,
  TableCell,
  TableBody,
  Table,
} from "@/components/ui/table";
import { Button } from "@/components/ui/button";
import { Link } from "react-router-dom";
import axiosClient from "@/util/axios";

const AdminProducts = () => {
  const [bins, setBins] = useState([]);

  useEffect(() => {
    axiosClient
      .get("/bin")
      .then((response) => {
        setBins(response.data.data);
        console.log(response); // Assuming the response.data contains an array of bin objects
      })
      .catch((error) => {
        console.error("Error fetching bins:", error);
      });
  }, []);

  return (
    <>
      <header className="flex h-14 lg:h-[60px] items-center gap-4 border-b dark:border-gray-700 bg-gray-100/40 px-6 dark:bg-gray-800/40">
        <Link className="lg:hidden" to="#">
          {/* Assuming you have a suitable icon for the home link */}
          <Package2Icon className="h-6 w-6" />
          <span className="sr-only">Home</span>
        </Link>
        <div className="flex-1">
          <h1 className="font-semibold text-lg">Products</h1>
        </div>
        <Button size="sm">
          <Link to="/new-bin">New Bin</Link>
        </Button>
      </header>
      <main className="flex flex-1 flex-col gap-4 p-4 md:gap-8 md:p-6">
        <div className="border-2 dark:border-gray-700 rounded-lg">
          <Table>
            <TableHeader>
              <TableRow>
                <TableHead className="w-[100px]">Bin</TableHead>
                <TableHead className="min-w-[150px]">Location</TableHead>
                <TableHead className="hidden md:table-cell">Pin Code</TableHead>
                <TableHead className="hidden md:table-cell">District</TableHead>
                <TableHead className="hidden md:table-cell">Status</TableHead>
                {/* <TableHead className="text-right">Action</TableHead> */}
              </TableRow>
            </TableHeader>
            <TableBody>
              {bins.map((bin, index) => (
                <TableRow key={index}>
                  <TableCell className="font-medium">{index + 1}</TableCell>
                  <TableCell>{bin.location}</TableCell>
                  <TableCell className="hidden md:table-cell">
                    {bin.pincode}
                  </TableCell>
                  <TableCell className="hidden md:table-cell">
                    {bin.district}
                  </TableCell>
                  <TableCell className="hidden md:table-cell">
                    {bin.isFilled ? (
                      <>
                        <h1 className="text-red-700">Filled</h1>
                      </>
                    ) : (
                      <>
                        <h1 className="text-green-700">Not Filled</h1>{" "}
                      </>
                    )}
                  </TableCell>
                  {/* <TableCell className="text-right">
                    <Button size="icon" variant="ghost">
                      <FileEditIcon className="w-4 h-4" />
                      <span className="sr-only">Edit</span>
                    </Button>
                  </TableCell> */}
                </TableRow>
              ))}
            </TableBody>
          </Table>
        </div>
      </main>
    </>
  );
};

export default AdminProducts;

function FileEditIcon(props) {
  return (
    <svg
      {...props}
      xmlns="http://www.w3.org/2000/svg"
      width="24"
      height="24"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      strokeWidth="2"
      strokeLinecap="round"
      strokeLinejoin="round"
    >
      <path d="M4 13.5V4a2 2 0 0 1 2-2h8.5L20 7.5V20a2 2 0 0 1-2 2h-5.5" />
      <polyline points="14 2 14 8 20 8" />
      <path d="M10.42 12.61a2.1 2.1 0 1 1 2.97 2.97L7.95 21 4 22l.99-3.95 5.43-5.44Z" />
    </svg>
  );
}

function Package2Icon(props) {
  return (
    <svg
      {...props}
      xmlns="http://www.w3.org/2000/svg"
      width="24"
      height="24"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      strokeWidth="2"
      strokeLinecap="round"
      strokeLinejoin="round"
    >
      <path d="M3 9h18v10a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V9Z" />
      <path d="m3 9 2.45-4.9A2 2 0 0 1 7.24 3h9.52a2 2 0 0 1 1.8 1.1L21 9" />
      <path d="M12 3v6" />
    </svg>
  );
}
```


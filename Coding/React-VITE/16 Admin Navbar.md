AdminNavbar.jsx

```jsx
import React, { useState } from "react";
import { Link } from "react-router-dom";
import { Input } from "../ui/input";
import { Button } from "../ui/button";
import { Avatar, AvatarFallback, AvatarImage } from "../ui/avatar";
import DarkModeToggler from "../DarkModeToggler/DarkModeToggler";
import { SearchIcon } from "lucide-react";
import AdminLogoutButton from "../LogoutButton/AdminLogoutButton";

const AdminNavbar = ({ isAdmin, setIsAdmin }) => {
  return (
    <>
      <header className="fixed top-0 left-0 flex h-16 w-full shrink-0 items-center px-4 md:px-6 z-50 bg-blue-50 dark:bg-gray-900">
        <Link className="mr-6 flex items-center" to={"/"}>
          <RecycleIcon className="h-6 w-6 text-green-500" />
          <span className="ml-2 text-lg font-semibold">
            <b>EcoTrove</b>
          </span>
        </Link>
        <div className="ml-auto flex gap-2">
          {!isAdmin ? (
            <>
              <Link to={"/signin"}>
                <Button variant="outline">Sign in</Button>
              </Link>
              <Link to={"/signup"}>
                <Button>Sign Up</Button>
              </Link>
            </>
          ) : (
            <>
              <div className="">
                <form className="relative">
                  <SearchIcon className="absolute left-2.5 top-2.5 h-4 w-4 text-gray-500 dark:text-gray-400" />
                  <Input
                    className="pl-8"
                    id="search"
                    placeholder="Search..."
                    type="search"
                  />
                </form>
              </div>
              {/* <Avatar className="h-9 w-9">
                <AvatarImage alt="User Avatar" src="/placeholder-avatar.jpg" />
                <AvatarFallback>
                  <b>
                    {localStorage.getItem("username") &&
                      localStorage.getItem("username").charAt(0).toUpperCase()}
                  </b>
                </AvatarFallback>
              </Avatar> */}
              <AdminLogoutButton setIsAdmin={setIsAdmin} />
            </>
          )}
          <DarkModeToggler />
        </div>
      </header>
    </>
  );
};

export default AdminNavbar;

function MountainIcon(props) {
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
      <path d="m8 3 4 8 5-5 5 15H2L8 3z" />
    </svg>
  );
}
function RecycleIcon(props) {
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
      <path d="M7 19H4.815a1.83 1.83 0 0 1-1.57-.881 1.785 1.785 0 0 1-.004-1.784L7.196 9.5" />
      <path d="M11 19h8.203a1.83 1.83 0 0 0 1.556-.89 1.784 1.784 0 0 0 0-1.775l-1.226-2.12" />
      <path d="m14 16-3 3 3 3" />
      <path d="M8.293 13.596 7.196 9.5 3.1 10.598" />
      <path d="m9.344 5.811 1.093-1.892A1.83 1.83 0 0 1 11.985 3a1.784 1.784 0 0 1 1.546.888l3.943 6.843" />
      <path d="m13.378 9.633 4.096 1.098 1.097-4.096" />
    </svg>
  );
}
```

Create src/components/AdminLogoutButton/AdminLogoutButton.jsx

```jsx
import React from "react";
import { useNavigate } from "react-router-dom";
import toast from "react-hot-toast";

const AdminLogoutButton = ({ setIsAdmin }) => {
  const navigate = useNavigate();
  const handleLogout = () => {
    localStorage.clear();
    setIsAdmin(false);
    toast.success("Logout Successfully!");
    navigate("/");
  };

  return (
    <button
      onClick={handleLogout}
      className="group inline-flex flex-shrink-0 justify-center items-center h-9 w-9 font-medium rounded-full text-gray-800 hover:bg-gray-100 dark:text-gray-200 dark:hover:bg-gray-800"
    >
      <svg
        className="h-4 w-4"
        xmlns="http://www.w3.org/2000/svg"
        width="16"
        height="16"
        viewBox="0 0 24 24"
        fill="none"
        stroke="currentColor"
        strokeWidth="2"
        strokeLinecap="round"
        strokeLinejoin="round"
      >
        <path d="M9 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h4" />
        <polyline points="16 17 21 12 16 7" />
        <line x1="21" x2="9" y1="12" y2="12" />
      </svg>
    </button>
  );
};

export default AdminLogoutButton;

```





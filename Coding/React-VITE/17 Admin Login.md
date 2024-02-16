Add these in App.jsx

```jsx
{
  isAdmin ? (
    <>
      <AdminNavbar isAdmin={isAdmin} setIsAdmin={setIsAdmin} />
    </>
  ) : (
    <>
      <Navbar isUser={isUser} setIsUser={setIsUser} />
    </>
  );
}
```

Create Admin/AdminLogin/AdminLogin.jsx

```jsx
import React, { useState } from "react";
import { useNavigate } from "react-router-dom"; // Import useHistory for navigation
import {
  CardTitle,
  CardDescription,
  CardHeader,
  CardContent,
  CardFooter,
  Card,
} from "@/components/ui/card";
import { Label } from "@/components/ui/label";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";

const AdminLogin = ({ setIsAdmin }) => {
  const navigate = useNavigate(); // Access the history object for navigation
  const [formData, setFormData] = useState({
    email: "",
    password: "",
  });

  const handleChange = (e) => {
    const { id, value } = e.target;
    setFormData((prevData) => ({ ...prevData, [id]: value }));
  };

  const handleLogin = () => {
    // Check if the username and password match the expected values
    if (formData.email === "admin@123.com" && formData.password === "123") {
      // Navigate to the admin home page
      localStorage.setItem("isAdmin", true);
      setIsAdmin(true);
      navigate("/admin-home");
    } else {
      // Handle invalid login (you can show an error message or perform other actions)
      console.log("Invalid login credentials");
    }
  };

  return (
    <Card className="w-full max-w-sm">
      <CardHeader className="text-center pb-0">
        <CardTitle className="text-3xl font-bold">Admin Login</CardTitle>
        <CardDescription>
          Enter your email below to login to your account.
        </CardDescription>
      </CardHeader>
      <CardContent className="space-y-4">
        <div className="space-y-2">
          <Label htmlFor="email">Email</Label>
          <Input
            id="email"
            placeholder="example@gmail.com"
            required
            type="email"
            value={formData.email}
            onChange={handleChange}
          />
        </div>
        <div className="space-y-2">
          <Label htmlFor="password">Password</Label>
          <Input
            id="password"
            placeholder="********"
            required
            type="password"
            value={formData.password}
            onChange={handleChange}
          />
        </div>
      </CardContent>
      <CardFooter className="flex justify-center">
        <Button className="w-full" onClick={handleLogin}>
          Login
        </Button>
      </CardFooter>
    </Card>
  );
};

export default AdminLogin;
```
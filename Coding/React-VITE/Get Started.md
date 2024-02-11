Create a folder with project name.

Open folder in VS Code.

Create folder Frontend.
Create folder Backend.

#### Create FEATURES.md.

```
## App Features

### User
- [ ] **Authentication**

Check the boxes once each feature is implemented and tested successfully. Happy coding!
```

#### Create LICENSE.

```
MIT License

Copyright (c) 2023 Fundx

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

#### Create README.md.

```
# App Name

App Description

Visit [App Name](https://www.app-link.com/) to kickstart your journey.

## Why App Name ?

More Description.

## Get Started

More Details to get going.
```

#### Open Frontend Folder

```
npm create vite@latest .
```

Press ok(y) , Chose React , Chose JavaScript

```js
npm install
npm run dev
```

#### Create a .env.local file

```
VITE_API_BASE_URL=http://localhost:5000/api/
```

#### Create following folders inside src folder.

components = NavBar/NavBar.jsx
pages = Home/Home.jsx

#### Install Essential Libraries for development.

```
npm i react-hot-toast react-query @hookform/resolvers @tanstack/react-query axios react-hook-form react-router-dom yup
```

#### Install ShadCN

#### Add Tailwind and its configuration

Install `tailwindcss` and its peer dependencies, then generate your `tailwind.config.js` and `postcss.config.js` files:

```
npm install -D tailwindcss postcss autoprefixer
```

```
npx tailwindcss init -p
```

#### Edit jsconfig.json file

Add the following code to the `jsconfig.json` file to resolve paths:

```json
{
  "compilerOptions": {
    // ...
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
    // ...
  }
}
```

### Update vite.config.js

Add the following code to the vite.config.js so your app can resolve paths without error

```
npm i -D @types/node
```

```
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import path from "path"

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
});
```

### Run the CLI

Run the `shadcn-ui` init command to setup your project:

```
npx shadcn-ui@latest init
```

### Configure components.json

You will be asked a few questions to configure `components.json`:

```
Would you like to use TypeScript (recommended)? no
Which style would you like to use? › Default
Which color would you like to use as base color? › Slate
Where is your global CSS file? › › src/index.css
Do you want to use CSS variables for colors? › no / yes
Where is your tailwind.config.js located? › tailwind.config.js
Configure the import alias for components: › @/components
Configure the import alias for utils: › @/lib/utils
Are you using React Server Components? › no
```

### That's it

You can now start adding components to your project.

```
npx shadcn-ui@latest add button
```

The command above will add the `Button` component to your project. You can then import it like this:

```
import { Button } from "@/components/ui/button"

export default function Home() {
  return (
    <div>
      <Button>Click me</Button>
    </div>
  )
}
```

#### Create util folder

Create axios.js file.

```js
import axios from "axios";

const baseURL = import.meta.env.VITE_API_BASE_URL;

const axiosClient = axios.create({
  baseURL: baseURL,
});

export default axiosClient;
```

#### Edit main.jsx file.

```js
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.jsx";
import "./index.css";
import { BrowserRouter } from "react-router-dom";
import { QueryClient, QueryClientProvider } from "react-query";

const queryClient = new QueryClient();

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <QueryClientProvider client={queryClient}>
      <BrowserRouter>
        <App />
      </BrowserRouter>
    </QueryClientProvider>
  </React.StrictMode>
);
```


#### Edit App.jsx file.

```js
import { useState } from "react";
import { Toaster } from "react-hot-toast";
import { Navigate, Route, Routes } from "react-router-dom";

function App() {
  const [isUser, setIsUser] = useState(localStorage.getItem("isUser"));

  return (
    <>
      <Toaster position="top-right" reverseOrder={false} />
      <div className="bg-blue-100 dark:bg-gray-900 dark:text-gray-50">
        <Navbar isUser={isUser} setIsUser={setIsUser} />
        <div className="pt-16 min-h-screen flex flex-col items-center justify-center">
          <Routes>
            {!isUser ? (
              <>
                <Route path="/" element={<Navigate to={"/signup"} />} />
                <Route
                  path="/signin"
                  element={<SignIn setIsUser={setIsUser} />}
                />
                <Route
                  path="/signup"
                  element={<SignUp setIsUser={setIsUser} />}
                />
              </>
            ) : (
              <>
                <Route exact path="/" element={<Home isUser={isUser} />} />
                <Route path="*" element={<ErrorPage isUser={isUser} />} />
              </>
            )}
          </Routes>
        </div>
        <Footer isUser={isUser} />
      </div>
    </>
  );
}

export default App;
```

#### Dark Mode Toggler

```js
import React, { useState, useEffect } from "react";
import toast from "react-hot-toast";

const DarkModeToggler = () => {
  const [darkMode, setDarkMode] = useState(false);

  useEffect(() => {
    // Check if dark mode preference is set in local storage
    const isDarkMode = localStorage.getItem("darkMode") === "true";
    setDarkMode(isDarkMode);

    // Apply dark mode class to the body
    if (isDarkMode) {
      document.body.classList.add("dark");
    } else {
      document.body.classList.remove("dark");
    }
  }, []);

  const setTabColor = (darkMode) => {
    const tabColor = !darkMode ? "#0F172A" : "#FFFFFF";
    document
      .querySelector("meta[name='theme-color']")
      .setAttribute("content", tabColor);
  };

  const toggleDarkMode = () => {
    const newDarkMode = !darkMode;
    toast.success("DarkMode Toggled Succesfully!");
    setDarkMode(newDarkMode);

    // Save dark mode preference to local storage
    localStorage.setItem("darkMode", newDarkMode);

    // Apply dark mode class to the body
    if (newDarkMode) {
      document.body.classList.add("dark");
    } else {
      document.body.classList.remove("dark");
    }
    setTabColor(darkMode);
  };

  return (
    <>
      <button onClick={toggleDarkMode}>
        {darkMode ? (
          <>
            <span className="group inline-flex flex-shrink-0 justify-center items-center h-9 w-9 font-medium rounded-full text-gray-800 hover:bg-gray-100 dark:text-gray-200 dark:hover:bg-gray-700">
              <svg
                className="w-4 h-4"
                xmlns="http://www.w3.org/2000/svg"
                width={16}
                height={16}
                fill="currentColor"
                viewBox="0 0 16 16"
              >
                <path d="M8 11a3 3 0 1 1 0-6 3 3 0 0 1 0 6zm0 1a4 4 0 1 0 0-8 4 4 0 0 0 0 8zM8 0a.5.5 0 0 1 .5.5v2a.5.5 0 0 1-1 0v-2A.5.5 0 0 1 8 0zm0 13a.5.5 0 0 1 .5.5v2a.5.5 0 0 1-1 0v-2A.5.5 0 0 1 8 13zm8-5a.5.5 0 0 1-.5.5h-2a.5.5 0 0 1 0-1h2a.5.5 0 0 1 .5.5zM3 8a.5.5 0 0 1-.5.5h-2a.5.5 0 0 1 0-1h2A.5.5 0 0 1 3 8zm10.657-5.657a.5.5 0 0 1 0 .707l-1.414 1.415a.5.5 0 1 1-.707-.708l1.414-1.414a.5.5 0 0 1 .707 0zm-9.193 9.193a.5.5 0 0 1 0 .707L3.05 13.657a.5.5 0 0 1-.707-.707l1.414-1.414a.5.5 0 0 1 .707 0zm9.193 2.121a.5.5 0 0 1-.707 0l-1.414-1.414a.5.5 0 0 1 .707-.707l1.414 1.414a.5.5 0 0 1 0 .707zM4.464 4.465a.5.5 0 0 1-.707 0L2.343 3.05a.5.5 0 1 1 .707-.707l1.414 1.414a.5.5 0 0 1 0 .708z" />
              </svg>
            </span>
          </>
        ) : (
          <>
            <span className="group inline-flex flex-shrink-0 justify-center items-center h-9 w-9 font-medium rounded-full text-gray-800 hover:bg-gray-100 dark:text-gray-200 dark:hover:bg-gray-800">
              <svg
                className="w-4 h-4"
                xmlns="http://www.w3.org/2000/svg"
                width={16}
                height={16}
                fill="currentColor"
                viewBox="0 0 16 16"
              >
                <path d="M6 .278a.768.768 0 0 1 .08.858 7.208 7.208 0 0 0-.878 3.46c0 4.021 3.278 7.277 7.318 7.277.527 0 1.04-.055 1.533-.16a.787.787 0 0 1 .81.316.733.733 0 0 1-.031.893A8.349 8.349 0 0 1 8.344 16C3.734 16 0 12.286 0 7.71 0 4.266 2.114 1.312 5.124.06A.752.752 0 0 1 6 .278zM4.858 1.311A7.269 7.269 0 0 0 1.025 7.71c0 4.02 3.279 7.276 7.319 7.276a7.316 7.316 0 0 0 5.205-2.162c-.337.042-.68.063-1.029.063-4.61 0-8.343-3.714-8.343-8.29 0-1.167.242-2.278.681-3.286z" />
              </svg>
            </span>
          </>
        )}
      </button>
    </>
  );
};

export default DarkModeToggler;
```

#### Edit Index.html file

```html
  <meta name="theme-color" content="#FFFFFF">
  <meta name="theme-color" content="#0F172A" media="(prefers-color-scheme: dark)">

  <title>Project Name</title>
```

#### First API Call

```js
// Import necessary dependencies
import React, { useState, useEffect } from 'react';
import axiosClient from './axios';

// Define your component
function Home() {
  // State to store the fetched data
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);

  // Function to fetch data from the API
  const fetchData = async () => {
    try {
      // Make a GET request to fetch data
      const response = await axiosClient.get('/posts'); // Example endpoint from JSONPlaceholder API
      setData(response.data);
      setLoading(false);
    } catch (error) {
      console.error('Error fetching data:', error);
      setLoading(false);
    }
  };

  // useEffect hook to fetch data when component mounts
  useEffect(() => {
    fetchData();
  }, []);

  // Render the component
  return (
    <div>
      <h1>API Data</h1>
      {loading ? (
        <p>Loading...</p>
      ) : (
        <ul>
          {data.map(item => (
            <li key={item.id}>{item.title}</li>
          ))}
        </ul>
      )}
    </div>
  );
}

export default Home;
```
#### Create vercel.json File

```json
{
    "routes": [
        {
            "src": "/[^.]+",
            "dest": "/",
            "status": 200
        }
    ]
}
```

#### Now You Are Ready to Host Your Project.

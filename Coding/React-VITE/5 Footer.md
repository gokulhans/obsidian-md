Create src/components/Footer/Footer.jsx

```js
import React from "react";
import { Link } from "react-router-dom";

const Footer = () => {
  return (
    <footer className="w-full py-6 bg-blue-50/70 dark:bg-gray-900/70">
      <div className="container px-4 sm:px-6 lg:px-8 xl:px-10 2xl:px-12">
        <div className="flex flex-col gap-4 sm:flex-row sm:items-center sm:justify-between">
          <nav className="flex gap-6 sm:order-last justify-center">
            <Link
              className="text-sm sm:text-base font-medium hover:underline"
              href="#"
            >
              Home
            </Link>
            <Link
              className="text-sm sm:text-base font-medium hover:underline"
              href="#"
            >
              About
            </Link>
            <Link
              className="text-sm sm:text-base font-medium hover:underline"
              href="#"
            >
              Services
            </Link>
            <Link
              className="text-sm sm:text-base font-medium hover:underline"
              href="#"
            >
              Contact
            </Link>
          </nav>
          <p className="text-xs sm:text-sm md:text-base text-gray-500 dark:text-gray-400 flex justify-center">
            © 2024 Acme Inc. All rights reserved.
          </p>
        </div>
      </div>
    </footer>
  );
};

export default Footer;
```
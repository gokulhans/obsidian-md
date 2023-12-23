```js
"use client";

import { Montserrat } from "next/font/google";
const montserrat = Montserrat({ subsets: ["cyrillic"], weight: "500" });

const Font = () => {
  return (
    <>
      <h1>Google Inter Font Specified in Layout.js</h1>
      <h1 className={montserrat.className}>Google Montserrat Font</h1>
    </>
  );
};
export default Font;
```

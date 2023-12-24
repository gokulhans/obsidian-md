create folder /api/ inside /app/

create a route

api/users/route.js

it should be route.js

```js
import { NextResponse } from "next/server";

export function GET() {
  return NextResponse.json({ result: "hello" });
}
```


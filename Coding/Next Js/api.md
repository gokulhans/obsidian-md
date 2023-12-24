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

## Dynamic API Routing

create folder like this [id]
users/1 result is params.id is 1 

```js
import { NextResponse } from "next/server";

export function GET(_, response) {
  const { id } = response.params;
  return NextResponse.json({ id });
}
```


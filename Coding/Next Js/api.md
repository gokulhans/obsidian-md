create folder /api/ inside /app/

create a route

api/users/route.js

it should be route.js

## Get Request

```js
import { NextResponse } from "next/server";

export function GET() {
  return NextResponse.json({ result: "hello" });
}
```

## Get Request By ID, Dynamic API Routing

create folder like this [id]
users/1 result is params.id is 1 

```js
import { NextResponse } from "next/server";

export function GET(_, response) {
  const { id } = response.params;
  return NextResponse.json({ id });
}
```

## POST Request

Post Request Function

```js
﻿export async function POST(req, res) {
﻿
	let { email, password } = await req.json();
	
	if (!email || !password) {
		return NextResponse.json(
		{ error: "required filed not found" },
		{ status: 400}
	);
	
	return NextResponse.json({ res: "data send successfully" });
}
```

Sample Post request Body

```js
{
	"email": "alex@gmail.com",
	"password": "alex123"
}
```


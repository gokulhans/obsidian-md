create folder named [user]
users/[user]
can call users/any_username
get it in params of the component.

```js
"use client";

const User = ({ params }) => {
  console.log(params);
    return (
    <div>{params.user}</div>
  )
}
export default User
```

if the route is like this => users/name/country/kerala/username

use users/[...user]
it create array of all params in name of user.
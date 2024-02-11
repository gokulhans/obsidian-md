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

#### Install Tailwind CSS

```
npm install -D tailwindcss
npx tailwindcss init
```

#### Configure your template paths

Add the paths to all of your template files in your `tailwind.config.js` file.
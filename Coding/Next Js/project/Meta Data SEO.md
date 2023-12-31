
layout.js

```js
export const metadata = {
  title: {
    default:"Next.js 14 Homepage",
    template:"%s Next.js 14"
  },
  description: "Next.js starter app description",
};
```

page.js

```js
export const metadata = {
  title: "About Page",
  description: "About description",
};
```

title template get common in every meta data file. eg:- About Page Next.js 14

### Dynamic metadata

```js
export const generateMetadata = async ({ params }) => {
  const { slug } = params;

  const post = await getPost(slug);

  return {
    title: post.title,
    description: post.desc,
  };
};
```
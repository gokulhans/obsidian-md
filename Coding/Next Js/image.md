## Local Image
internal image

```js
import Image from 'next/image';
import NaturalImage from '@/public/path-to-image.jpg'

<Image src={NaturalImage}
 alt="Description of the image"
 width={500} />
```

## External Image
internet image

```js
<img src="https://example.com/path/to/external/image.jpg" alt="Description of the external image" width={500} height={300} />
```

In next.config.js File add the image domain.

```js
/** @type {import('next').NextConfig} */
const nextConfig = {
 images: {
	 domains: ['example.com','images.another.com'],
 }, 
}
module.exports = nextConfig
```
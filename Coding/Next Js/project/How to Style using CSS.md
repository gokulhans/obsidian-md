
page.jsx

```js
import styles from "./home.module.css";

const Home = () => {
  return (
    <div className={styles.container}>Hello world</div>
  );
};

export default Home;
```

home.module.css

```css
.container {
  display: flex;
  gap: 100px;
}
```
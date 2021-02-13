# NextCommerce (IN EARLY DEVELOPMENT)

🛍 Add any commerce API to your Next.js project with NextCommerce

## Why?

Most Next.js commerce examples are tightly coupled to a certain provider. This library aims to provide an abstract API layer that means anybody building with Next.js only needs to learn, and build with one commerce API, NextCommerce.

No matter what commerce adapter is connected, developers invoking the `addItem` function can expect the same required args, and responses from cart, products, and checkout. This is great for agencies working with various commerce APIs too!

## Quickstart

### Server

```js
// pages/api/commerce/[...nextcommerce].js

import NextCommerce from "next-commerce";
import { ChecAdapter } from "next-commerce/adapters";

export default NextCommerce({
  adapter: ChecAdapter({
    public_key: "...",
  }),
});
```

### Client

```js
// pages/index.js

import { getProducts } from "next-commerce/inventory";
import { addItem } from "next-commerce/cart";

export async function getStaticProps() {
  const products = await getProducts({ limit: 6 });

  return {
    props: {
      products,
    },
  };
}

function IndexPage({ products }) {
  return (
    <ul>
      {products.map((product) => (
        <li key={product.id}>
          <p>{product.name}</p>
          <button onClick={() => addItem(product.id)}>Add to Cart</button>
        </li>
      ))}
    </ul>
  );
}
```

## Why API routes?

It's true this implementation could be done completely client-side, the server-side approach allows us to create secure transformers/serializers, and work with APIs that don't have any implement type tokens.

The added benefit is your site has its own proxy commerce API, go full omnichannel with your own API!

## Creating adapters

A NextCommerce adapter allows you to connect to whatever commerce API you are using while still using the familiar NextCommerce hooks on the frontend.

// src/App.js
import React, { useState } from 'react';
import './App.css';
import Header from './components/Header';
import ProductList from './components/ProductList';
import Cart from './components/Cart';

function App() {
  const [cart, setCart] = useState([]);

  const addToCart = (product) => {
    setCart([...cart, product]);
  };

  return (
    <div className="App">
      <Header />
      <main className="main-content">
        <ProductList addToCart={addToCart} />
        <Cart cart={cart} />
      </main>
    </div>
  );
}

export default App;




// src/components/Header.js
import React from 'react';

const Header = () => {
  return (
    <header className="header">
      <h1>Medicine Website</h1>
      <button className="cart-button">Cart</button>
    </header>
  );
};

export default Header;




// src/components/ProductList.js
import React from 'react';

const ProductList = ({ addToCart }) => {
  const products = [
    { id: 1, name: 'Medicine 1', description: 'Description 1', price: 10, quantity: 5 },
    { id: 2, name: 'Medicine 2', description: 'Description 2', price: 15, quantity: 0 },
    // Add more products as needed
  ];

  return (
    <div className="product-list">
      {products.map((product) => (
        <div key={product.id} className="product">
          <h2>{product.name}</h2>
          <p>{product.description}</p>
          <p>Price: ${product.price}</p>
          {product.quantity > 0 ? (
            <>
              <input type="number" defaultValue={1} min={1} max={product.quantity} />
              <button onClick={() => addToCart(product)}>Add to Cart</button>
            </>
          ) : (
            <p className="out-of-stock">Out of Stock</p>
          )}
        </div>
      ))}
    </div>
  );
};

export default ProductList;



// src/components/Cart.js
import React from 'react';

const Cart = ({ cart }) => {
  return (
    <div className="cart">
      <h2>Cart</h2>
      {cart.length === 0 ? (
        <p>Your cart is empty</p>
      ) : (
        <ul>
          {cart.map((item) => (
            <li key={item.id}>{item.name}</li>
          ))}
        </ul>
      )}
    </div>
  );
};

export default Cart;




/* src/App.css */
.App {
  text-align: center;
}

.main-content {
  display: flex;
  justify-content: space-around;
  margin: 20px;
}

.header {
  background-color: #3498db;
  padding: 20px;
  color: #fff;
}

.cart-button {
  background-color: #2ecc71;
  color: #fff;
  padding: 10px;
  border: none;
  cursor: pointer;
}

.product-list {
  display: flex;
  flex-wrap: wrap;
}

.product {
  border: 1px solid #ccc;
  padding: 10px;
  margin: 10px;
  text-align: center;
}

.out-of-stock {
  color: #ff0000;
}

.cart {
  width: 200px;
  border: 1px solid #ccc;
  padding: 10px;
  text-align: left;
}

.cart h2 {
  margin-bottom: 10px;
}

.cart ul {
  list-style: none;
  padding: 0;
}

.cart li {
  margin-bottom: 5px;
}


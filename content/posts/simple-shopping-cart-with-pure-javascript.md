+++
title = 'Simple Shopping Cart with pure Javascript'
date = 2022-05-18T00:00:00+00:00
draft = false
tags = ['javascript', 'tutorial', 'shopping-cart', 'teaching']
+++

I'm a code mentor and private programming tutor. Today, my student and I were working on event listeners in JS and I tried to teach how to make a simple and minimal shopping cart. If you are learning JS, this could be a good exercise. You can find the code [here](https://github.com/hamidhaghdoost/js-shopping-cart). And you can see a demo [here](https://js-shopping-cart-isvmhe6wo-tuytooshs-projects.vercel.app).

In this work, we added our products like this:

```html
<div class="product">
    <h3>Product one</h3>
    <p>Price: 2000</p>
    <button data-id="1" data-price="2000">Add to cart</button>
</div>
```

We know that in the real world we do not do this manually and we generate them with loops using data that we have retrieved from a database.

We also have a nav-bar like this:

```html
<div class="toolbar">
    <h1 class="brand">Shop</h1>
    <p>
        Cart items:
        <span id="count">0</span>,
        Price:
        <span id="sum">0</span>
    </p>
</div>
```

And in the JS file, we add event listeners to the add buttons:

```javascript
let btns = document.querySelectorAll(".products button");

for (let i = 0; i < btns.length; i++) {
    btns[i].addEventListener("click", add);
}
```

Then we add or remove the items based on the state of the product in the cart:

```javascript
function add(event) {
    let price = Number(event.target.dataset.price);

    let index = cart.indexOf(event.target.dataset.id);
    console.log(cart, index);
    if (index >= 0) {
        cart.splice(index, 1)
        count--;
        sum -= price;
        event.target.className = "";
        event.target.textContent = "Add to cart";
    } else {
        cart.push(event.target.dataset.id);
        count++;
        sum += price;
        event.target.className = "added";
        event.target.textContent = "Remove";
    }
    updateCart();
}
```

And finally, we update the cart based on the current cart items:

```javascript
function updateCart() {
    document.getElementById("sum").textContent = sum;
    document.getElementById("count").textContent = count;
}
```

The complete code is available in this [github repo](https://github.com/hamidhaghdoost/js-shopping-cart). If you find it useful, give it a star please :)

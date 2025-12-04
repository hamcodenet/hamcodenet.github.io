+++
title = 'Local Storage for shopping cart in Javascript'
date = 2022-05-23T00:00:00+00:00
draft = false
tags = ['javascript', 'localstorage', 'shopping-cart', 'tutorial', 'teaching']
+++

In a previous exercise class with students, we created a [simple shopping cart](https://hamcode.net/posts/simple-shopping-cart-with-pure-javascript/) with JS. Today I had another lecture and I added a `localStorage` feature to this project. In this version of the project, the added items can persist in the cart after a refresh and we added another file named `cart.html` that shows the added cart items. You can see the source code of this project in the v2.0.0 tag in this repo: [JsShoppingCart](https://github.com/hamidhaghdoost/js-shopping-cart)

In this lecture, we used JS Objects to store cart items like this:

```javascript
if (id in cart) {
    cart[id].qty++;
} else {
    let cartItem = {
        title: title,
        price: price,
        qty: 1
    };
    cart[id] = cartItem
}
```

And we added cart items to localStorage like this:

```javascript
localStorage.setItem("cart", JSON.stringify(cart));
```

Finally, in the `cart.js` file we can create table rows like this:

```javascript
let cart = {};
if (localStorage.getItem("cart")) {
    cart = JSON.parse(localStorage.getItem("cart"));
}

let tbody = document.getElementById("tbody");

for (let id in cart) {
    let item = cart[id];

    let tr = document.createElement('tr')

    let title_td = document.createElement('td')
    title_td.textContent = item.title
    tr.appendChild(title_td)


    let price_td = document.createElement("td");
    price_td.textContent = item.price;
    tr.appendChild(price_td);

    let qty_td = document.createElement("td");
    qty_td.textContent = item.qty;
    tr.appendChild(qty_td);

    tbody.appendChild(tr)

}
```

In the next session, we want to talk about AJAX and we will get the products from an API. If you find this code useful, give it a like :)

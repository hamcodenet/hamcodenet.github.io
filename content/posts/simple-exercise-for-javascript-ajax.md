+++
title = 'Simple exercise for Javascript Ajax'
date = 2022-05-14T00:00:00+00:00
draft = false
tags = ['javascript', 'ajax', 'tutorial', 'teaching']
+++

I have about 4 years of experience working as a private tutor of programming. About five years ago, I published a blog post on my website in Persian language entitled "[Private Laravel Tutor](https://haamid.ir/%D8%A2%D9%85%D9%88%D8%B2%D8%B4-%D8%AE%D8%B5%D9%88%D8%B5%DB%8C-%D9%84%D8%A7%D8%B1%D8%A7%D9%88%D9%84/)" and people started to call me. I always love teaching people and it was a good opportunity.

After a while, the number of students increased and today I have two sessions per day on average. Most of my previous students are now working around the world.

Today I had a JS session about working with AJAX. I'm posting the content of the code for beginner friends in this community.

## index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Learning Ajax</title>

    <link rel="stylesheet" href="css/app.css">
</head>
<body>
    <button class="btn" id="load">Load Posts</button>
    <button class="btn" id="clear">Clear Posts</button>
    <div id="posts">

    </div>
    <script src="js/app.js"></script>
</body>
</html>
```

## css/app.css

```css
body {
    margin: 0;
}

#posts {
    background-color: #f5f5f5;
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
}


.post {
    width: 25%;
    margin: 20px;
    border: 3px solid rgb(36, 220, 91);
    padding: 10px;
}

.post:hover {
    border: 3px solid rgb(0, 0, 0);
}

.post h1 {
    font-family: cursive;
}

.btn {
    padding: 10px;
    margin: 10px;
    background-color: rgb(36, 220, 91);
    color: black;
}
```

## js/app.js

```javascript

document.getElementById("load").addEventListener("click", function () {
    url = "https://jsonplaceholder.typicode.com/posts";
    sendAjax(url);
});

function sendAjax(url) {
    let http = new XMLHttpRequest();
    http.onload = function () {
        let posts_element = document.getElementById("posts");
        let posts = JSON.parse(this.responseText);

        posts.forEach(function (post) {
            let div = document.createElement("div");
            div.className = "post";

            let h3 = document.createElement("h3");
            h3.textContent = post.title;
            div.appendChild(h3);

            let p = document.createElement("p");
            p.textContent = post.body;
            div.appendChild(p);

            posts_element.appendChild(div);
        });
    };
    http.open("GET", url);
    http.send();
}

document.getElementById("clear").addEventListener("click", function () {
    let posts_element = document.getElementById("posts");
    posts_element.textContent = ''
});
```

If you are looking for a tutor, feel free to contact me :)

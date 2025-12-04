+++
title = 'Bootstrap open Accordion after Ajax loaded'
date = 2022-06-04T00:00:00+00:00
draft = false
tags = ['bootstrap', 'javascript', 'ajax', 'accordion']
+++

[Accordion](https://getbootstrap.com/docs/5.2/components/accordion/) is a nice component of Bootstrap. It uses the [Collapse](https://getbootstrap.com/docs/5.2/components/collapse/) feature of Bootstrap. It works properly under the hood, but sometimes you need to do something different. In my case, I needed to click on the accordion header, then send an Ajax request to get the content of the accordion, and then open it. There was not a straightforward API or documentation for that, and finally I found it.

```javascript
<script>
    let prevent = true;

    $("#collapseThree").on("show.bs.collapse", function (e) {
        if (prevent) {
            e.preventDefault();
        }
        setTimeout(function () {
            prevent = false;
            $("#collapseThree").collapse("show");
            prevent = true;
        }, 1000);
    });
</script>
```

In this example, I've added an event listener on the open state of collapse and I've used a `setTimeout` function to simulate an Ajax request.

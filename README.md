<h1>Up-to-date (for now) version of P5.js that works on Khan Academy</h1>
<!-- Oh dear, I'm not so good at this markdown thing. -->
<p>I was looking at a project (https://www.khanacademy.org/computer-programming/p5js-on-ka/5684432689086464) made by Bluebird (username @birdwatcher03 on KA and @birdofblue on Github) where he said: </p>

> ... KA messes with the webpage environment .... The window object is frozen. This means you can't redefine properties of window. For a long time p5.js has included a polyfill of requestAnimationFrame that KA breaks. If we instead put our code in an iframe which is unfrozen, the polyfill shouldn't break and p5.js should run normally. Then I can move on to figuring out the thumbnail, and little quirks.
> So far, somewhat good.
>
> Also, turns out *the most recent version of p5.js actually doesn't have the polyfill*, so maybe i need to just make a new program. Gotta check it out more.

<p>(Emphasis was added my me.)</p>

<p>I wondered what would happen if I tried the most recent version of P5.js in Khan Academy, and it didn't initially work. If you try it for yourself, the console will probably have something like this:</p>

```
🌸 p5.js says: p5 had problems creating the global function "print", possibly because your code is already using that name as a variable. You may want to rename your variable to something else. (http://p5js.org/reference/p5/print)
```
<p>And this:</p>

```
p5.js:66694 Uncaught (in promise) TypeError: Cannot assign to read only property 'print' of object '#<Window>'
    at p5.js:66694:42
    at new p5 (p5.js:66506:23)
    at _globalInit (p5.js:65322:15)
```

<p>in it.<br><br>
So, I renamed the `print()` function to `print1()`, which was probably a very bad idea in light of usability and clarity.
However, it works on Khan Academy!<br>
I typically use the one (https://cdn.jsdelivr.net/gh/vExcess/library@main/p5.js) Vexcess (@VXS on KA) or Dark Owl (https://www.khanacademy.org/computer-programming/i/5295202303000576) had modified for use on KA, which work well except they are currently a bit outdated.<br>
I, and most likely others as well, sometimes like to use functions like `beginClip()`/`endClip()` which are not included in those versions.
</p>

<h3>Using this P5.js fork</h3>

Here's a simple example if it helps:

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>Thanks to Bluebird</title>
        
        <script src="https://cdn.jsdelivr.net/gh/4rmaged/p5.js@main/lib/p5.js"></script>
        <style>
            *{
                margin:0;
                padding:0;
            }
            body{
                width:100%;
                height:100%;
            }
            #container{
                width:100vw;
                height:100vh;
                overflow-y: hidden;
            }
            canvas{
                background-color:red;
            }
        </style>
    </head>
    <body>
        <div id="container"><canvas id="mycanvas" alt="Oops, it looks like your browser might not support the canvas element!"></canvas></div>
        <script type>
            let x=0;
            function setup(){
                let b = document.querySelector("#container").getBoundingClientRect();
                createCanvas(b.width,b.height,document.querySelector("#mycanvas"));
                fill("black");
                // You have to use `print1()` instead of `print()`
                // because of bad ideas enacted my me!
                print1("Hello, world!");
            }
            function draw(){
                background("orange");
                ellipse(x,height/2,20,20);
                x++;
            }
        </script>
        <!--<script>-->
    </body>
</html>
```

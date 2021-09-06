---
layout: post
title:  "Print.sc Link Generator"
date:   2021-09-06 00:30:00 -0600
author: Leo
categories: javascript
---

So today I was watching a [LTT](https://youtu.be/05K5glVCwis) video about TikTok _hacks_ and they mentioned [this](https://prnt.sc/) site. It is apparently a service that lets you host screenshots to share easily. They also offer a tool that seems to automatically generate a url for your screenshot. This is where things sketchy.

All the links are publicly accessible and in a very predictable two letter, four digit format `https://prnt.sc/aa0000`. I spent a couple of minutes typing random letters and numbers before I got annoyed and figured I could automate it so here it is:

### Link Generator

{% include prnt-link-generator.html %}

## Code
Because GitHub Pages only lets you run client-side scripts I had to learn some JS to make this so don't judge my code too much.

```js
// This function will write a new link to the the html link element
function rnd_link() {

    // Make 4 random digits
    let a = Math.floor(Math.random() * 10);
    let b = Math.floor(Math.random() * 10);
    let c = Math.floor(Math.random() * 10);
    let d = Math.floor(Math.random() * 10);

    // variables to store the random letters
    let string = '';
    let rnd_char;

    // make two random letters using the ASCII numbers for all lower case letters
    for (let i = 0; i < 2; i++) {
        rnd_char = Math.floor((Math.random() * 25) + 97);
        string += String.fromCharCode(rnd_char)
    }

    // Build url string
    url = 'https://prnt.sc/' + string + a + b + c + d

    // Add url to link and link text
    document.getElementById("link").innerHTML = '<a href="' + url + '" target="_blank" rel="noopener noreferrer">' + url + '</a>';
}
```

Generating random numbers in JS is a bit annoying since the `Math.random()` function only gives you a random number between 0 and 1 but not including 1. This means you have to add the math to turn that into a random number from 0 to 10.

The other weird bit was making the random 4 digit number since you can't specify length for the random number. I am sure there is a better way of doing it but I didn't want to think about it too much so just generating 4 separate digits was good enough for me. This also makes sure that cases like a two digit number have their corresponding zeros on the left side.

## Final thoughts
I have also made this link generator available [here](https://catorce.uno/prnt-link-generator) as a stand alone git pages site. I still have to make some quality of life improvements like responsive html so it doesn't look like it was made for ants when you see it from a smartphone. Also, if I don't get distracted from this, I might make it fetch and display the screenshot from the site so you don't have to navigate to a different tab./

And please don't use sketchy sites that host your screenshots publicly!

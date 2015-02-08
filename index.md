---

layout: default

style: |

  .slide p {
    margin-bottom: 24px;
  }

  .slide h3 {
    font-size: 30px;
    font-weight: bold;
  }

  .slide blockquote cite {
    font-weight: 700;
  }

  .slide table th,
  .slide table td {
    background: none;
  }

  .slide pre code {
    background-color: #efefef;
    padding: 0.5em;
    line-height: 1.5em;
    font-sizeL 20px;
  }

  .no-title h2 {
    display: none;
  }

  .two-codes table td {
    width: 50%;
  }

---

# Component development in CSS

*by [Varya Stepanova](http://varya.me/) from [SC5 Online](http://sc5.io/)*

![](pictures/cover.jpg)

<!-- This lecture is about developing web interfaces with CSS from component perspective -->

<style>

.cover {
  color: #fff;
}

.cover h2 {
  color: #fff;
  font-weight: bold;
  font-size: 90px;
  line-height: 1.25em;
  text-shadow: 5px 10px 15px rgba(0,0,0,1);
}

.cover p {
  text-shadow: 5px 10px 15px rgba(0,0,0,1);
}

.cover a {
  color: #fff;
}

</style>

## Me
{: .no-title }

### Now
Senior Frontend Developer for SC5 Online

### Before
TMG (Amsterdam, the Netherlands); Yandex (Moscow, Russia)

###Area of expertise
Components on the web: libraries, SGDD, BEM. Techs: CSS, JavaScript, etc.

<!--
Before we start, I would like to introduce myself and explain why
this topic has been chosen.
-->

## Spoiler

You will learn:

TODO: List

<!--
This is what I'm going to show today
-->

## CSS



> *Cascading Style Sheets* (CSS) is a style sheet language used for describing the look and formatting of a document
> written in a markup language. <cite>[Wikipedia](https://en.wikipedia.org/wiki/Cascading_Style_Sheets)</cite>

First published in 1996
{: .note}

<!--
The meaty part of the lecture is about CSS.
Are you familiar with this technology?

CSS is used to style web documents. CSS rules can be matched to DOM nodes and bring them view which
is descriped with CSS properties.

This concept is pretty old. CSS was first introduced in 1996. And nothing conceptually has been changed since then.
However the web now is far more complex than in 1996, so in industry we are facing the chalelngies and need a way to
overcome.
-->

## Industry challenges
{: .no-title }

![](pictures/homepage.png)

<!--
In this picture you can see how the web pages used to look like. And from the architectural point of view they were
similar. The industry just did not have experience back then to provide recommendations how to build the we good.

Now things have already changed. Today, if you are developing not you cat's homepage but a serious website, it should
meet the requirements.
-->

## Bulletproof Web Desing
{: .bulletproof .no-title }

<!--
This problem was first spoken out loud by this gentelman. His name is Dan Cederholm and he is the author of the book
shown. The "Bulletproof Web Design" is a first place where the inductry needs were explained.
In was first published in 2005 and has 2 more editions since then. However this is quite mature book, I still recommend
it if you want to step in the industry level of creating web sites.
He first said that the HTML/CSS markup we produce should be stable. It should be maitainable meaning not very sensetive
to the providing changes.
So, it's not like single action - provide the code and forget about it. A developer will get back to their code to fix
something. Other developers will bring their changes into the code. And nothing should be broken in unexpected places.
-->

<style>
.bulletproof {
  background-image:
    url('pictures/bulletproof.jpg'),
    url('pictures/dan-cederholm.jpg');
  background-position: top right, -120px 0;
  background-size: auto, 100%;
  background-repeat: no-repeat;
}
</style>

## Big CSS

* massive sites
* big teams of developers
* heavy UI
* long running projects

<!--
massive sites: A lot of code, thousands of lines
big teams of developers: up to hundreds of ppl, teams can grow and change
heavy UI: each piece of interface has a lot of code and logic behind
long running project: need to be maintainable
-->

##Is this good?

    H1 { color: blue }
    P EM { font-weight: bold }
    A:link IMG { border: 2px solid blue }
    A:visited IMG { border: 2px solid red }
    A:active IMG { border: 2px solid lime }

<!--
Now look at this code. Do you see something strange? Any guess?
Who would write their CSS like this?

The problem is that CSS was created to make text bold and links underlined. It ideally suited
solving these problems. In many websites developers still use CSS like.

Actually this code from [CSS level 1 specification](http://www.w3.org/TR/CSS1/). It is
very simple, was recommended in 1996. Time passed and we met new chalenges.
-->

## What makes CSS hard?

* …Vertical centering
* …Equal height columns
* …Browser inconsistencies
* …Unobvious tricks

<!--
Before we decide what is wrong with that peice, let's guess what is hard in CSS.

When ppl are asked, the repson is usually
- vertical centing
- making columns of equial height
- browers render CSS differently, so it takes special knowledge and work to make the interface consistent
- many solutions are unobvious tricks which needed to be memorized

But this is not true, this is easy or at least clear how to manage. You can google for all this questions.
-->

## What are the real hard problems in CSS?

* Scoping
* Specificity conflicts
* Non-deterministic matches
* Dependency management
* Removing unused code

<!--
The real hard problems of CSS are here:
- No scoping. Everything is CSS is global.
- Specificity conflicts. I'll explain in detal later.
- Non-deterministic matches which naturally result from declarativeness of CSS language
- Dependency management
- Removing unused code
-->

## CSS has no scoping

    a { /* Affects all the links */
      color: red;
    }
    ul li a { /* Affects all the links in lists */
      color: green;
    }

<!--
This especially maters if you link third-party CSS.
A common problem for developing libraries or code which will be later delivered to another web site.
Everything in CSS is global, and writing good CSS is similar to writing a good program module if you only allowed to use
global variables.
This can be mixed with another CSS and applied to wrong nodes.
Writing good CSS means you has to predict the future.
-->

## Specificity

> Specificity is the means by which a browser decides which property values are the most relevant to an element and gets
> to be applied. Specificity is only based on the matching rules which are composed of selectors of different sorts.

<!--
Another problem is specificity.
Who remember what specificity is?
Ok, I will explain.
-->

## The most specific matters

    <div id="test">
      <span>Text</span>
    </div>

<separator/>

    div#test span { color: green }
    span { color: red }
    div span { color: blue }

<!--
If a brower has 2, 3 or more rules which match the same DOM node, how it decides what are the properties to take into
work?
The order does not matter.
For every selector a browser calculates how important this set of rules is. The rule with the more specific selector
would be prioritized.
So, here we see...
-->

## How to override?

    <div class="sidebar">Left floated sidebar</div>

<separator/>

    .sidebar { /* Does not work?! */
      float: right;
    }
{: .next }

<separator/>

    body .sidebar { /* Overrides 'div .sidebar {}' */
      float: right;
    }
{: .next }

<!--
When it comes to developments, specificity matters when redefining pre-given
components.

To redefine the left-floated sidebar, we would overwrite the rule.
-->

## Specificity hell
{: .no-title }

    .navbar-inverse .navbar-nav>li>a {
      color: #999;
    }

    #home-menu-container #home-menu li a {
      color: red;
    }

    body #home-menu ul li a {
      color: blue !important;
    }

<!--
People ask on Stackoverflow how to overwrite Bootsrtap
These things can be in different files
-->

##Non-deterministic matches

    #content div div {
      float: left;
    }

<!-- This can be matched to anything -->
<!-- You cannot rely on the document structure, because it contantly changes while developing -->
<!-- в момент, когда ты пишешь, ты указываешь признаки нод, на которые сматчится правило, а не точный адрес. смотри:
можно писать адрес «Rettigweg 1, 13187 Berlin", а можно «около Wollankstrasse такая боковая улица с тремя домами, и
там есть такой желтый дом, и там на втором этаже ещё балконы металлические с узорами» -->

## Dependency management
{: .dependency-management }

###No dependencies, sorry

<div class="next" markdown="1">
### But what about?

    @import url('i-need-this.css');
</div>

### No, sorry again.
{: .next .sorry }

<!--
CSS was not developed as a programming language and now it still isn't. So, there is no way to declare that
one piece of CSS needs anotehr one.
OK, there is import. But this is not  aproduction solution. And assuming undeterministic matches we cannot rely on it.
-->

<style>
.dependency-management .sorry
{
  color: green;
}
</style>

## Removing unused code

100 pages in projects

    .person div a {
      color: pink;
    }

Can I remove it? Will it break something? Maybe it is for a third-party HTML code?

<!--
CSS is declarative, so you cannot say what are the nodes the rules will aply to.
If you have a lot of pages you cannot remove a piece of CSS and check visually if something is broken.
Even worse with  dynamic web sites.
-->

## Where CSS is hard?
{: .no-title .hard-css }

<table><thead>

<th markdown="1">

This is not hard in CSS

</th>

<th markdown="1">

This is!

</th>

</thead><tr>

<td markdown="1">

    #sidebar ul li a {
      <mark>color: red;</mark>
      <mark>display: block;</mark>
      <mark>padding: 1em;</mark>
    }

</td>

<td markdown="1">

    <mark>#sidebar ul li a</mark> {
      color: red;
      display: block;
      padding: 1em;
    }

</td>

</tr></table>

*How do we architect encapsulated components?*
{: .next }

<!--
Writing CSS is easy. It is very easy to read and it is very likely that you can
find the tricks you need at Stackoverflow. But architechting CSS is very difficult.

We need a way to architect independent encapsulated components.
Being put into any place on the page, the components should not break anything. Also, it should not be broken
itself.
-->

<style>
.hard-css em {
  font-size: 30px;
}
</style>

## Methodologies
{: .shout }

<!--
As CSS does not provide us with the answer to the question how to do it, the developers should up
the methodologies.
The methodology does not give change into the technology. It suggest a developer how to use the
technology better.
-->

##OOCSS
{: .shout }

<!--
The first methodology proposed was OOCSS, stands for Object Oriented CSS.
-->

##Nicole<br/>Sullivan
{: .nicole }

<!--
It was in 2007, this is Nicole Sullivan, who authored it.
She worked for Yahoo and by that time she was dealing with components for Yahoo UI and was trying to
give some order to all this mess. So, she proposed to use some principles from OOP to CSS. This was in 2007.
I will not explain the detailes because I belive that this era is passed by.
But I still think that I should mentione her as a pioneer. She was a first developer who was trying to
solve it.
-->

<style>

.nicole {
  position: relative;
  background-image: url('pictures/nicole-sullivan.jpg');
}

.nicole h2 {
  position: absolute;
  right: 100px;
  bottom: 275px;
  font-size: 80px;
  color: white;
  font-weight: bold;
  text-shadow: 5px 10px 15px rgba(0,0,0,1);
}

</style>

## SMACSS
{: .shout }

<!--
Another milestone is SMACCS, which is Scalable and Modular Architecture for CSS.
This is a book, first published in 2009 but still available.
-->

##Jonathan<br/>Snook
{: .jonathan }

<!--
The author is this gentelman, Jonathan Snook. You can find his website if interested.
-->

<style>

.jonathan {
  position: relative;
  background-image:url(pictures/jonathan-snook.jpg);
}

.jonathan h2 {
  position: absolute;
  right: 50px;
  bottom: 200px;
  font-size: 72px;
  font-weight: bold;
}

</style>

## BEM
{: .shout }

<!--
And the last new thing appeared was BEM, stands for Block, Element Modifier.
It was created in 2009, then evoluated and had a long way to its popularity by now.
-->

## Vitaly<br/>Harisov
{: .harisov }

<!--
This is one of the main authors. Vitaly Harisov. He works for Yandex and heads the
frontend development there.
-->

<style>

.harisov {
  position: relative;
  background-image: url(pictures/vitaly-harisov.jpg);
  background-size: auto 640px;
}

.harisov h2 {
  position: absolute;
  right: 100px;
  bottom: 200px;
  font-size: 80px;
  font-weight: bold;
}

</style>

## Sergey<br/>Berezhnoy
{: .veged }

<!--
Another co-author is Sergey Berezhnoy, who also works for Yandex.
O was very lucky to work with them and be a member of the BEM team, so I can tell you
a little bit more about it today.
-->

<style>

.veged {
  position: relative;
  background-image: url(pictures/veged.jpg);
  background-size: 1024px auto;
}

.veged h2 {
  position: absolute;
  left: 100px;
  top: 100px;
  font-size: 80px;
  font-weight: bold;
}

</style>

## BEM eco-system

* <mark>CSS Methodology</mark>
* JavaScript framework
* Template engine
* Building system
* Supplementary tools

<!--
Actually behind BEM there is a massive amount for JavaScript libraries, own template engine, many supplimentary tools.
Mosty these things are very local, but the CSS Methodology is a popular thing and becoming a standard all over the
world. So, I'll explain it in details.
-->

## Harry & Nicolas
{: .no-title .harry-nicolas }

### Harry<br/>Roberts
{: .harry }

###Nicolas<br/>Gallagher
{: .nicolas }

<!--
These 2 gentelmen are also important persons in the BEM community.
These are Harry Roberts from Britan and Nicolas Gallaher from USA. They had have a great role in BEM to be wide-spreaded
and become a standard.
Both are very famous developers and Harry is also the most wanted speaker for frontend conferences now.
So, if you are interested in their motivation of taking this approach, you can google for their blogs and social
networks accounts.
-->

<style>

.harry-nicolas {
  position: relative;
  background-image: url(pictures/harry-nicolas.jpg);
}

.harry-nicolas .harry {
  color: #fff;
  font-size: 50px;
  position: absolute;
  bottom: 50px;
  left: 300px;
  line-height: 1.5em;
}

.harry-nicolas .nicolas {
  color: #fff;
  font-size: 50px;
  position: absolute;
  bottom: 50px;
  right: 50px;
  line-height: 1.5em;
}

</style>

## BEM

* Block
* Element
* Modifier

## Interface
{: .no-title .interface }

<style>
.interface div {
  margin-top: 20px;
  background-image: url(pictures/bem/page.png);
  background-size: contain;
  background-repeat: no-repeat;
}
</style>

## Interface of blocks
{: .no-title .interface-blocks }

<style>
.interface-blocks div {
  margin-top: 20px;
  background-image: url(pictures/bem/page-blocks.png);
  background-size: contain;
  background-repeat: no-repeat;
}
</style>

## Everything is a block
{: .no-title }

    <body class="page">

      <div class="header">
          <img class="logo" ... />
          <div class="search">...</div>
          <div class="menu">...</div>
      </div>

      <div class="layout">
          <div class="sidebar">...</div>
          <div class="menu">...</div>
      </div>

<!-- Blocks are marked with classes in HTML -->

## Why not...?

    <ul id="menu">
      <li>Tab 1</li>
      <li>Tab 2</li>
    <ul>

<separator/>

    #menu {
      /* styles for element */
    }

## No IDs

Someday you will need to repeat the block at the same page

## Elements
{: .elements }

![](pictures/bem/elements.png)

## Elements markup
{: .no-title }


    <div class="tabbed-pane">
      <ul>
          <li class="<mark>tabbed-pane--tab</mark>">Tab1</li>
          <li class="<mark>tabbed-pane--tab</mark>">Tab2</li>
          <li class="<mark>tabbed-pane--tab</mark>">Tab3</li>
      </ul>
      <div class="tabbed-pane--pane">
          ...
      </div>
    </div>

## CSS for an element

    .block {
      /* styles for block */
    }
      <mark>.block--element</mark> {
        /* styles for element */
      }

<!--
Elements have their own CSS classes. These classes are named so that it is clear which block the
element belongs to.
So, the idea is to encapsulate the components, its name becomes a kind of namespace and everything inside belongs to
this namespace.
Here dash-dash is used as a separator. Sometimes people use 2 underscores, but dash-dash looks like the most
common convention.
-->

## Why not...?

    <ul class="menu">
      <li class="item">Tab 1</li>
      <li class="item">Tab 2</li>
    <ul>

<separator/>

    .menu .item {
      /* styles for element */
    }

## No cascade

    <div class="panels">
      <div class="item">
          <ul class="goods">
            <li class="item">
              <!--
                Remember: <mark>non-deterministic matches</mark>
                -->
            </li>
          </ul>
      </div>
    </div>

<!--
Poor little item does not know if it belongs to panels or to goods.
Making the selector more specific would not help, because we cannot rely on the document structure.
-->

## Modified block
{: .no-title .modified-block }

<!--
Components are similar visually and  functionally.
Good not to repeat ourselves but to reuse the code of the first component and provide some changes to it.
-->

## Modifier

    <ul class="menu <mark>menu_footer</mark>">
      <li class="menu--item">...</li>
      ...
    </ul>

<separator/>

    .menu_footer {
      font-size: 0.8em;
    }

<!--
BEM answer to this question is a modifier.
With additinal CSS clas to a block you can provide more information about view.
You can see that both block class and modifier class sit together at the same node.
-->

<style>
.modified-block div {
  padding-top: 20px;
  background-image: url(pictures/bem/site-footer-menu.png);
  background-size: contain;
  background-repeat: no-repeat;
}
</style>


## CSS for a modifier
    .block {
      /* styles for block */
    }
      <mark>.block_modifier</mark> {
        /* styles for modifier */
      }
      .block--element {
        /* styles for element */
      }

## Modified element

![](pictures/bem/menu-current-item.png)

## Element's modifier

    <ul class="menu">
      <li class="menu--item">Tab 1</li>
      <li class="menu--item <mark>menu--item_current</mark>">Tab 2</li>
      <li class="menu--item">Tab 3</li>
    </ul>

## CSS for an elements' modifier

    .block
      /* styles for block */
    }
      .block--element {
        /* styles for element */
      }
        <mark>.block--element_modifier</mark> {
          /* styles for modified element
        }
{: .css }

## Why not...?

    <ul class="menu footer">...<ul>

<separator/>

    .menu.footer { /* combined selector */
      font-size: 0.8em;
    }

## Why not...?

    <ul class="menu">
      <li class="menu--item current">Tab 2</li>
    <ul>

<separator/>

    .menu--item.current { /* combined selector */
      background-color: red;
    }

## No overspecific selectors

You would suffer when redefining

    .menu--item.current {
      background: white;
    }
    .menu_dark .menu--item {
      background: black; /* Still white, baby */
    }

## BEM & CSS preprocessors

    .block {
      /* styles for block */
      <mark>&</mark>_modifier {
        /* styles for modifier */
      }
      <mark>&</mark>--element {
        /* styles for element */
      }
    }
{: .css }

## [getbem.com](http://getbem.com/)
{: .shout }

## This is solved

* Scoping
* Specificity conflicts
* Non-deterministic matches
* Dependency management
* Removing unused code

## Web Components
{: .shout }

<!-- More info: https://developer.mozilla.org/en-US/docs/Web/Web_Components -->

## Technologies behind
{: .wc-behind }

<div class="wc-logo"></div>

* Shadow DOM
* Custom Elements
* HTML Templates
* HTML Imports

<style>

.wc-behind .wc-logo {
  display: block;
  float: right;
  width: 200px;
  height: 200px;
  margin-right: 200px;
  background-image:url('pictures/webcomponents.png');
  background-size: contain;
  background-repeat: no-repeat;
  background-position: 50% 50%;
}

</style>

## Web Components

* [Navite component](demo/video.html)
* [Custom web component](demo/custom-button.html)
* [Templates](demo/templates.html)
* [HTML import](demo/html-import.html)

<!-- The idea is that you can teach the browser how to deal with your custom components. -->

<!-- So, the CSS now can be scoped -->

## HTML import, library

    <!-- Import element -->
    <link rel="import" href="my-lib/google-map.html">

    <!-- Use element -->
    <google-map lat="37.790" long="-122.390"></google-map>

## Are We Componentized Yet?
{: .componentized }

![](pictures/componentized.png)

<style>

.componentized img {
  width: 100%;
}

</style>

## Web Components Polyfills
{: .wc-polyfills }

* [WebComponents.org](http://webcomponents.org/)
* [X-Tag](http://www.x-tags.org/)

<style>

.wc-polyfills ul li::before {
  content: '';
  width: 100px;
  height: 100px;
  margin-right: 1em;
  display: inline-block;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: top left;
  background-position: 50% 50%;
  vertical-align: middle;
}
.wc-polyfills ul li:first-child::before {
  background-image: url('pictures/webcomponents.png');
}
.wc-polyfills ul li:nth-child(0n + 2)::before {
  background-image: url('pictures/polymer.svg');
}

</style>

## Make it work

    <!-- Polyfill Web Components support for older browsers -->
    <mark><script src="webcomponents.min.js"></script></mark>

    <!-- Import element -->
    <link rel="import" href="google-map.html">

    <!-- Use element -->
    <google-map lat="37.790" long="-122.390"></google-map>

## Ready-made components

* [Polymer](https://www.polymer-project.org/)
* [Google Web Components](http://googlewebcomponents.github.io/)

## Usage examples

* [Toolbar](demo/toolbar.html)
* [Google map](demo/google-map.html)

## Style guide driven development

## Summary

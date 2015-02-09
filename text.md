# Component development in CSS

Hello. My name is Varya Stepanova. I am from SC5 Online.
This lecture is about developing web interfaces with CSS from component perspective.

## Me

Before we start, I would like to introduce myself and explain why
this topic has been chosen.

## Spoiler

This is what I'm going to show today

## CSS

The meaty part of the lecture is about CSS.
Are you familiar with this technology?

CSS is used to style web documents. CSS rules can be matched to DOM nodes and bring them view which
is descriped with CSS properties.

This concept is pretty old. CSS was first introduced in 1996. And nothing conceptually has been changed since then.
However the web now is far more complex than in 1996, so in industry we are facing the chalelngies and need a way to
overcome.

## Industry challenges

In this picture you can see how the web pages used to look like. And from the architectural point of view they were
similar. The industry just did not have experience back then to provide recommendations how to build the we good.

Now things have already changed. Today, if you are developing not you cat's homepage but a serious website, it should
meet the requirements.

## Bulletproof Web Desing

This problem was first spoken out loud by this gentelman. His name is Dan Cederholm and he is the author of the book
shown. The "Bulletproof Web Design" is a first place where the inductry needs were explained.
In was first published in 2005 and has 2 more editions since then. However this is quite mature book, I still recommend
it if you want to step in the industry level of creating web sites.
He first said that the HTML/CSS markup we produce should be stable. It should be maitainable meaning not very sensetive
to the providing changes.
So, it's not like single action - provide the code and forget about it. A developer will get back to their code to fix
something. Other developers will bring their changes into the code. And nothing should be broken in unexpected places.

## Big CSS

massive sites: A lot of code, thousands of lines
big teams of developers: up to hundreds of ppl, teams can grow and change
heavy UI: each piece of interface has a lot of code and logic behind
long running project: need to be maintainable

## Massive web sites

You cannot check all the pages visially for every change, so your code should be written the way which
makes it possible to predict.

A lot of websites with common codebase: repeating would be too expensive.

## Big teams

Hundreds of people.
Developers need common approaches.
Communication matters.

## Heavy UI

This login form in the middle does not look as a massive component.
Just 2 inputs, checkbox, button.
Guess how much code is needed to represent it?

## Heavy UI

So, this is HTML.
And almost every node here needs CSS. Not one property but many.


## Long running projects


In the web development you cannot create version 2, we provide changes little by little
So, the code should be maintainable for years


##Is this good?

Now look at this code. Do you see something strange? Any guess?
Who would write their CSS like this?

The problem is that CSS was created to make text bold and links underlined. It ideally suited
solving these problems. In many websites developers still use CSS like.

Actually this code from [CSS level 1 specification](http://www.w3.org/TR/CSS1/). It is
very simple, was recommended in 1996. Time passed and we met new chalenges.

## What makes CSS hard?

Before we decide what is wrong with that peice, let's guess what is hard in CSS.

When ppl are asked, the repson is usually
- vertical centing
- making columns of equial height
- browers render CSS differently, so it takes special knowledge and work to make the interface consistent
- many solutions are unobvious tricks which needed to be memorized

But this is not true, this is easy or at least clear how to manage. You can google for all this questions.

## What <b>really</b> makes CSS hard?

The real hard problems of CSS are here:
- No scoping. Everything is CSS is global.
- Specificity conflicts. I'll explain in detal later.
- Non-deterministic matches which naturally result from declarativeness of CSS language
- Dependency management
- Removing unused code

## CSS has no scoping

This especially maters if you link third-party CSS.
A common problem for developing libraries or code which will be later delivered to another web site.
Everything in CSS is global, and writing good CSS is similar to writing a good program module if you only allowed to use
global variables.
This can be mixed with another CSS and applied to wrong nodes.
Writing good CSS means you has to predict the future.

## Specificity

Another problem is specificity.
Who remember what specificity is?
Ok, I will explain.

## The most specific matters

If a brower has 2, 3 or more rules which match the same DOM node, how it decides what are the properties to take into
work?
The order does not matter.
For every selector a browser calculates how important this set of rules is. The rule with the more specific selector
would be prioritized.
So, here we see...

## How to overwrite?

When it comes to developments, specificity matters when redefining pre-given
components.

To redefine the left-floated sidebar, we would overwrite the rule.

## Specificity hell

This is the real example I found on the net.

People ask on Stackoverflow how to overwrite Bootsrtap
These things can be in different files

##Non-deterministic matches

CSS is declarative and this is a big point.

When you are sending a paper letter to a friend, you write address "London, Baker street, bld 221B, to mr Holmes" and can be sure that this letter will be delivered to them.

In CSS you write someting "This is on a big street, and there is a house with balcony there, and a shop nearby"

This can be matched to anything
You cannot rely on the document structure, because it contantly changes while developing.

## Dependency management

CSS was not developed as a programming language and now it still isn't. So, there is no way to declare that
one piece of CSS needs anotehr one.
OK, there is import. But this is not  aproduction solution. And assuming undeterministic matches we cannot rely on it.

## Removing unused code

CSS is declarative, so you cannot say what are the nodes the rules will aply to.
If you have a lot of pages you cannot remove a piece of CSS and check visually if something is broken.
Even worse with  dynamic web sites.

## Where CSS is hard?

Writing CSS is easy. It is very easy to read and it is very likely that you can
find the tricks you need at Stackoverflow. But architechting CSS is very difficult.

We need a way to architect independent encapsulated components.
Being put into any place on the page, the components should not break anything. Also, it should not be broken
itself.


## Methodologies

As CSS does not provide us with the answer to the question how to do it, the developers should up
the methodologies.
The methodology does not give change into the technology. It suggest a developer how to use the
technology better.

##OOCSS


The first methodology proposed was OOCSS, stands for Object Oriented CSS.

##Nicole<br/>Sullivan

It was in 2007, this is Nicole Sullivan, who authored it.
She worked for Yahoo and by that time she was dealing with components for Yahoo UI and was trying to
give some order to all this mess. So, she proposed to use some principles from OOP to CSS.
I will not explain the detailes because I belive that this era is passed by.
But I still think that I should mentione her as a pioneer. She was a first developer who was trying to
solve it.

## SMACSS

Another milestone is SMACCS, which is Scalable and Modular Architecture for CSS.
This is a book, first published in 2009 but still available.

##Jonathan<br/>Snook

The author is this gentelman, Jonathan Snook. You can find his website if interested.

## BEM

And the last new thing appeared was BEM, stands for Block, Element Modifier.
It was created in 2009, then evoluated and had a long way to its popularity by now.

## Vitaly<br/>Harisov

This is one of the main authors. Vitaly Harisov. He works for Yandex and heads the
frontend development there.

## Sergey<br/>Berezhnoy

Another co-author is Sergey Berezhnoy, who also works for Yandex.
O was very lucky to work with them and be a member of the BEM team, so I can tell you
a little bit more about it today.

## BEM eco-system

Actually behind BEM there is a massive amount for JavaScript libraries, own template engine, many supplimentary tools.
Mosty these things are very local, but the CSS Methodology is a popular thing and becoming a standard all over the
world. So, I'll explain it in details.

## Harry & Nicolas

These 2 gentelmen are also important persons in the BEM community.
These are Harry Roberts from Britan and Nicolas Gallaher from USA. They had have a great role in BEM to be wide-spreaded
and become a standard.
Both are very famous developers and Harry is also the most wanted speaker for frontend conferences now.
So, if you are interested in their motivation of taking this approach, you can google for their blogs and social
networks accounts.

## BEM

* Block
* Element
* Modifier

## Interface

This is an ordinary web page, a web interface

## Interface of blocks

Header is also a block including others

## Everything is a block

Blocks are marked with classes in HTML

## Why not...?

Why not to use IDs?

## No IDs

Someday you will need to repeat the block at the same page

## Elements

## Elements markup

## CSS for an element

Elements have their own CSS classes. These classes are named so that it is clear which block the
element belongs to.
So, the idea is to encapsulate the components, its name becomes a kind of namespace and everything inside belongs to
this namespace.
Here dash-dash is used as a separator. Sometimes people use 2 underscores, but dash-dash looks like the most
common convention.

## Why not...?

Why not to use cascase?

## No cascade

Remember about non-determonostic matches
Poor little item does not know if it belongs to panels or to goods.
Making the selector more specific would not help, because we cannot rely on the document structure.

## Modified block

Components are similar visually and  functionally.
Good not to repeat ourselves but to reuse the code of the first component and provide some changes to it.

## Modifier

BEM answer to this question is a modifier.
With additinal CSS clas to a block you can provide more information about view.
You can see that both block class and modifier class sit together at the same node.

## CSS for a modifier

## Modified element

## Element's modifier

## CSS for an elements' modifier

Note that separators for element name and modifier name are different

## Why not...?

Why not to use a combined selector?

## Why not...?

And for element?

## No overspecific selectors

You would suffer when redefining


## BEM & CSS preprocessors

CSS preprocessors are --
This results in long BEM classes

## [getbem.com](http://getbem.com/)

## This is solved

* Scoping
* Specificity conflicts
* Non-deterministic matches
* Dependency management
* Removing unused code


So, this was about how the developers deal with component development in CSS now.
As you can see, CSS as a technology does not provide us a solution. So, we think up
our own way and recomendations how to use it.
But the reason of the need to use the metholodogy is drawbacks of CSS. And the right
way would be to fix the problems itself.

## Web Components

Here I introduce you another concept called Web Components. This is not the methodology but
a new technology, a new standard which will hopefully solve the problems we considered.

## Technologies behind

Web Components is not another language but some additions into already existing standards.
So, the additionas are:
- shadow DOM
- Custom elements in HTML
- HTML templates
- HTML Imports

I will show you in code what it all means.

## Web Components

These are a few pages I prepared for the lecture which demonstrate the concept.
Let's take a look into them one by one.

1. Video page
Open code
Inspect element
Switch on Shadow DOM
Shadow DOM is DOM behind the component. Video is native component.

2. Custom web component
We can write our own components.
HTML is just <my-button>
In Shadow DOM we can see more compex structure.
This is because we can tech the browser to deal with our custom component. This teaching
goes with JavaScript.
Take into account that styles are encapsulated.

3. Templates
Easier than describe everything in JavaScript

4. HTML imports
Everything about one components can be detached into an HTML file and then linked to the page.

## HTML import, library

With HTML imports you can create your own components and use them across different websites.
Or you can use someone else's components as a library.

## Are We Componentized Yet?

The concept is new and not all the browsers support.
But you can see the Polyfills column

## Web Components Polyfills

These are JavaScript additions which "teach" a browser to emulate the work of Web Components.
Add such a sript onto your page and you will be sure that the components work.

## Make it work

The same code, but with additional JavaScript

## Ready-made components


You can search for ready-made components. There is not that many of them, but
you can have some.

## Usage examples

I created a couple of examples about how the components can be used.

1. Toolbar
With linking the components simple code turns into more complex. Each element has its styles.

2. Goole Map
The component encapsulates JavaScript logic

This is all about web components

## SGDD

Whatever the approach we have chosen for developing the components, we also need
to organize the process of developing them and to have proper tools.
This is where style guide driven development goes. The last trend.

## Living Styleguides

Living styleguide is a UI book.
The components are not a part of a web page but are listed one by one.

## Style Guide Driven Development

When you start from a styleguide

## sc5-styleguide package

## SC5 Styleguide

http://styleguide.sc5.io

## Killer features

* {: .next }CSS / SCSS / SASS / LESS

Open the styleguide
Show that code compilates into the web site

* {: .next }Related variables

Show the variables in the interface. The context can be cropped.

* {: .next }Live editting

Editting teh variables.

* {: .next }Angular directives

Making Angular to work

* {: .next }Easy to integrate

Integrates with gulp

## How it works

## KSS Knyle Style Sheets

## Integration

Build the data

## Integration

Apply styles


## Integration

Watch the changes

## Development with SC5 Styleguide

* Living overview of UI
* Quick manual testing
* Quick built-out of new pages
* Unit tests for UI
* <b>Easier designer/developer/client collaboration</b>

In more details this can be studied at the website.

## Component development in CSS

* Big CSS
* BEM (SMACSS, OOCSS)
* Web Components
* SGDD

### [varya.me/component-development-css](http://varya.me/component-development-css/)

The topics covered:
- What is big CSS and indystry web interfaces, what are the problems it brings
- Modern approaches which are in use right now
- Had sneak peek to teh future touching web components
- The process of developing components starting with styleguide

I hope this was useful.
This is the link where you can find this presentation.

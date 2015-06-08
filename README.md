# Component Driven CSS

[Check out the presentation](http://varya.me/component-development-css/)

## Plan

1. Introduction
   What are you going lo learn
1. Industry needs
   What do you need when developing for big systems.
1. Component driven development. Why?
   1. Old-school frontend development cycle
   1. "Divide and rule"
1. What is hard with CSS
   1. What is CSS?
   1. What is difficult in CSS?
   1. What is really dificult in CSS?   
1. Dive into the problems
   1. Scoping styles
   1. Specificity conflucts
   1. Non-deterministic matches
   1. Dependency management
1. CSS methodologies
1. Web Components
   1. Polyfils and libraries 
1. Living styleguides
1. Summary

## Text

1. Introduction
   What are you going lo learn
1. Industry needs

   As computer sience students you probably know what is CSS. Do you?
   
   > Cascading Style Sheets (CSS) is a style sheet language used for describing the look and formatting of a document written in a markup language. "Wikipedia"
   
   CSS was designed to enable the separation of document content from document presentation. The specification was first published in 1996.
   
   Since then the inductry met a lot of new challenges and developers were looking for the solutions to them. Many ideas they came up were taken into work and are still used. Some evolved and became even better. A few went further and became new Web Standards.
   
   Today I will tell you what is CSS in the modern web industry. Indeed it help us a lot, but sometimes it brings new difficulties.

   First place which I know where the industry needs were explained and requirements to the resultant product were given is a book "Bulletproof Web Desing" by Dan Cederholm. It was first published in 2005 which is quite long ago for such a rapid evolving inductry.
   
   The idea is that HTML/CSS markup is not created once and forever. By 2005 industry needed it to be stable and mantainable.
   TODO: take photo from http://pepelsbey.net/pres/bem-ok/en/?full#dan-cederholm image from http://pepelsbey.net/pres/bem-ok/en/?full#11
   
   Industry needs are different from developin your cat's homepage. Usualy in industry they deal with
   * massive sites
   * big teams of developers
   * heavy UI
   * long running projects
   
1. Component driven development. Why?
   1. Old-school frontend development cycle
   1. "Divide and rule"
1. What is hard with CSS
   1. What is CSS?
   1. What is difficult in CSS?
   1. What is really dificult in CSS?   
   
   CSS was created to make text bold and links underlined. It ideally suited solving these problems. In many websites developers still use CSS like
   
   ```
H1 { color: blue }
P EM { font-weight: bold }
A:link IMG { border: 2px solid blue }
A:visited IMG { border: 2px solid red }
A:active IMG { border: 2px solid lime }
   ```
   Actually this code from [CSS level 1 specification](http://www.w3.org/TR/CSS1/). It is very simple, was recommended in 1996. Time passed and we met new chalenges.
   
   Writing CSS is easy. It is very easy to read and it is very likely that you can find the tricks you need at Stackoverflow. But architechting CSS is very difficult.
   
1. Dive into the problems
   1. Scoping styles
   1. Specificity conflucts
   1. Non-deterministic matches
   1. Dependency management
1. CSS methodologies
   1. OOCSS
      By Nicole Sullivan from Yahoo.<br/>
      She proposed OOP for CSS. This was a little bit naive but this was a first attempt.
   1. SMACSS
      Book by Jonathan Snook
   1. BEM
      Vitaly Harisov and Sergey Berezhnoy
      TODO: explain BEM, use `--` for modifiers
      TODO: link to getbem.com
      TODO: Explain that everything is easier with pre-processors
      Western people who popularize BEM are Harry Roberts and Nicolas Gallagher http://pepelsbey.net/pres/bem-ok/en/?full#harry-nicolas
1. Advanced BEM
   1. JavaScript
   1. Templating
   1. Building the project
1. Web Components
   The idea is that you can teach the browser how to deal with your custom components.
   1. Polyfils and libraries 
1. Style guide driven development
   1. Documenting CSS
   > Comments, comments, comments! "Harry Roberts"
   1. UI book of components
1. Summary

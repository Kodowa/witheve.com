---
title: "Literate Programming and Eve"
---

# Literate Programming and Eve

Through building Eve, we've found constant inspiration from the ideas of the 1970s and 80s, when what it meant to interact with a computer was still largely a question. Literate programming, a concept central to Eve, was an idea from this time that never fully gained traction, and remains today a largely unexplored yet potentially transformative direction for programming. Donald Knuth introduced literate programming in 1984 as an alternative perspective on the motivation of the programmer. In [his words][2]:

> The practitioner of literate programming can be regarded as an essayist, whose main concern is with exposition and excellence of style. Such an author ...  strives for a program that is comprehensible because its concepts have been introduced in an order that is best for human understanding, using a mixture of formal and informal methods that reinforce each other.

While some held the view that programming languages are a way to communicate with a computer, Knuth argued the opposite: the purpose of writing a program is to communicate with another human being; that the computer understands the language of the program is incidental. In this world, code is merely one artifact that makes up a program, the others being prose, illustrations, tables, charts, and any other artificat that we typically use to communicate ideas.

We gravitated toward the idea of literate programming because it fits so well with the ethos of Eve - it shifts the focus to people.

[IMAGE OF EDITORS]

## Fighting against our languages

Knuth invented literate programming to help him write a book. He married a markup language with a traditional programming language (in his case Tex, which he also invented for the purpose, and Pascal). Through a macro system, he circumvented the order imposed by the Pascal compiler, which allowed him to write code in an order that made narrative sense, and to express that narrative using rich text rendered from Tex source. From a single source file written in the style of literate programming, his toolchain generated a human-readable document and source ready to be consumed by the Pascal compiler.

This method solved his problem, but it has its drawbacks. First, it involves generating and keeping track of three files, instead of just a single source file for traditional programs. Second, to use this system you have to know three languages -- a markup language, a programming language, and a macro language to tie the two together. This also means that you have to deal with three syntaxes and three sources of errors. Finally, maintaining the documents was difficult. For example, if you spotted an error in the generated source code, the fix had to be made in the literate source.

While Knuth’s tooling was cutting-edge in 1984, his work only just began to reveal the potential in this direction of research. Unfortunately, today's literate programming systems remain faithful to Knuth's original toolchain, shortcomings included. It's not surprising, considering today’s most popular languages are still actively antagonistic toward the goals of literate programming (for example, most compilers still impose an order on source code). To write literate programming tooling today means facing the same barriers Knuth was trying to conquer 32 years ago.

## Improving on Old Ideas

We are advocating for the practice of literate programming becasue we believe it will lead to better, more maintainable programs. Yet we've encountered skepticism that literate programming is an idea with legs. Sure, it sounds good on paper, but in practice it hasn't lived up to its promises. This is certainly a valid viewpoint -- we can't argue that literate programming is a popular practice today. However, we're putting forth the argument that languages and tools built with a human-centric design focus can take literate programming much further than Knuth was able to given the tools of his time. Let's look at how Eve addresses some of the common arguments against literate programming.

### Many of the benefits of literate programming, like making programs more maintainable, are only appreciable after a considerable upfront investment.

It's true that literate programming requires more writing, most of which won't directly impact the execution of the program. When deadlines are tight and you have to get code out the door, you're not thinking about how frustrated you'll be in three months, when you have to revisit a rushed portion of code. What were you thinking when you wrote this? You don't know, and certainly no one else who reads your program will. But we're human, so we're biased to optimize for benefit now, rather than later.

Eve tries to reward the practice of literate programming with more upfront rewards. You can certainly write Eve programs without writing a single line of prose, but we hope the tools we provide are so useful, that you'll want to write prose just to take advantage of them. For instance, Eve programs use CommonMark to define a table of contents that can be used for navigation. By adding headers and dividing your program into sections, it not only becomes more readable, but also easier to navigate.

Similarly, the Eve editor lets you reorganize code for a particular purpose. Have two related blocks of code at different spots in the program? Elide all the other sections, isolating the program to only the sections you are care about. It's like code collapse on steroids. We've got much more planned on this front, but the goal is to encourage a literate programming mindset by making it a worthwhile endeavor in the short term.

As you leverage these short-term benefits of literate programming, we hope you'll also begin to see the long-term benefits as well. For instance, literate programming can help you think about your program more thoroughly. You can reveal edge cases, incorrect assumptions, gaps in understanding the problem domain, and shaky implementation details before any code is even written. Instead of explaining your code to a duck, explain it to yourself, or your colleague. If you can't, perhaps you need to revisit your assumptions. This can actually be a time-saver; instead of rushing to write incorrect code several times, slowing down and writing your thoughts and intent can help you get it right the first time.

### Tools that support literate programming are currently lacking in quality and quantity.

It's true that there aren't a lot of literate programming tools out there. Of the ones you can find, most of them follow Knuth's original designs from 1984. We've designed Eve with an emphasis on humane tooling, and literate programming fits naturally into this context. In Eve, you write prose in CommonMark, and code blocks in the Eve language. We chose CommonMark because it is very simple, with only a few piece of easy to learn syntax; and it produces source documents that are readable themselves. However, the Eve editor takes things a step further -- you don't even need to know CommonMark, as all prose formatting is accomplished through a WYSIWYG interface. This ensures that you'll never have to deal with CommonMark parsing errors.

On the program langauge side, Eve is a completely orderless language. This means we can write blocks of code in any order, and they are a valid program. In the context of literate programming, this means we don't need a a macro language to turn a literate program into something understandable by a compliler. We can render an Eve program as an editable document, or we can compile it to run as-is.

This architecture has far reaching consequences. It means we can render your program as a rich text document. You can edit that document in place, and see the changes in the program immediately, right next to the source. But even more interestingly, it means we can embed elements of your program _in_ the document itself, turning an ordinary document into a live, reactive document with updating values, charts, and visualizations. We're not sure the estent of the tools we can build for this kind of systen but we're eager to find out.

### The code is the truth of the program, so the prose and code will ultimately diverge, leading to prose that is actively misleading.

This argument is really about the fundamental role of a programmer. Our view is that a program is really a design document, a compilation of design decisions about the final program. As with all things design, the "who" and "why" are just as important as the "what" and "how". For instance, how could you find the bug in the following code without the accompanying comment?

```javascript
// Print every other line of the array to the console
for (var i = 0; i < myStringArray.length; i++) {
   console.log(myStringArray[i]);
}
```

This example shows how important intent is to a program. Yes, I can see that this block of code draws a button, but why does it do that? And who is the button for? The person who clicks on the button informs the label on the button. Is it an important button? That might determine its size and location. Reading a program with the "who" and "why" missing, is like reading a novel by only reading the dialogue. You might understand what's going on, and maybe you can piece it together with some effort. But you won't get the full picture, and it would have been easier just to read the author's words in the first place.

Comments provide one way for you to express your intent, but the exposition and presentation of ideas is just as important to communicate with an audience. Organization of ideas, graphics, charts, and supporting materials; cross-references, indexes, tables of contents -- these are all tools by which we communicate and understand ideas in other media, and they are just as important to the expression of ideas in a programming context.

From this perspective, inconsistencies between the code and the prose are themselves errors in the program, and should be treated as seriously as a buffer overflow.

## Programs for Humans

Literate programming is a first-class design concept in Eve. We will be writing all of our programs in this this manner, and will encourage others to do the same for the reasons above. Here are some example Eve programs:

- Quick start tutorial
- TodoMVC
- Flappy Eve
- Mobile application
- Tic Tac Toe

We'll also be writing Eve itself in the style of literate programming. Take a look at some components of the editor written in Eve:

- Analyzer
- View

If you’re curious to learn more about Eve, take a look at the following resources:

[1]: https://en.wikipedia.org/wiki/Literate_programming
[2]: http://www.literateprogramming.com/knuthweb.pdf
[3]: https://blog.bufferapp.com/science-of-storytelling-why-telling-a-story-is-the-most-powerful-way-to-activate-our-brains
[4]: http://www.perl.com/pub/tchrist/litprog.html

A study on the maintenance of literate programs
[5]: http://dl.acm.org/citation.cfm?id=2817507&dl=ACM&coll=DL&CFID=857994702&CFTOKEN=23309015

Literate programming on a team project
[6]: https://www.cs.princeton.edu/research/techreps/TR-302-91

Literate programming a practitioner's view
[7]: http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.365.8708


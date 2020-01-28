---
layout: post
title: "Why Python Should Be Your First Programming Language"
categories: [Languages, Python]
---

When someone asks what computer language they should learn first, I usually point them to **Python**. A first language should meet at least these criteria:

+ It should be a general-purpose language that a beginner can apply to different sorts of problems, rather than a special-purpose language that's only useful for a limited range of problems.
+ It should run on as many operating systems as possible rather than running on just one, so beginning programmers can learn and practice on whatever computer is at hand and can share their work with others regardless of platform.
+ It should manage memory automatically, rather than forcing beginners to worry about this onerous form of digital housekeeping.
+ It should be expressive (do a lot with a little code) rather than verbose (do a little with a lot of code), making it easier to read and write.
+ It should offer beginners a small number of approved ways of doing something rather than drowning them in options and possibilities.
+ It should have been thoughtfully designed and then refined over years of public use to minimize its quirks and inconsistencies, rather than being haphazardly designed and riddled with counterintuitive behavior and puzzling features.

Python meets all these criteria with room to spare.

But why is it a better beginner's language than any of the alternatives? To answer that, let's run through the most popular languages and look for reasons to reject each one, until only Python is left. Since that feels like kind of a *mean* approach, I'll also list some of Python's strengths and explain why I'd recommend it even if its competitors weren't all disqualified. 

Note that "Python" in this post always means Python 3 rather than Python 2. Both are in wide usage but Python 3 is a better language, is the way of the future, and is certainly the more sensible choice for new programmers.

Learning a computer language isn't a trivial undertaking. If you're going to invest all that time, you might as well learn a language that lots of other people use. It's easier to get a job if you know a language that's in demand, but it's also easier to find instructional materials, get help on the web, and talk to other people about your programming projects and problems. 

The most commonly cited ranking of programming language popularity is probably the [TIOBE Index](https://www.tiobe.com/tiobe-index/) (TIOBE is a Dutch company that tests software), which is based on the number of language-related queries people have made on Google, YouTube, Wikipedia, and other web sites.

In alphabetical order, here are the TIOBE Index's eleven most popular languages as of December 2019. I picked eleven because it's important to discuss Ruby, which didn't quite make it into the top ten this year.

+ C
+ C#
+ C++
+ Java
+ JavaScript
+ PHP
+ Python
+ Ruby
+ SQL
+ Swift
+ Visual Basic .NET

Using the criteria above, let's see which languages we can cross off the list.


### Special-purpose languages

**SQL** is only used for driving databases. This is a useful thing to know how to do, and most developers eventually learn the basics of SQL. But it isn't a general-purpose language and makes no sense as a first language.

**PHP** was created to power web pages. For example, when you enter your username and password on a website, it might well be a small PHP program that validates that info and lets you into the website. Since the language is most at home when embedded in web pages or powering a website from a back-end server, it feels like a fish out of water when you pull it out of that environment and try to use it as a general-purpose language. It's ungainly and keeps reminding you that it would rather be nestled in some warm, cozy HTML.


### Single-platform languages

Languages that run on lots of different operating systems are more useful than languages that only work on a single OS, for two reasons: you can practice programming on whatever computer is closest to hand, and you can share your work with other people regardless of what computer they use.
 
**C#** and **Visual Basic .NET** only run on Windows, unless you're willing to go through pretty severe contortions with results that are far from guaranteed. Anyway, C# is awfully close to Java, which runs on anything.

**Swift** only runs on iPhones and iPads. If your goal is to write iOS apps, Swift is your best bet. Writing a simple game that runs right on your iPhone can be a pretty exciting way to get your feet wet with programming. But for most people, it makes more sense to learn a first language that runs on Windows, macOS, and Linux computers instead of just portable iOS devices.


### Languages that force you to manage memory

The old stalwarts **C** and **C++** give you fine-grained control over the computer and run like greased lightning. But they also make you manually manage memory allocation and deallocation, which is a tedious, fiddly, error-prone task. This is a *huge* source of bugs and an unnecessary complication for people new to computer programming. Graduate to C or C++ later if you need more control or speed, but learning either as your first language is a surefire path to frustration and headaches.


### Languages that are unnecessarily verbose

For many years **Java** was the standard first language taught in universities. It's decent in that role, and there are certainly worse ways to learn to program. But Java lost some of its luster as a first language once we realized how much more effort it takes to do something in Java than it generally does in other languages. To use some specialized vocabulary, Java isn't as "expressive" as languages that can accomplish the same work in fewer lines of code. For example, printing `Hi there!` takes a whopping *five* lines of Java code:

```java
class Hi {
    public static void main(String[] args){
      System.out.println("Hi there!");
    }
}
```

Not only is this code verbose, it's also pretty opaque to someone who doesn't know Java. All the other languages we're still considering can do this same task with a single line of code, and even someone unfamiliar with those other languages can instantly understand what that code does. 

Java was the first language I used professionally and I still have a soft spot for it, but these days we have better options for first languages.


### Languages that offer too many ways to do something

It's tempting to think *flexibility* in a language -- having lots of ways to do a particular thing -- would be a great thing to look for in a language. It's not! It's easiest to learn programming languages that are opinionated about how programmers should use them. You want to be able to memorize a single command instead of memorizing a range of possibilities. This also makes it easier to recognize what other people are doing in that language when you read their code. This is a huge deal! 

**Ruby** gives you way too many options to program the way you want to, instead of insisting that you adhere to accepted standards. This disqualifies Ruby as a first language. People who love Ruby *really* love Ruby, but I find its refusal to pick one way to do things infuriating.

Here's an example. *These snippets all do exactly the same thing.*

```ruby
# snippet 1
if language == :swedish
  puts 'Hej världen!'
end

# snippet 2
if language == :swedish then puts 'Hej världen!' end

# snippet 3
puts 'Hej världen!' if language == :swedish
```

If that's not bad enough, consider that you could double the number of equivalent snippets by replacing each `if` and `==` with an `unless` and `!=`. 

For even more fun, double the number of snippets again by replacing each single quotation mark with a double quotation mark. 

And double it again by replacing `puts` with `print` and a new line character. 

Why stop now? Double it again by replacing `==` with `.eql?`. 

*That's forty-eight ways to write a simple conditional and print statement!* I rest my case.

(As an aside, I've fantasized for years about creating a radical subset of Ruby that strips out all these options and gives you only one way to perform common tasks. Ruby-minus-minus is a language I could get behind.)


### Languages that were designed in ten days

JavaScript got its start as a language to embed in web pages to give them extra functionality. It successfully replaced Flash as the technology of choice to make static web pages dynamic. Through supporting technologies like Node.js (which lets you run JavaScript programs outside of a web browser), JavaScript has branched out in new directions and is now a non-crazy choice for a general-purpose language. If your goal is to become a front-end programmer, it might be the only language you ever need to know.

But it's not the best first language to learn.

The reasons for this mostly stem from the fact that it really truly was [designed in ten days](https://thenewstack.io/brendan-eich-on-creating-javascript-in-10-days-and-what-hed-do-differently-today/). While that's an amazing accomplishment considering that JavaScript pretty much drives the entire web now, it's not a recipe for a clean, consistent, easy-to-learn language. JavaScript is filled with syntactic oddities, dangerous potholes, and things that you *can* do but really shouldn't. There are so many dark and frightening corners in the language that Douglas Crockford, one of its foremost practitioners and advocates, coined the term "the bad parts" to refer to the legal but unwise ways of using JavaScript. It's a confusing combination of programming paradigms and inconsistent behavior. 

Ready to see something truly marvelous? In JavaScript, `"123" + 1` should give some sort of error since it makes no sense to add a string of text to a number. But JavaScript says this equals `"1231"`. Well, OK, I guess JavaScript converts numbers to text, and then concatenates the text. So `"1231" - 1` would probably be `"123"`, right? Nope, JavaScript says it's `122`.   

I could go on about the perils of JavaScript as a first language, but I'll limit myself to one more complaint. As countless "Why I hate JavaScript" blog posts explain, the web is *littered* with bad JavaScript written by inexperienced developers who don't have the foggiest idea what they're doing. Looking at other people's code is just about the best way to learn a language -- *unless it's JavaScript*. Seriously, it's treacherous out there. There's legitimate debate about whether "elegant JavaScript code" is an oxymoron, but there's no debate about there being a staggering amount of barely functional, poorly structured, impossible-to-decipher code all over the web. Beware!


### And the winner is...

You already know the winner is Python. It might seem like I'm cheating here, considering that Python could have terrible characteristics of its own that would disqualify it just as resoundingly as any of the languages we've already looked at. But I claim that it doesn't. It's not a perfect language (I'm really tired of typing `self`), but it has a ton going for it. Here's how it stacks up to the disqualifying criteria listed above:

+ It's a general-purpose language that's been successfully used for robots, games, neural nets, and everything in between. This makes it immediately useful to people exploring computer programming for the first time.
+ It runs on Windows, macOS, Linux, iOS, lots of flavors of Unix, and just about any other platform you can think of. You can learn it on whatever platform you're already comfortable with. Whatever computer you're reading this post on almost certainly has Python installed already (unless it's a phone).
+ It automatically manages memory, so beginners have one less complication to worry about. 
+ It's about the most compact major language out there. Doing more in fewer lines of code makes it easy to learn and easy to read.
+ It usually allows or encourages one way of doing things. When there are multiple ways, senior coders often agree on what the most Pythonic way is. That's what new programmers should learn.
+ It's almost thirty years old and has undergone countless minor revisions and at least one major revision. Over the decades most of its rough edges have been polished off, making it simple and pleasant to learn and use.

In addition to the ways that it surpasses its competitors, it also has its own strengths:

+ It enforces consistent formatting by treating whitespace syntactically. This makes everyone's Python code looks reassuringly similar, and as a bonus it usually means fewer lines of code. For example, here's ugly but perfectly legal Java for declaring a class with three instance variables:

    ```java
    class 
  Foo {     int i = 1     ;
int j       = 2;                 int k =      3;
        
            }
    ```
    
    Knowing that the Java compiler will happily accept that fractured code makes your skin crawl, doesn't it? The same code in Python has no braces, relying on indentation to play the same syntactic role. You'd better format it correctly, or it won't work!
    
    ```python
class Foo:
    i = 1
    j = 2
    k = 3
    ```

+ It's fast enough. As a beginning programmer, you're not going to process billion-record data sets or write stock trading algorithms that rely on microsecond timing. Python has enough performance to deal with 99% of typical computer tasks. And there are techniques and tools (like PyPy or performance-optimized libraries) for speeding it up further if you ever reach that point.
+ There are countless Python-focused learning resources on the web.
+ There are great free IDEs, including [PyCharm](https://www.jetbrains.com/pycharm), [Visual Studio Code](https://code.visualstudio.com/), or [Wing](https://wingware.com).
+ It comes with a huge library of helper code for creating graphics and sound, networking with other computers, performing sophisticated math and statistics, interacting with databases, and doing just about anything else you might want to do with a computer program. If the standard library doesn't have what you need, there's an enormous ecosystem of free third-party libraries.

## Conclusion

In my mind, Python is the obvious choice for a first language for almost anyone. The only glaring exceptions are people who learn programming with a particular job in mind. If you're angling to become a database administrator, by all means go straight to SQL. If you want to work for a company that operates entirely on Windows, then C# or Visual Basic .NET are sensible places to start. But if you're just curious about programming and want to learn the fundamentals, there's no better way to start than by picking up a Python book, downloading a Python-aware IDE, and jumping in.

There's one other option I should mention. [Scratch](https://scratch.mit.edu) is a purely graphical language that teaches you to program by dragging and snapping together shapes instead of typing commands. In all honesty, this is a *fantastic* way to learn how to program, and 95% of what you learn with Scratch will apply directly to Python or any of the other languages in the TIOBE list. The problem with Scratch is that it's geared toward kids. Adults might be turned off by the bright colors and graphical approach, thinking that it must be a toy language. They're right in the sense that Scratch isn't used in professional settings because it only runs in a browser, but they're absolutely wrong to think that Scratch is a watered-down way to learn about programming. 

If you can get past the kid-focused look and feel, I strongly recommend that novice programmers learn the basics from Scratch and then move on to Python to put those basics into use with a more traditional language. You'll be amazed how much easier it is to learn Python (or any language) if you're already comfortable with Scratch.
 
Finally, I should point out that all the languages we've looked at subscribe to the "imperative" and/or "object-oriented" programming paradigms. These are far and away the most common families of programming languages, but they're not the only families out there. They are almost certainly the easiest paradigms to get started with, but if you find your interest in programming growing, you should consider exploring languages in the "functional" family (such as Clojure or Haskell) or the "logical" family (such as the wondrous Prolog, which is as close to magic as any technology I've ever worked with). Each programming language paradigm forces your brain to work in different ways, and it's fascinating to explore the wildly varying approaches required to solve the same problem using different paradigms.

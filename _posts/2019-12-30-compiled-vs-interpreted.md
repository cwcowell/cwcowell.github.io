---
layout: post
title: "Compiled vs. Interpreted Languages"
categories: [Ruby, Java, Python]
---

Computer languages are sometimes described as "interpreted" or "compiled." Beginning programmers might wonder what those terms mean, and which type of language they should learn. This post explains the difference and offers advice on whether a beginner should lean in either direction.


## Languages vs. Programs

As you'll see later, the terms "interpreted" and "compiled" refer not to any some intrinsic property of computer languages, but to how we normally run programs written in those languages. So although claims like "C is a compiled language" or "Ruby is an interpreted language" are common, they're not strictly accurate. Saying that "people usually run programs written in C by using a compiler" or "people usually run programs written in Ruby by using an interpreter" is more accurate. But because these sentences are wordier, people often use misleading shortcut expressions instead.

To recap: a computer language isn't inherently compiled or interpreted. But running programs written in that language will typically involve a compiler, an interpreter, or both, depending on the language. And because writing "Python is an interpreted language" is so much easier than writing "Programs written in Python are normally run with an interpreter," I'll use the shorter-but-not-entirely-accurate phrasing in this post.


## Computers Only Speak One Language

Under the hood, computers are monolingual. They only *natively* speak a language called "machine code," which isn't quite as cryptic as a string of 1s and 0s, but isn't far off. Different computers speak different dialects of machine code, depending on what CPU they use. For example, here's a snippet of machine code for the 6502 CPU that powered 80s-era home computers like the Apple II (borrowed from Richard Mansfield's [*Machine Language for Beginners*](https://www.atariarchives.org/mlb/)).

```
0398- A0 00    0451 LDY #$00 
039A- Bl BA    0460 LOOP LDA (L1L),Y
039C- F0 1C    0470 BEQ STOPLINE ; ZERO = LINE FINISHED
039E- CD 06 04 0480 CMP BASIC+6  ; SAME AS 1ST SAMPLE CHAR?
03Al- F0 04    0490 BEQ SAME     ; YES? CHECK WHOLE STRING
03A3- C8       0500 INY          ; NO? CONTINUE SEARCH
03A4- 4C 9A 03 0510 JMP LOOP
```

Notice that this code includes explanatory comments in English (to the right of the semicolons), but it's still hard to read and even harder to write. Since it's so difficult to deal with, almost no one writes computer programs in machine code.

Instead, we write programs in human-friendly languages like C, Java, or Python, and then use tools to translate those programs into equivalent machine code. That machine code is what the computer ultimately runs when when we tell it to run our program. This rest of this post describes the different ways that translation from your favorite language to machine code happens.

*A note on terminology:* I'll refer to code that's written in a human-friendly language as "source code" to distinguish it from the machine code that the computer knows how to run.

 
## Compiling

The simplest way to translate source code to machine code is to "compile" it. This means that you ask a tool called a compiler to inspect the code you wrote and make a whole new file that contains equivalent machine code. Then to run your program you don't execute the source code file, but instead execute the machine code file. 

For example, here's source code for the world's simplest C program:

```c
#include <stdio.h>
int main(void) 
{
    printf("Hello, world!\n");
}
```

As already mentioned, computers don't speak C. So if we save this source code in a file called `hello.c` and try to run it, we expect to--and do--get an error. (The first command below tells the computer that this file is a runnable program, even though it isn't really.)

```console
$ chmod a+x hello.c
$ ./hello.c
./hello.c: line 3: syntax error near unexpected token `('
./hello.c: line 3: `int main(void)'
```

Let's get around this problem by compiling our C program into machine code, a language the computer does speak. We'll use a tool called GCC (which stands for Gnu Compiler Collection), and we'll tell GCC to save the machine code in a new file called `hello-machine-code`.

```console
$ gcc hello.c --output hello-machine-code
```

Now we can run the machine code version of our program:

```console
$ ./hello-machine-code
"Hello, world!"
```

Just for fun, let's use a tool called `objdump` to peek inside the `hello-machine-code` file. We'd expect to see a bunch of machine code in there. And sure enough, look what shows up:

```
$ objdump hello-machine-code

00000000000004e8 <_init>:
 4e8:	48 83 ec 08          	sub    $0x8,%rsp
 4ec:	48 8b 05 f5 0a 20 00 	mov    0x200af5(%rip),%rax
 4f3:	48 85 c0             	test   %rax,%rax
 4f6:	74 02                	je     4fa <_init+0x12>
 4f8:	ff d0                	callq  *%rax
 4fa:	48 83 c4 08          	add    $0x8,%rsp
 4fe:	c3                   	retq

<remaining lines snipped>
```

This is only the first 8 lines of `hello-machine-code`. The whole file contains a whopping 180 lines of machine code, compared to 5 lines in the original C source code! This is another reason people write programs in languages like C instead of machine code: even trivial programs like this one are enormously long.

Now you know how to compile C source code into machine code. At least, you know the simplest possible way to do it. A tool like GCC has a million options for fine-tuning the machine code that it produces, and compiling a huge, professional software project might take multiple steps and several hours to complete, but the basic process remains the same.

Once you've compiled your source code into runnable machine code, you could in theory delete your source code -- it's no longer doing anything for you. But in practice, you should keep it around in case you need to add features, fix bugs, or otherwise change it in the future. Of course, each time you make any changes to the source code (no matter how minor!) you must compile it with GCC again so the executable machine code contains your changes.

You might be wondering how to compile languages other than C from source code to machine code. We'll look at that later. For now, let's on to the next approach to running human-readable code: interpreting it.


## Interpreting

Instead of using a tool like GCC to compile all your code at once before you run it, you can instead use a tool called an "interpreter" to compile each line *as it runs*. 

For example, consider this Ruby program, which you could paste into a file called `hello.rb`.

```ruby
print 'Hello '
print 'World'
puts '!'
```

The most common way to run Ruby programs like this is to use a Ruby interpreter that compiles the first line of Ruby to equivalent machine code, runs the machine code version of the first line of Ruby, compiles the second line of Ruby to machine code, runs the machine code version of the second line of Ruby, and continues in this way until the program exits.

So to run our `hello.rb` program, we skip any compilation step and instead just tell the Ruby interpreter to run our program.

```console
$ ruby hello.rb
Hello World!
```

Behind the scenes, here's what's happening in the Ruby interpreter:

1. Translate the first line (`print 'Hello '`) into equivalent machine code
1. Execute that machine code (so `Hello ` appears on the screen)
1. Translate the second line (`print 'world'`) into equivalent machine code
1. Execute that machine code (so `world` appears on the screen)
1. Translate the third line (`print '!'`) into equivalent machine code
1. Execute that machine code (so `!` appears on the screen)
1. Exit the program, since there are no more lines of Ruby source code to translate

Easy, right? Well yes, but there's a big downside to running a program with an interpreter. Compiling source code into machine code is computationally expensive (that means it's slow), and the interpreter has to compile each line of your program while the program is running. Result? Your program runs *really slowly*. 

I'm exaggerating: it probably runs plenty fast enough for most people most of the time, and in fact probably spends most of its time waiting for a slow human to enter input, or for data to be read from or written to a drive or a network connection. We use the expression "CPU bound" to describe a program that spends most of its time waiting for the CPU (whether the CPU is calculating math, compiling a single line of Ruby source code into machine code, or whatever). Most of the programs most of us run most of the time are not CPU-bound. This is all a complicated way of saying that although running a program with an interpreter is slower than running the same program with a compiler, it's probably not slower enough for you to notice or care.

There's another performance-related consideration: using an interpreter means you don't have to wait for the compiler to translate the whole program from source code to machine code before the program can start running. So although interpreted programs run more slowly than compiled programs once they're up and running, they *start running* a lot faster. This makes interpreted languages tons easier to debug or tweak, because you can see the results of your code changes immediately instead of having to wait through a potentially lengthy compile step first. And remember that it can take *hours* to compile  long, complicated programs.


## Combining Compiling and Interpreting

Some languages are designed to be run using a hybrid technique that uses both compiling and interpreting. For example, to run a Java program you first compile the Java source code using the `javac` command. Contrary to what I've said about compiling above, this step doesn't translate the source code into machine code, but rather to an awkward intermediate language called "Java bytecode," which is not quite understandable by humans but also not executable by computers (since computers only natively speak machine code). Then a Java interpreter (called the "Java Virtual Machine", or more commonly, "JVM") runs your program just like the Ruby interpreter we discussed in the section above: it compiles a single line of the Java bytecode into equivalent machine code, executes that machine code, and continues to work its way through the entire Java bytecode program in this way.

For example, here's the sample program from above written in Java, which you could paste into a file called `Hello.java`.

```java
class Hello {
    public static void main(String[] args) {
        System.out.println("Hello world!"); 
    }
}
```

To run it, first compile the Java source code into Java bytecode.

```console
$ javac Hello.java
```

Now run the Java bytecode with the Java interpreter (the JVM).

```console
$ java Hello
Hello world!
```

Just for fun, let's use the `javap` tool to peek inside the compiled Java program and inspect the Java bytecode.

```
$ javap -c Hello.class

class Hello {
  Hello();
    Code:
       0: aload_0
       1: invokespecial #1  // Method java/lang/Object."<init>":()V
       4: return

  public static void main(java.lang.String[]);
    Code:
       0: getstatic     #7  // Field java/lang/System.out:Ljava/io/PrintStream;
       3: ldc           #13 // String Hello world!
       5: invokevirtual #15 // Method java/io/PrintStream.println:(Ljava/lang/String;)V
       8: return
}
```

I don't know about you, but I can't say this makes a lot of sense to me even though I wrote the original source code. Fortunately, it not only makes perfect sense to the JVM, but it's also in a form that's easy for the JVM to interpret and execute very, very quickly.

At this point you might be baffled why anyone would want to combine the worst aspect of compiled programs (having to wait for the compiler to finish before you can run the program) with the worst aspect of interpreted programs (having to wait for each line to be compiled while the program is running, slowing the program down enormously). Rest assured there are good technical reasons for this odd hybrid approach, though those reasons are beyond the scope of this post. 

I will say that one of the reasons the hybrid strategy works at all is a technique called "Just-in-time compilation," more commonly known as "JIT." Let's look at that next.


## Just-In-Time Compilation

I lied a little when I described the hybrid approach to running Java programs. In the early days of Java, that's exactly how it worked, but the JVM has grown more sophisticated and now things are more complicated. To run a Java program with a modern version of Java, you still use the `javac` command to compile Java source code into Java bytecode. And you still use the JVM to interpret that Java bytecode, using the `java` command. 

But today's JVM does something very clever: it keeps track of track of which chunks of Java bytecode run most often (for example, a loop that runs over and over), and it does a uses a special high-tech strategy for compiling those pieces of source code. This "Just-in-time compilation" takes into account the surrounding source code, the values passed into it, and who knows what other technical considerations, and produces machine code that runs not just fast, but extra-super-ultra-fast. 

To increase speed further, the JVM's JIT compiler can make assumptions about the source code (for example, it might assume that a variable will never be set to a negative number), and if those assumptions turn out to be wrong, it can try a new compilation strategy on that piece of source code. 

Although fancy JIT compilation takes more time to perform than the plain compilation that happens during normal interpretation, in most cases the end result is a program that runs faster (usually *much* faster) overall. You'll see some hard numbers demonstrating the power of JIT in the next section.


## Can Any Language Be Compiled or Interpreted?
 
 *Note: this section refers to a program that finds prime numbers. You can see the code in Java, Ruby, and Python in [this post]({{ site.baseurl }}{% post_url 2019-12-22-prime-number-code %}).*
 
 I've given examples of running a compiled C program, running an interpreted Ruby program, and running a hybrid Java program. But are you limited in how you can run programs in a given language? For example, could you interpret a C program, or compile a Ruby program?
 
 The short answer is that these days things have gotten much muddier. There are sometimes several ways to run a program in a given language. However, there are definitely still *most common* ways of running programs in each language. For example, C, C++, Objective C, and Swift code is almost always compiled. Ruby, Python, Perl, and PHP code is almost always interpreted (with the caveat described below). Java, Scala, Clojure, and Kotlin code is almost always compiled to intermediate bytecode and then interpreted by the JVM, which also applies JIT compilation.
 
For example, you can run a Python program with JIT compilation by using the [Pypy](https://pypy.org/) interpreter instead of the standard Python interpreter. Pypy runs a prime number finder in about 20% of the time that the normal interpreter takes!

```console
$ python Primes.py 100000
finding 100000 primes
elapsed: 0:00:06.96

$ pypy3 Primes.py 100000
finding 100000 primes
elapsed: 0:00:01.51
```


Or you could run a Java program *without* JIT compilation by using a special `-Xint` option. This makes a prime number finder take 3 times as long!

```console
$ java Primes 100000
finding 100000 primes
elapsed: 1.053 seconds

$ java -Xint Primes 100000
finding 100000 primes
elapsed: 3.603 seconds
```

Or you could use the [TruffleRuby](https://github.com/oracle/truffleruby) Ruby interpreter, which compiles Ruby into an intermediate language that runs in a special virtual machine (which, for extra *Inception*-style complexity, can itself optionally run in the Java Virtual Machine). This is usually faster than the standard Ruby interpreter: the prime number finder runs with TruffleRuby in an astounding 9% of the time that it takes with the standard Ruby interpreter!

```console
$ rbenv local 2.7.0
$ ruby Primes.rb 100000
finding 100000 primes
elapsed: 8.611756718 seconds

$ rbenv local truffleruby-19.3.0
$ ruby Primes.rb 100000
finding 100000 primes
elapsed: 0.758 seccnds
```

As a final example of how complicated this landscape has become, you used to be able to use GCC (which we used to compile C above) to compile Java code directly into machine code before running it. For some reason this feature has been deprecated and is no longer available in modern versions of GCC, but old versions are still available on the internet.
 
 To restate the main point of this section: people often talk about a language being interpreted, compiled, or a hybrid, but the reality is that there are often lots of different ways to run a program no matter what language it's written in, and different types of programs might perform better when run with different techniques.
 
Having said all that, I'd feel guilty if I didn't admit that much of what I've said here about interpreters is a simplification. Pure interpretation is rare. What the standard interpreters for Python and Ruby (and other languages) actually do is *not* translate and execute a line at a time, as I claim above, but instead to do something similar to how Java works: they compile the source code into an intermediate, non-human-readable language, and then interpret *that*. And to confuse matters further, when they interpret the intermediate language, they often use JIT compilation! But computer programmers usually describe Python, Ruby, and their ilk as interpreted languages despite this technical wrinkle. This is because they *act* like interpreted languages to the end user: the initial compilation process happens automatically when you run a program in one of those languages, and it's so fast that it's essentially unnoticeable.
 

## Compiled, Interpreted, or Hybrid Languages for Beginning Programmers?

All else being equal, interpreted languages are easiest to get started with. Quick turnaround time between making changes to the code and seeing that code execute encourages experimentation. Snce beginners run their programs frequently as they learn and debug, the short startup time of interpreted languages reduces frustration and annoyance.

Having said that, if there are reasons to get started on a compiled language like C or a hybrid language like Java, go for it! Don't let the minor inconvenience of compiling scare you off. You'll spend far more time learning how to write correct, idiomatic code in C or any other language than you'll spend on running its compiler.


## Conclusion

We covered a lot of territory in this post. Let's recap the highlights.

+ Computers only speak one language: whatever dialect of machine code that is supported by their CPU.
+ Running a program with an interpreter is fast to start up but then runs slowly. However, it probably runs fast enough for you not to notice or care that it's slow.
+ Running a program with a compiler is slow to start up (because of the compilation step) but then runs quickly.
+ Running a program with a hybrid approach that blends interpretation and compilation (whether ahead-of-time, just-in-time, or both), and involves an intermediate language, is becoming the standard way of running programs in many languages. Similar to a pure compilation approach, this can be slow to get going but then runs quickly.
+ Real world use cases often involve a blending of all 3 techniques.
+ All else being equal, interpreted languages can be less annoying for beginners. But there are plenty of other considerations that are more important when picking a language to learn.

I should point out that there are exceptions to almost every claim in this post. For example, there are probably exotic, special-purpose computers in research labs whose machine code actually is a high-level language like Lisp or C, meaning that you could run programs written in those languages without either compiling or interpreting them. But for a beginning programmer, this should provide a true-enough picture of the different ways that computers run programs.

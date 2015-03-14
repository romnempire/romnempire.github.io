#What is Polymorphism?  14 March 2015

polymorphism is an irritating and complex term that comes up a lot in technical interviews, and also your introductory CS course.  It is also a powerful language feature in object oriented languages.  This is my explanation of polymorphism.

Lets assume you have an assembly program and a java program.  if you're approaching polymorphism for the first time, you probably don't know what assembly programming is.  a computer, at its core (and simplified a little), is a machine that knows how to perform a series of operations on bits stored in memory.  in order to make a computer do something, at some point you need to generate a list of operations you would like the processor to do and what sections of bits it should perform those operations on.  that list of operations is most easily represented by an assembly file.

now, most assembly languages (most processor families have their own) offer a powerful tool for abstraction and code reuse that stops the assembly file from just being a linear series of imperative commands.  this is THE SUBROUTINE, and lets say it looks like this.

    store $d, $0 #load 0 into register d
    JMP subroutine_meow # jump to subroutine_cat
    JMP subroutine_meow # do it again

    subroutine_meow:
        addi $d, $d, 1 

so now let's look at a java program with similar functionality.

    adder a;

    public interface adder() {
        public add(int i);
    }

    public class add1 implements adder() {
        public add(int i) {
            return i++;
        }
    }

    public class add2 implements adder() {
        public add(int i) {
            return i+2;
        }
    }

    public static void main(String[] args) {
        init();

        int i = 0;
        i = a.add(i);
        i = a.add(i);

    }

    public static void init() {
        a = new add1();
    }

so look this over and make sure it does basically the same thing as the assembly.  but there's a lot of bullshit in this that isn't in the assembly.  the add2 and the interface that are just not used.  also ignore the fact that adding one is literally one op so to make a subroutine for it is inefficient and contrived.

lets look at what is used and make some analogies.  what is similar?  if you take a moment to organize your thoughts so far and try to answer the question, it'll force you to think about the material in an abstract way which is good.  if you don't, then like whatever, keep reading.

now the method `add()` looks pretty similar to `subroutine_meow`, right?  it takes some code from main and sticks it somewhere else reusable.  so methods are kind of ilke subroutines.  now the instruction `JMP subroutine_meow` looks pretty similar to `a.add(i)`.  so a call to method is kind of like a jump operation.

now, what is different?  take a moment and think about this one again or dont.

in the java-ish code, i'm calling the method through an object.

now, by calling a method that's attached to an object rather than calling a method directly, i'm adding a layer of abstraction to the code that is redirectable.  whuzzat?  k so imagine the `init()` function looks like this:

    public static void init() {
        a = new add2();
    }

so now the method call `a.add(i)` is gonna do something pretty different.  it's gonna add 2.  k so like, what's the big deal?  who gives a shit?  okay, so there's a functional answer and a historical answer.  functionally, we just changed the behaviour of the line `i = a.add(i);` without changing the line, but instead by changing the underlying state within which that line was run.  that's huge.  it allows you to make even more reusable code because not only are your code blocks reusable because of methods, but also your calls to methods are reusable because of objects.  now historically, this represents a paradigm shift.  imagine you've been writing in assembly for god knows how long.  you are not going to be thinking, hey, this subroutine name that i'm jumping to... what would happen if it could mean multiple things, instead of just referring to the code block i gave a name?

so where did this shit come from?  k so there's this old asshole named alan kay whos pretty respectable and worth studying who baasically made up this 'object oriented' thing.  [link of relevancy](http://userpage.fu-berlin.de/~ram/pub/pub_jf47ht81Ht/doc_kay_oop_en).  He was thinking about bilology and cells and stuff and was like, hay so cells communicate by messages and each cell can respond to the same message differently so how can we replicate this in programming.  so at some level, object oriented design is a paradigm borrowed from nature which is like cool hippy shit, yo.  but it's also a good way to come up with new ideas.  ya seek inspiration from very different fields you know a lot of crap about.

anyways, lets define polymorphism.  polymorphism is when code is written in a general fashion so that a code block can be made to perform two different tasks depending on the underlying assumptions in which it is run.  now arguably this is too broad, because this definition includes the subroutine abstraction along with the object and generics abstractions that are typically mentioned in the definition of polymorphism, but fuck it i've written a lot of words here so whatevs.  this is all on github anyways, so you can bother me about it there if you've got a better idea.
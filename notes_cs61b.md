# 1 Java Crash Course

In what follows we are going to show you the basic syntaxes in **Java**, which will be used throughout the course cs61b. 

In theory, we can use any programming languages (even without a specific one) to talk about the data structures and algorithms, but it is better to use one, especially a modern and practical one. Java is such one! So here we go.

## 1.1 Hello World
Let's get started with the classic "hello world" program. In java, we code like this in the following:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello world!");
    }
}
```

Some syntatic features to notice:
- The program consists of a class declaration, which is declared using the keywords `public class`. In Java, all code lives inside of classes.
- The code that is run is inside of a `method` called main, which is declared as public `static void main(String[] args)`.
- We use curly braces `{` and `}` to denote the beginning and the end of a section of code. (*You can fell the difference from **Python***)
- Statements must end with semi-colons. (*In **Python** no worries for this huh?*)

## 1.2 Run it!
In order to run it, we need two "spells"---`javac` and `java`---by which we can run the `helloworld` program we just wrote above.

```
$ javac HelloWorld.java
$ java HelloWorld
Hello World! 
```

For further details about this process, we just show you this intuitive image and stop here. (*Keep on going and take a course on **compiler** if you are really interested.*)

![JavaComilingProcess](https://joshhug.gitbooks.io/hug61b/content/assets/compilation_figure.svg)

## 1.3 Variables and Loops
Let's look at this typical program, which prints the integers from 0 to 9. (*I believe you definitely have wrote a program like this in a course teaching programming.*)

```java
public class HelloNumbers {
    public static void main(String[] args) {
        int x = 0;
        while (x < 10) {
            System.out.print(x + " ");
            x = x + 1;
        }
    }
}
```

If you run this program you will see:
```
$ javac HelloNumbers.java
$ java HelloNumbers
$ 0 1 2 3 4 5 6 7 8 9 
```
But more importantly, there are more features you shall notice:
- The variable `x` cannot be used until it is declared. And in the declaration `int x = 0;` you can see `x` must be given a specific type. In this case, the type for `x` is `int`.
- Our loop definition is contained inside of curly braces, and the boolean expression that is tested is contained inside of parentheses.
- Notice here we use `System.out.print` instead of `System.out.println` to print outputs, for now the difference between them is simple:       
  - `println` **would add a new line** after printing the outputs you want, while `print` **would not**.


## 1.4 More basics

### 1.4.1 Conditionals
For conditional statements in Java, we just give a simple program which prints the absolute value of the variable `x`. (*Just a toy program to demonstrate what conditional structure looks like in Java.*)

```java
public static void main(String[] args) {
        int x = -100;

        if (x > 0) {
            x = x;
        } else if (x == 0) {
            x = 0;
        } else {
            x = -x;
        }

        System.out.println("abs of x is " + x);
    }
```

### 1.4.2 For loops
Programmers in the 1950s observed that it was very common to have code that featured initialization of a variable, followed by a loop that begins by checking for a termination condition and ends with an increment operation. Thus was born the `for` loop.

```java
public class ClassNameHere {
    /** Uses a basic for loop to sum a. */
    public static int sum(int[] a) {
      int sum = 0;
      for (int i = 0; i < a.length; i = i + 1) {
        sum = sum + a[i];
      }
      return sum;
    }
}

```

Here we defined a function called `sum`, which takes an `array` of integers and returns the sum of all its elements. And if you notice the keywords `public static`, just put your mind in rest and we will talk about it later.

#### **The enhanced For Loop**
Java also supports iteration through an array using an “enhanced for loop”. The basic idea is that there are many circumstances where we don’t actually care about the index at all. In this case, we avoid creating an index variable using a special syntax involving a colon.

For example, the code below:

```java
public class EnhancedForBreakDemo {
    public static void main(String[] args) {
        String[] a = {"cat", "dog", "laser horse", "ketchup", "horse", "horbse"};

        for (String s : a) {
            for (int j = 0; j < 3; j += 1) {
                System.out.println(s);
                if (s.contains("horse")) {
                    break;
                }                
            }
        }
    }
}
```

In this case, we do not create an index `i`. Instead, the String `s` takes on the identity of each String in `a` exactly once, starting from `a[0]`, all the way up to `a[a.length - 1]`.

## 1.5 Static Typing

As you may have noticed, a lot of `static` appear in the Java codes, and yes it is one of the most important features in Java --- **Static Typing**.

Java variables can contain values of that type, and only that type. Furthermore, the type of a variable can never change. One of the key features of the Java compiler is that it performs a static type check. For example, suppose we have the program below:

```java
public class HelloNumbers {
    public static void main(String[] args) {
        int x = 0;
        while (x < 10) {
            System.out.print(x + " ");
            x = x + 1;
        }
        x = "horse";
    }
}
```

compiling this program gives the message below:
```
$ javac HelloNumbers.java 
HelloNumbers.java:9: error: incompatible types: String cannot be converted to int
        x = "horse";
                ^
1 error
```
The compiler rejects this program out of hand before it even runs. This is a big deal, because it means that there's no chance that somebody running this program out in the world will ever run into a type error!

## 1.6 Objects
All code in Java must be part of a class (or something similar to a class, which we'll learn about later). So let's talk about an example of a class --- `Dog` class:

```java
public class Dog {
    public int weightInPounds; // an instance variable of Dog class

    // the Construcor of Dog class
    public Dog(int w) {
        weightInPounds = w;
    }

    // a Method of Dog class
    public void makeNoise() {
        if (weightInPounds < 10) {
            System.out.println("yipyipyip!");
        } else if (weightInPounds < 30) {
            System.out.println("bark. bark.");
        } else {
            System.out.println("woof!");
        }    
    }
}
```
- the **variable** (specifically, **instance variable**) `weightInPounds` inside of `Dog` class simply describes a "trait" of a "dog".
- the **function** `makeNoise` inside of `Dog` class simply defines what a "dog" can do. And we often call it a **method** instead of a funcion.
- the special `public Dog(int w)` means we have defined a **constructor** which would be invoked and set the variable when we create a `Dog`.

But the code above can't run itself because if you do, the compiler would yell at you and say something like:

```
$ java Dog
Error: Main method not found in class Dog, please define the main method as:
       public static void main(String[] args)
```

To fix that we can simply add a `main` method to it, **or** we create another `.java` file and write a so-called **client program** --- `DogLauncher`.

```java
public class DogLauncher {
    public static void main(String[] args) {
        Dog d;
        d = new Dog();
        d.weightInPounds = 20;
        d.makeNoise();
    }
}
```

Here we show how to really use that `Dog` class:
- We use `Dod d` to declare an instance `d` of `Dog` class, but you should notice, it is just *empty*, and does not contain anything yet!
- Then we use the keyword `new` to really create an instance, i.e., `new Dog()`, then we assigned it to `d`, thus `d` now contains an instance. In addition, when `new Dog()` happens, the constructor of `Dog` class would work right? But as you can see, there is no parameter passed to it, so actually the constructor we defined would not be invoked. But it turns out the Java provides a default constructor to deal with this so we do not have to worry about it.
- Notice that we use the **dot notation** to access the variables and methods of a class. (We call variables and methods of a class **members of a class**)

### Static v.s. Non-Static

#### Class Methods vs. Instance Methods
Java allows us to define two types of methods: 
- Class methods, a.k.a. static methods.
- Instance methods, a.k.a. non-static methods. 

Instance methods are actions that can be taken only by a specific instance of a class. Static methods are actions that are taken by the class itself. Both are useful in different circumstances. As an example of a static method, the `Math` class provides a `sqrt` method. Because it is static, we can call it as follows:
```java
x = Math.sqrt(100);
```
If `sqrt` had been an instance method, we would have instead the awkward syntax below. Luckily `sqrt` is a static method so we don't have to do this in real programs.
```java
Math m = new Math();
x = m.sqrt(100);
```

#### Static Variables
It is occasionally useful for classes to have static variables. These are properties inherent to the class itself, rather than the instance. For example, we might record that the scientific name (or binomen) for Dogs is "Canis familiaris":

```java
public class Dog {
    public int weightInPounds;
    public static String binomen = "Canis familiaris";
    ...
}
```

Static variables should be accessed using the name of the class rather than a specific instance, e.g. you should use `Dog.binomen`, not `d.binomen`. 

## 1.7 Reference and The Golden Rule of Equals(GRoE)

Okay, let's put it simple in this way, we declare two rough facts about the reference type and the assignment operator `=` :
1. Reference types hold the **bits of address** (*In that address, the actual content of that reference type is placed.*)
2. When you see an assignment, e.g., `x = y`, it just means **copyting the bits from y to x**. It also applies to the **Parameter Passing** when calling a method.

**P.S.** There are 8 primitive types: `byte`, `short`, `int`, `long`, `float`, `double`, `boolean`, `char`. Everything else, including **arrays**, is not a primitive type but rather a **reference type**.

**Example:** Suppose you have the following codes:
```java
Dog d = new Dog(20); // Instanialize a dog of 20 pounds and d holds it
Dog g = d; // Copyting the bits from d to g
g.weightInPounds = g.weightInPounds - 20;
```
Now think about the effects after the assignment using the facts above. The most crucial part is to really figure out what it means to copy the bits from d to g.

A intuitive way is to visualize it using a so-called **Box and Pointer** notation, here is an example:

![BoxandPointer](https://joshhug.gitbooks.io/hug61b/content/chap2/fig21/mystery_of_the_walrus_resolved_step3.png)

As you see, the `a` points to an instance of a class `Walrus`, which means something like `Walrus a = new Walrus(1000, 8.3)` happened before. For `b`, just like the **Example** above, it may be assigned before from `a`, i.e., `Walrus b = a;`.



# 2 Lists

From here we are gonna talk about data structures and algorithms, but for now we just aim to have a feeling for it using a simple example --- the **Lists**.

## 2.1 IntLists (*Naked Recursive Lists*)

To build a simple list ever, we can use the recursive definition of a list, which consists of two parts:
- the first value of the list, which we call `first`.
- the rest part of the list, which is also a list, called `rest`.

**P.S.** We would use `null` for the empty list which contains nothing.

Now we can create a IntList class using the definition above:

```java
public class IntList {

    /** Recursive definition of a list. */
    public int first;
    public IntList rest;

    /** Constructor for IntList. */
    public IntList(int f, IntList r) {
        first = f;
        rest = r;
    }
}
```

If we want to add elements to it, for example, if we want to add 5, 10, 15 to its back and add 5, 10, 15 to its front, we would just write code like this: (*a list I want is like this: 15->10->5->5->10->15*)

```java
// add 5, 10, 15 to its back
IntList L = new IntList(5, null);
L.rest = new IntList(10, null);
L.rest.rest = new IntList(15, null);

// add 5, 10, 15 to its front
L = new IntList(5, L);
L = new IntList(10, L);
L = new IntList(15, L);
```

As you can feel and see, it is trcky and kind of hard to read. For the moment, the `IntList` is hard to use too, well, we'll adopt the usual object oriented programming strategy of adding helper methods to our class to perform basic tasks.

### addLast
Yep, the first method came up in my mind is a method which would add an element to its back so we would never have to use the tricky 
`L.rest.rest = new IntList(15, null)` statements.

```java
/** Add an element with specific value in the back. */
public void addLast(int x) {
    if (rest == null) {
        rest = new IntList(x, null);
        return;
    }
    rest.addLast(x);
}
```

The method is recursive too when it comes to recursive definition as you feel it. The method `addLast` woule help us to avoid using the tricky and naked assignments. Instead we would just simply code like this:
```java
IntList L = new IntList(5, null);

// add elements to its back
L.addLast(10);
L.addLast(15);
```

It does look nicer and more readable. Now you may have the question: What about `addFirst` which add elements to its front? Well, after a rough thought we would have the following code:

```java
/** Naive attempt to add an element in the front. */
public void addFirst(int x) {
    this = new IntList(x, this); // I hope it works huh.
}
```

Though it may seem intuitive and straightforward, but it cannot be compiled otherwise you would get a message like this:
`The left hand side of an assignment must be a variable.`
Recall that the static features in Java, you might get a feeling and understand why Java chooses to do this. (*See [Discussion_about_this](https://stackoverflow.com/questions/7979623/why-is-assignment-to-this-not-allowed-in-java) for more discussions.*)

Now that we can't use keyword `this` to add an element to its front, is there any other ways to get around with this? Well, you actually can change the signature of `addFirst` method, more specifically, `public IntList addFirst(int x)`.

```java
/** Modified approach to addFirst. */
public IntList addFirst(int x) {
    return  new IntList(x, this);
}
```
Now we can use this method (*I promise!*), but it just looks a little bit different from what we have expected at first. (*Because deep down in my heart, I think adding element should not return anything, which is just a mutation. Of course in functional paradigm where mutation is not allowed, it is reasonable and good to do so. But here we are in Java World.*)

```java
// add elements in the front
list = list.addFirst(3);
list = list.addFirst(4);
list = list.addFirst(5);
```

***Remark.*** Having been through this you might have a solid feeling for the naked recursive list. It is inconvenient at least in Java's OOP world. But the good part is from the recursive list you can really exercise writing recursive methods, which is vital for you. So for the rest of `IntList`, we continue adding some more methods to `IntList` not only to make using it easier, but also to offer a chance to exercise.

### printList
We really need a method to show what a specific `IntList` looks like, so we add method `public void printLast()` to `IntList` class:

```java
public void printList() {
    /** Print all the elements in IntList recursively. */
    System.out.println(first);
    if (rest == null) {
        return;
    }
    rest.printList();
}
```

Although so far the implementations we made for the methods of `IntList` class have all been recursive, we can actually implement them iteratively too! (*Think about it and I'll just leave it to you as an exercise* :)

Now we have the following code for testing:
```java
public class ListLauncher {
    public static void main(String[] args) {
        
        // initialize a IntList
        IntList list = new IntList(1, null);

        // add elements in the back
        list.addLast(2);
        
        // add elements in the front
        list = list.addFirst(3);
        list = list.addFirst(4);
        list = list.addFirst(5);

        // print the list to test the functionality
        list.printList();
    }
}
```
Running it gives us the following output:
```
5
4
3
1
2
```

### size & iterative size
We'd like to add a method `size` to the `IntList` class so that if you call `L.size()`, you get back the number of items in `L`. And this time we are gonna do it both recursively and iteratively.

Here is the recursive `size`:
```java
/** Returns the size of the list. */
    public int size() {
        if (rest == null) {
            return 1;
        }
        return 1 + rest.size();
    }
```
But before coming to the iterative part, here is a subtle thing to ponder: *In the base case for recursion above, can we use* `this == null` *to be the criterion for the base case*?

To answer this question, you just simply think of a trivial case when `L == null`. It would just skip the base case and excute the `rest.size()` as we expected, but which would cause the `nullPointerException` beacause you cannot access anything from `null`.

For iterative size, we have the following:
```java
/** Iterative size method. */
public int iterativeSize() {
    int size = 0;
    IntList p = this;

    while (p != null) {
        size = size + 1;
        p = p.rest;
    }

    return size;
}
```
Recall that we cannot reassign `this`, thus in order to traverse the list, we need a `p` to do it. (*Remeber that* `this` *can be assigned to a variable, but the converse is impossible.*)

### get
While the `size` method lets us get the size of a list, we have no easy way of getting the ith element of the list. Now we write a method `public int get(int i)` which returns the ith element of the list. (*The* `i` *counts from 0 and for now you can ignore the index boundary*)

```Java
/** Get the ith element in IntList. */
public int get(int i) { 
    if (i == 0) {
        return first;
    }
    return rest.get(i - 1);
}
```

***Remark.*** Note that the method we've written takes linear time! That is, if you have a list that is 1,000,000 items long, then getting the last item is going to take much longer than it would if we had a small list. We'll see an alternate way to implement a list that will avoid this problem soon.



## 2.2 SLLists (*Single Linked Lists*)

Having done all the implementatins of `IntList` class above, it is true that as a **Naked Recursive Data Structure**, `IntList` is awkward to use and read, resulting further development based on it hard to organize and maintain. 

In order to use an `IntList` correctly, the programmer must understand and utilize recursion even for simple list related tasks. This limits its usefulness to novice programmers, and potentially introduces a whole new class of tricky errors that programmers might run into, depending on what sort of helper methods are provided by the `IntList` class. 

So, inspired by all this, we are going to build through a series of improvements a new class `SLList`, which much more closely resembles the list implementations that programmers use in modern languages.

### Improvement #1: Rebranding
Our first step will be to simply rename everything in `IntList` and throw away the helper methods in `IntList`. You may think it is not a big change, but trust me. Be patient and see the whole process step by step.

```java
// Rebranding new class IntNode
public class IntNode {
    public int item;
    public IntNode next;

    // constructor for IntNode
    public IntNode(int i, IntNode n) {
        item = i;
        next = n;
    }
}
```

### Improvement #2: Bureaucracy
Knowing that `IntNodes` are hard to work with, we're going to create a separate class called `SLList` that the user will interact with. The basic class is simply:

```java
// Seperate class that interact with users --- SLList
public class SLList {
    public IntNode first;

    // Constructor for SLList
    public SLList(int x) {
        first = new IntNode(x, null);
    }
}
```

Already, we can get a vague sense of why a `SLList` is better. Compare the creation of an `IntList` of one item to the creation of a `SLList` of one item.
```java
IntList L1 = new IntList(5, null);
SLList L2  = new SLList(5);
```
See? The `SLList` hides the detail that there exists a `null` link from the user. The `SLList` class isn't very useful yet, so let's add an `addFirst` and `getFirst` method as simple warmup methods.

#### addFirst & getFirst
These two methods are pretty straightforward if you understand what is going on in `IntList` and the structure of `SLList`.

```java
/** Adds an item to the front of the list. */
public void addFirst(int x) {
    first = new IntNode(x, first);
}    

/** Retrieves the front item from the list. */
public int getFirst() {
    return first.item;
}
```

You can see that `addFirst` in `SLList` is more cleaner and nicer than that in `IntList`. Of course it cleaner and easier to use them, see the comparisons:
```java
// For IntList
IntList L = new IntList(15, null);
L = new IntList(10, L); // the naked add
L = L.addFirst(5); // the helper method add but not nice
int x = L.first; 

// For SLList
SLList L = new SLList(15);
L.addFirst(10);
L.addFirst(5);
int x = L.getFirst();
```

Comparing the two data structures visually, we have: (with the `IntList` version on top and `SLList` version below it)

![VisualComparisonsIntandSL](https://joshhug.gitbooks.io/hug61b/content/chap2/fig22/IntList_vs_SLList.png)

Essentially, the `SLList` class acts as a middleman between the list user and the naked recursive data structure.


### Improvement #3: Public vs. Private
Unfortunately, there is still a subtle fatal flaw in `SLList`. A programmer can easily modify the list directly, without going through the `addFirst` method provided by the middleman, for example one can easily write codes like this:

```java
SLList L = new SLList(15);
L.addFirst(10); // this is good
L.first.next.next = L.first.next; // But this is horrible!!!!
```

This code would cause an infinite loop in the list, like the visual image would show:

![rawwrite](https://joshhug.gitbooks.io/hug61b/content/chap2/fig22/bad_SLList.png)

To deal with this problem, we can modify the `SLList` class so that the first variable is declared with the `private` keyword.
```java
public class SLList {
    private IntNode first; //hiden from the outside
...
```
Private variables and methods can only be accessed by code inside the same `.java` file, e.g. in this case `SLList.java`. By contrast, any code inside the `SLList.java` file will be able to access the first variable. 

***Remark.***
- It may seem a little silly to restrict access. After all, the only thing that the `private` keyword does is break programs that otherwise compile. However, in large software engineering projects, the `private` keyword is an invaluable signal that certain pieces of code should be ignored (and thus need not be understood) by the end user. Likewise, the `public` keyword should be thought of as a declaration that a method is available and will work forever exactly as it does now.
- As an analogy, a car has certain `public` features, e.g. the accelerator and brake pedals. Under the hood, there are `private` details about how these operate. In a gas powered car, the accelerator pedal might control some sort of fuel injection system, and in a battery powered car, it may adjust the amount of battery power being delivered to the motor. While the private details may vary from car to car, we expect the same behavior from all accelerator pedals. Changing these would cause great consternation from users, and quite possibly terrible accidents.
- **Thus, when you create a public member (i.e. method or variable), be careful, because you're effectively committing to supporting that member's behavior exactly as it is now, forever.**

### Improvement #4: Nested Classes
At the moment, we have two `.java` files: `IntNode` and `SLList`. However, the `IntNode` is really just a supporting character in the story of `SLList`. 

Java provides us with the ability to embed a class declaration inside of another for just this situation. The syntax is straightforward and intuitive:

```java
public class SLList {
    public class IntNode {
        public int item;
        public IntNode next;
        public IntNode(int i, IntNode n) {
            item = i;
            next = n;
        }
    }

    private IntNode first; 

    public SLList(int x) {
        first = new IntNode(x, null);
    } 
...
```

Having a nested class has no meaningful effect on code performance, and is simply a tool for keeping code organized. 

If the nested class has no need to use any of the instance methods or variables of `SLList`, you may declare the nested class `static`, as follows. Declaring a nested class as `static` means that methods inside the static class can not access any of the members of the enclosing class. In this case, it means that no method in `IntNode` would be able to access `first`, `addFirst`, or `getFirst`.

```java
public class SLList {
    public static class IntNode {
        public int item;
        public IntNode next;
        public IntNode(int i, IntNode n) {
            item = i;
            next = n;
        }
    }

    private IntNode first;
...
```

This saves a bit of memory, because each `IntNode` no longer needs to keep track of how to access its enclosing `SLList`.

Put another way, if you examine the code above, you'll see that the `IntNode` class never uses the `first` variable of SLList, nor any of `SLList`'s methods. As a result, we can use the `static` keyword, which means the `IntNode` class doesn't get a reference to its boss, saving us a small amount of memory.

#### addLast() & size()
To motivate our remaining improvements and also demonstrate some common patterns in data structure implementation, we'll add `addLast(int x)` and `size()` methods.

```java
/** Adds an item to the end of the list. */
public void addLast(int x) {
    IntNode p = first;
    while (p.next != null) {
        p = p.next;
    }

    p.next = new IntNode(x, null);

}

/** Returns the size of the list by iteration. */
public int iterativeSize() {
    IntNode p = first;
    int totalsize = 0;

    while (p != null) {
        totalsize += 1;
        p = p.next;
    }

    return totalsize;
}

/** Returns the number of items in the list using recursion. */
public int size() {
    return size(first);
}

/** Helper method for recursive method size(). */
private static int size(IntNode p) {
    if (p.next == null) {
        return 1;
    }

    return 1 + size(p.next);
}
```
A few things to add:
- For the recurive `size` method, the recursive call for `size` in `IntList` was straightforward: `return 1 + this.rest.size()`. For a `SLList`, this approach does not make sense. A `SLList` has no `rest` variable. Instead, we'll use a common pattern that is used with middleman classes like `SLList` -- we created a `private` helper method that interacts with the underlying naked recursive data structure. (*An alternate approach is to create a non-static helper method in the `IntNode` class itself. Either approach is fine, though I personally prefer not having any methods in the `IntNode` class.*)
- Here, we have two methods, both named `size`. This is allowed in Java, since they have different parameters. We say that two methods with the same name but different signatures are **overloaded**.


### Improvement #5: Caching
Consider the `size` method we wrote above. Suppose `size` takes 2 seconds on a list of size 1,000. We expect that on a list of size 1,000,000, the `size` method will take 2,000 seconds, since the computer has to step through 1,000 times as many items in the list to reach the end. Having a `size` method that is very slow for large lists is unacceptable, since we can do better.

It is possible to rewrite size so that **it takes the same amount of time, no matter how large the list**. To do so, we can simply add a `size` variable to the `SLList` class that tracks the current size, yielding the code below. This practice of saving important data to speed up retrieval is sometimes known as **caching**.

```java
public class SLList {
    ... /* IntNode declaration omitted. */
    private IntNode first;
    private int size;

    public SLList(int x) {
        first = new IntNode(x, null);
        size = 1;
    }

    public void addFirst(int x) {
        first = new IntNode(x, first);
        size += 1;
    }

    public int size() {
        return size; // very fast size method
    }
    ...
}
```

This modification makes our `size` method incredibly fast, no matter how large the list. Of course, it will also slow down our `addFirst` and `addLast` methods, and also increase the memory of usage of our class, but only by a trivial amount. In this case, the tradeoff is clearly in favor of creating a cache for size.

### Improvement #6: The Empty List
So far our `SLList` has improved a lot, compared to the old `IntList`:
- Users of a `SLList` never see the naked `IntNode` class.
  - Simpler to use.
  - Cleaner and more efficient `addFirst` method.
  - Avoid direct use of the `IntNode` class.
- Faster `size` method

Another natural advantage is that we will be able to easily implement a constructor that creates an **empty list**. The most natural way is to set `first` to `null` if the list is empty. This yields the constructor below:
```java
public SLList() {
    first = null;
    size = 0;
}
```
Unfortunately, this causes our `addLast` method to crash if we insert into an empty list. Since `first` is null, the attempt to access `p.next` in `while (p.next != null)` below causes a **null pointer exception**.

```java
public void addLast(int x) {
    size += 1;
    IntNode p = first;
    while (p.next != null) {
        p = p.next;
    }

    p.next = new IntNode(x, null);
}
```

### Improvement #6b: Sentinel Nodes
One natural solution to fix `addLast` is to create a special case for the empty list, as shown below:
```java
public void addLast(int x) {
    size += 1;

    // special case for empty list
    if (first == null) {
        first = new IntNode(x, null);
        return;
    }

    IntNode p = first;
    while (p.next != null) {
        p = p.next;
    }

    p.next = new IntNode(x, null);
}
```

This solution works, but special case code like that shown above should be avoided when necessary. Human beings only have so much working memory, and thus we want to keep complexity under control wherever possible. For a simple data structure like the `SLList`, the number of special cases is small. More complicated data structures like trees can get much, much uglier.

A cleaner, though less obvious solution, is to make it so that all `SLLists` are the "same", even if they are empty. We can do this by creating a special node that is always there, which we will call a **sentinel node**. The sentinel node will hold a value, which we won't care about.

For example, the empty list created by `SLList L = new SLList()` would be as shown below:

![EmptyListwithSentinelNode](https://joshhug.gitbooks.io/hug61b/content/chap2/fig22/empty_sentinelized_SLList.png)

And a `SLList` with the items 5, 10, and 15 would look like:

![NonEmptyListwithSentinelNode](https://joshhug.gitbooks.io/hug61b/content/chap2/fig22/three_item_sentenlized_SLList.png)

In the figures above, the lavender `??` value indicates that we don't care what value is there. Since Java does not allow us to fill in an integer with question marks, we just pick some abitrary value like -518273 or 63 or anything else.

Since a `SLList` without a sentinel has no special cases, we can simply delete the special case from our addLast method, yielding:

```java
// Free from special case with sentinel node
public void addLast(int x) {
    size += 1;
    IntNode p = sentinel;
    while (p.next != null) {
        p = p.next;
    }

    p.next = new IntNode(x, null);
}
```

As you can see, this code is much much cleaner!

#### Invariants
An invariant is a fact about a data structure that is guaranteed to be true (assuming there are no bugs in your code).

A `SLList` with a sentinel node has at least the following invariants:
- The `sentinel` reference always points to a sentinel node.
- The front item (if it exists), is always at `sentinel.next.item`.
- The `size` variable is always the total number of items that have been added.

Invariants make it easier to reason about code, and also give you specific goals to strive for in making sure your code works.



## 2.3 DLLists (*Doubly Linked Lists*)
So far, we have built the `SLList` class, which is far way better than the trick naked `IntList` in the first place. But we have a few more considerations to take account for, let's get started.

#### addLast
Consider the `addLast` method in `SLList` class:
```java
public void addLast(int x) {
    size += 1;
    IntNode p = sentinel;
    while (p.next != null) {
        p = p.next;
    }

    p.next = new IntNode(x, null);
}
```
Although it is free from annoying special cases, it still has a problem: *It is slow.* For a long list, the `addLast` method has to walk through the entire list, much like we saw with the `size` method without caching earlier. 

Similarly as the case in `size` method, we can attempt to speed things up by adding a `last` variable, to speed up our code, as shown below:

```java
public class SLList {
    private IntNode sentinel;
    private IntNode last;
    private int size;    

    public void addLast(int x) {
        last.next = new IntNode(x, null);
        last = last.next;
        size += 1;
    }
    ...
}
```

![SLListwithLast](https://joshhug.gitbooks.io/hug61b/content/chap2/fig23/sllist_last_pointer.png)

But after a deeper thought, despite of acceleration of speed of `addLast` and `getLast` methods, if we had a `removeLast` method, this method would be still pretty slow. The reason is that we have no easy way to get the second-to-last node, to update the last pointer, after removing the last node.

#### SecondToLast
Now the issue here is a method that removes the last item in the list will be inherently slow. This is because we need to first find the second to last item, and then set its next pointer to be `null`. Adding a `secondToLast` pointer will not help either, because then we'd need to find the third to last item in the list in order to make sure that `secondToLast` and `last` obey the appropriate invariants after removing the last item.

### Improvement #7: Looking Back
The most natural way to tackle this issue is to add a previous pointer to each `IntNode`, i.e.
```java
public class IntNode {
    public IntNode prev;
    public int item;
    public IntNode next;
}
```
In other words, our list now has two links for every node. One common term for such lists is the "Doubly Linked List", which we'll call a `DLList` for short. This is in contrast to a single linked list from an `SLList`.

The addition of these extra pointers will lead to extra code complexity. You can see from the visualization, the following box and pointer diagram below shows more precisely what a doubly linked list looks like for lists of size 0 and size 2, respectively.

![DLListsize0](https://joshhug.gitbooks.io/hug61b/content/chap2/fig23/dllist_basic_size_0.png)

![DLListsize2](https://joshhug.gitbooks.io/hug61b/content/chap2/fig23/dllist_basic_size_2.png)


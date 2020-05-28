Notes from Ultimate Go --

**1.1 Prepare Your Mind**
Lines of code really can effect how healthy a project is, how healthy a team is. I want to move away from being impressed with projects with large amounts of code.

We were taught to create large abstarctions in our codebase to deal with change... this is something we also need to get rid of... all we're doing is add more code to our project which causes more pain.

We want thin layers of decoupling and still achieve ability to deal with change

Mechnanical Sympathy--
If performance matters, and it does, then its the hardware that matters. Performance comes from the hardware, nothing else. So we either need to be sympathetic to the hardware, or not. The hardware is the platform at the end of the day if performanc ematters.

Engineering is about understanding cost. Every decision has a benefit and cost. 

Engineering is about undersatning the costs you are changing. If you don't you're not engineering, you're hacking.

These are problems Go is trying to solve.

You can't throw more hardware at the problem... you can't throw more cloud computing at the problem, it's expensive. We want our software to minimize the use of resources to keep costs down.

You can't throw more developers at a problem. 

Go package structure could help with having multiple developers on the same project in a productive way.

Self reflect about who you are as a developer. What is my philosophy. WHat's driving my engineering decisions.

We're going to break you down and build you back up. 

Go has different costs, so you have to make different decisions. (**interesting thought that different languages ahve different cost considerations)

Ask yourself --- What is the legacy you're bringing behind?

I think history is really important (** really useful)

Good quotes about Legacy software

Hollywood should write a movie about legacy software systematically failing across the planet and nobody has any idea what to do because there's no unit testing.

I really believe legacy code will be the downfall of our civilization.

TITLE -- Legacy Code will be the downfall of civilization

THink about the person that would have to maintain code after you.

HOw to avoid creating legacy coe out of the box -- keep mental models of the code. 

A ream of copy paper is 10,000 lines of code.

The average developer can't maintain a mental model of code beyond that 10,000.

Meaning you know where everything in that code is... you understand the codebase intimiateyl enough that if there is a problem you know where to go in that code and start looking.

You want to keep a 10,000 to 1 developer balance.

If you're clever when you write it, how are you going to debug it?

I never allow developers on my team to use a debugger without permission... because in production all you'll have is your code and the logs you're keeping.

I have a 20 minute rule that says... leverage your metnal models, leverage your logging to find the bug. If you can't do that, we'll turn on the debugger. But we've got a refactoring problem here.

Create logs with more signal than noise.

**1.2 Productivity vs Performance**

We put people on a pedestal for hsaving microseconds off an algorithm, but I want really to focus on productivity.
Niklaus WIth said in 1987 developers think hardware will save software developers.
The hardware is the platform, we have to have mechanical sympathy with the hardware systems.
Hardware folks really haven't changed the hardware in 15 years. Great hardware sounds great but if we don't udnerstand the hardware and engineer for it, crazy new hardware can actually slow us down, not speed us up.
(Developers are blowing it)

Go's model is not a virtual machine, it's the real machine.

**1.3 Correctness versus Performance**

We want to write code optimized for correctness. Clever code optimizes for performance.
Lack of performance will come from four places:
1. Latency-- I/O, networking, disk I/O. That's a real killer, focus on thsi first
2. Memory allocations -- can cause performance problems... garbage collector impoortant here. We ask is it fast enough, not the fastest
3. How efficiently you access data
4. Algorithm effiencies -- we tend to focus on that piece for performance... the reality is the hardware will be so fast if we solve the first three. 

That's what is meant by optimizing for correctness.

Listen to the history, these are people that already learned these lessons from mistakes. Engineering isn't about the perfect solution, but cost tradeoffs.

We're one of the only industries where we ask people to write code before we teach them how to read.

This class is all about our ability to READ CODE.

Problems can usually be solved with mundane solutions.

If you're a backend developer your software should be working 24 hrs without issues. Nobody should know your name if you're doing your job well. If they know your name something went wrong. I build systems to the point nobody knows I exist... that's a good day in the office.

**1.4 Code Reviews**
Our number one priority must be integrity. If that's not your number one, you can't work for me.

If cell phones around the US stop workng for the next hour, how many people lose their lives? The answer is not zero. (DEEP SHIT)

Software is serious business.

People's lives and happiness are dependent on technology you're building.

At the macro level, every line of code allocates memory, reads memory, and writes to memory.

All we are doing in code is reading and writing integers to memory.

ALl those reads and writes cause eveyrthing we see 

At a micro level those reads and writes must always be correct and precise

What we do every day is solve data transformation prblems.

Data-Oriented design: fi you don't udnerstand the data you don't understand teh program.

Data-Oriented design is a framework as opposed to object-oriented design

As a software developer, you are a data scientist... you're working with data, transforming data on a daily basis. If you don't understand the data you don't understand the problem.

Integrity comes in two places at macro level:
Lines of code is critical. The average developer can't maintain a mental model of more than 10,000 lines of code. As projects get larger, we need more devleopers.

FOr every 1000 lines of code the average developer created 15 to 50 bugs.

Meaning in the worst case you're adding a bug every 20 lines. Always keep that in mind.

If you have more code than you need, there's more places for bugs to hide.

*Error Handling*

The majority of code you write is focused on failure, not the best case.

A study done on critical software, including Redis, showed 92% of bugs/failures came from bad error handling that was better and more focused.

Readability is number two to integrity.
Readability means your software must be comprehensible... focus on the average developer. The average developer on your team should be able to read every line of code, have a full udnerstanding of the mental models, and fix every bug that comes up.

Think of your team... are you the average developer on the team? Do you have the full mental model? Can you solve any bug that arises?

Above average coders have a responsibility not to write clever code the average developer can't udnerstand. If you're below average you have a responsibility to get up to average. 

An above average coder may need to be less clever... over cleverness can cause more problems on a team even than those that are below average.

Readability also means not hiding the cost of the code you're writing.

Some language features hide costs. Go doesn't have those features.

Remember we are focusing on the real machine. We want the developer to always know the costs they're taking.

Simplicity comes after Readability... simplicity is about hiding complexity. Simplicity is hard to design and complicated to build.

Simplicity is not something you do day one, it's something you refactor into.

Complexity sells better than simplicity.

So the order of importance is:
1. Integrity
2. Readability
3. Simplicity

Don't hide cost, hide complexity.

# Lesson 2: Language Syntax

## 2.1 -- Variables

Type is everything, Type is life. Without type, we can't have integrity and understand the costs of our program.

The same bit pattern can represent an infinite number of things depending on type-- 00001010 could be the number ten or color Red or many other things

Built in types, numerics, strings and bool... int, float64, string, bool...

The name float64 tells us both parts of the type-- 64 tells us it's an 8-byte or 64-bit value (that's our cost/memory footprint) and float tells us it's IEEE754 binary decimal. 

A bool is one byte that only needs one bit (on or off)

There are precision based integers... but if I saw you using one and it wasn't obvious why, that would raise a flag during a code review.

Most the time we will just use int, which seems confusing because it only gives us half the type info. Regardless of how much bytes we use, we know it will represent an integer value.

How much memory space will an int use? Depends on the architecture you're using... most will be using AMD64, a 64-bit architecture.

Since we're on a 64-bit architecutre, then the pointer/address size is 64-bits or 8-bytes.

Our generic word size (a value that can chagne size depending on architecture) is 64 bits in a 64-bit architecture.

The Go Playground is a single-threaded environment... also an AMD64 P32 architecture... means addresses are 32-bits on this archiecture... the address scheme is 4-byte or 32 bits, meaning its basically a 32-bit architecture.

By defaault we have our integer size follow the average word size of the architecture. It will be better or worse dpending on the architecture... by using int we allow the architecutre to choose (mechanical sympathy)

There's a concept called zero value, and it's very important. It's an integrity play... the cost of integrity is performance, but we'll never use it.

All memory we allocate must get set to it's zero value at least once. 

If I'm going to declare a value and set it to its zero value state, I will use var. Var gives us zero value 100% of the time in this language.

Type string... strings are made up types in any language... in go strings are unique... the zero value for a string is called an Empty String... in Go, strings are a two-word data structure where the first word is a pointer and the second word is a number of bytes. 

YOu may not always want to initilizae to zero... you can use the short variable declarition to declare and initilize at the same time. (this is the := walrus operator)

The string hello would look like an array of 5 bytes, a word storing a pointer to the array, and a word that stores the info that our array is 5 bytes

Go doesn't have casting, it has conversion. Conversion means we may be taking a memory cost as we convert one type to another.

## 2.1 Struct Types

We don't creat objects in Go, we create values

How much memory is assigned for a struct type?

You might think you just add up the size of the types within it... but the issue is you have something called alignment, which is how the hardware manages stuff.

Alignments make sure all values, wherever they are, fall within word boundaries...

That leads to a need for padding within structs

Padded bytes are used to make sure types are aligned where they need to be to ensure no value stretches across two words.

A struct must also align based on its largest field.

You could optimize a struct by laying out fields from largest to smallest... this is a red flag (pre optimization) unless you havea  memory porfile indicating you should change it... it's better to optimize for correctness (readability, group things logically) rather than optimization

Implicit conversion has caused a tremendous amount of pain in software over the decades... especially when one type is a signed int and the other is an unsigned int ... can cause data corruption

A function in go is a value, not a type

## 2.3 -- Pointers Part 1 (Pass by value)

Everything in Go is pass by value... What You See Is What You Get (WYSIWYG)

Threads are a path of execution at teh Operating System layer

THe OS schedules threads

There's three areas of memory important here... the data segment, stacks, and heaps. Data reserved for global variables etc

The stack is a data structure that every thread is given

At the OS level your stack is a contiguous block of memory, typically 1MB, per thread... if you had 10000 threads you have 10000 MB of memory being used

Goroutine is the path of exuection at the Go software level. The Goroutine also has a stack of memory for execution... it is only 2K, as compared to 1MB for an operating system stack.

The goroutine only has direct access to memory for the frame it is operating in

The frame gives a sandbox, a sense of mutability, so our goroutine code can only effect a limited amount of our data.

Mechanics is how things work, semantics is how things behave.

Every time you make a function call, you cross over a program boundary... moving from one frame to another every time you call a function... you slice a new frame off the stack, and that frame becomes the new active frame

Because eeverything is pass by value, that means we're making a copy of the data as it crosses that boundary... addresses are data just like values are data.

Function parameters hold space for values you're going to throw over the program boundary to operate in that little sandbox where the function runs.

Within the frame data can be mutated (like you could increment a count) without any side effects anywhere else in the program.

This is what is called value semantics.

If you want to write Go code optimized for correctness then value and pointer semantics is everything.

What is the cost of value semantics? One cost is you have multiple copies of the data throughout the program... it can be complicated to update changed data everywhere it needs to be updated... the value is you reduce side effects, isolation, immutability, which is important for integrity

## 2.3 Pointers Part 2 (Sharing Data)

Pointer semantics allow the sharing of data across program boundaries.

You think passing a pointer is pass by reference, but its not, its pass by value, but the value is an address. WHich is a piece of data.

Pointer variables store addresses.

The star * operator allows you to declare the pointer variable.

Pointers are literal types (unnamed)

Pointer variables are always 4 to 8 bytes of memory depending on the architecture

TYPE IS LIFE

There's a huge cost to pointers. What you've done is set yourself up for side effects. When you start mutating memory, you have to be careful.

Functional programming languages try to avoid data race problems by not giving you access to pointers

Any memory below the active frame is not valid memory. It will be re-used as new functions are called.

## Pointers Part 3, Escape Analysis

Value Semantics has the benefit of a sandbox/immutability, but sacrifices efficency because we're creating lots of copies

Pointer semantics gives you the efficiency at the risk of side effects due to mutating shared data

Leverage the aspects of the language to manage cognitive load over memory management

We don't have constructors in Go because they hide costs, but we do have Factory Functions.

Factory Functions is a fx that creates a value, initializes it for use and returns it back to the caller

& means sharing

THe compiler can do escape analysis for you to decide whether a value can be on the stack, which is what we want, or whether it escapes to the heap. Ideally we want it on the stack because it's all there, so it's fast... plus the stack is self cleaning.

It's called an allocation to move a value to the heap... the garbage collector cleans the heap.

We want to leverage value semantics to keep values on the stack. 

The Go syntax abstracts away the machine so you don't have to care where data is... but when eprformance and debugging start to matter it does help to know what's happening on the machine

Never use pointer semantics during construction, use value semantics if you are going to assign to a variable

## 2.3 Pointers Part 4 Stack Growth

If a compiler doesn't know the size of a value at compile time, it must immediately assign it to the heap... 

Frames (for stack) are sized at compile time, they're not dynamic. 

What happens if a goroutine runs out of stack space? (remember there's 2K of stack for goroutine)

Go has contiguous stacks... if a stack is being used up, it will allocate one 25% larger and copy all the frames over to the new stack (causing a latency hit)

We take that hit for integrity and to minimize resources (meaning don't give yourself more then 2K unless you need to... you don't usually go more than ten function calls deep)

No stack can have a pointer to another stack

## 2.3 Pointers Part 5, Garbage Collection

Remember, the first hit to performance will be from latency from networking and disk I/O

The second biggest hit will be from allocations and the garbage collector

The garbage collector is a tri-color, mark and sweep concurrent garbage collector... 

The garbage collector has a pacing algorithm ... It's trying to balance: the smallest heap size where the stop-the-world latency is no longer than 100 microseconds per run.

In order to achieve this the garbage collector is allowed to take up to 25% of your CPU capacity

So... how do we maintain the smallest heap size running at a reasonable pace (w/ under 100 microseconds stop-the-world time) and leverage less than 25% of CPU capacity

THe heap is nothing more than a very large graph... we have stacks with frames that may have values pointing to values on the heap

We don't use global variables

From our perspective, this is what's important: we have to balance our value and pointer semantics to minimize allocations to the heap ... you're not going to write zero-allocation software, but you want to optimize this balance

## 2.4 -- Constants

Constants only exist at compile time. 

There's a distinction between constants-of-a-kind and constants-of-a-type... the first can be implicitly converted... types cannot be implicitly converted in Go

In Go we have something called Kind promotion ... The Go specification says a constant has to be 256-bits of precision...

Constant of a kind promotion (Revist this... it's confusing)

Remember there's two types of constants in go, constants of a type and constants of a kind... your literal values in Go are constants of a kind... constants of a kind can be implicitly converted by the compiler, which means you can't have enmuerations in Go(what does this mean?)... constants of a kind can have up to 256 bits of precision.

## Lesson 3 -- Data Structures

Go only gives arrays, slices and maps and there's reasons why

## 3.1 Data Oriented Design

Data transformations are at the heart of everything we do.

Everything we're talking baout now is in the concrete... whenteh congrete data is changing then your problems are changing... 

Once the data changes and our algorithms change, that can lead to cascading changes across a codebase, which causes pain.

If you're abstracting too much you're walking away from correctness and readability... we want thin layers of decoupling to deal with change

Everything we do should be focused around minimizing the amount of code we need to solve every problem

## 3.2 Arrays Part 1 -- Mechanical Sympathy

The slice is the most important data structure in Go...

If performance matters, main memory is so slow it may as well not be there... the total amount of memory you have is the total amount of cache

A cache line historically has 64 bytes

How do we ensure the cache line is in L1 or L2? We need tow rite code that creates predicatable access patterns to memory if we want to have mechnaical sympathy

*Predicatable access patterns to memory is Everything*

If you use continguous memory with predictable strides, your computer pre-fetchers can grab it... this makes arrays better than anything else as it relates to hardware

Arrays are not the most important data structures in Go, the slice is. 

Technically a slice is a vector. 

The OS manages memory at a granularity called a page... can be 4k, 8k, 16k... 

The TLB is a special cache the operating system manages ... creates a cache of virtual addresses to physical memory locations... the OS abstracts the real address to allow for quick lookups via these virtual addresses

If you get TLB cache misses, the hardware has to go ask the OS where the thingy is, and the OS has to traverse its paging table, and if you have a VM like a cloud environment they have page systems too... a TLB miss can be really, really deadly

Performance is not about how fast you can cycle the clock, it's how efficienctly we can move data into memory (cache) so you can access it quickly

*The pre-fetchers are everything and we must be mechanically sympathetic with them ... pre-fetchers love arrays*

I don't care what your algorithm is, an array will beat it 

Actually a slice is the most important data structure in Go, because they represent arrays under teh hood... technically slices are *vectors*

Stack overflow link about what a vector is in C++ : https://stackoverflow.com/questions/508374/what-are-vectors-and-how-are-they-used-in-programming

If you use the slice for the majority of your data handling needs, you are inherently being mechanically sympathetic. Maps too build data underneath with contiguous memory... this creates perdictable memory access patterns which aids performance

## Arrays Part 2 -- Semantics

## Slices (Part 1)

A string is a two word data structure

Use a slice of values over a slice of pointers when reasonable

The slice is the go-to data structure in Golang

The make function allows us to create three of the reference types that are built into the language

Go has built-in types, user-defined types, and reference types (slice, maps, functions etc)... reference types have a pointer to an underlying structure

A reference type set to its zero value is nil

We will use make when we already know ahead of time how much memory to allocate toward its backing data structure (an array)

With value semantics, every piece of code is operating on its own copy of the data

WIth pointer semeantics, the data is shared, which brings efficiencies, but mutation must be dealt with because it can create side effects throughout the application

So, are you doing the same thing with these two loops?

```go
for i, v := range friends {
    friends[1] = "Jack"
    
    if i == 1 {
            fmt.Println(v)
        }
}
// Here we're passing a copy of the value of friend to Print, meaning we have a new string value which points to the underlying array which may hold, say, the letters for "Apple"
```

AND

```go
for i := range friends {
    friends[1] = "Jack"

    if i == 1 {
        fmt.Println(fruits[1])
    }
}
```

No, though both examples seem to be accessing fruits from our array, the first is accessing the VALUE of the frien d string, whereas the second is accessing the actual string data via a pointer. The second is the pointer semantic form, the first is the value semantic

Understand, value semantics mean we're operating on our own copy of the data.

A slice is a three-word architecture... a pointer, the length of the underlying array, and the capacity of the underlying array... if only length is set on the make call then capacity will match length

The make call will set all values in the backing array to its zero value

Reference types are built around value semantics (designed to be kept on the stack)

fruits := make([]string, 5, 8) makes a slice with length 5 and capacity 8... capacity is for efficient growth

Slices are 24-byte values (8 for pointer, 8 for length, 8 for capacity)

One problem with slices is the pointer... it could lead to side effects as we mutate data

**We do not want to be mixing value and pointer semantics**

## 3.3--Slices Part 2 (append slices)

There's two things we do often with slices... we append to them, and we take slices of them

'var' is an indicator that we're using a zero value

A zero value slice is three bytes (words) looking like this...

| nil |
______
|  0  |
______
|  0  |

An empty slice, on the other  hand, has a pointer to an empty slice (different case)

|  *  |
______
|  0  |
______
|  0  |

The API for append is using value semantics... it's a value semantic mutation API... gets its own copy of the slice value, mutates it and returns it back...

On call to append, append gets its own copy of the slice value...

A memory-leak in Go is when you create a reference to a value on the heap that never goes away

If memory is going up on every garbage collection, you have a memory leak

Until you get to 1000 elements append doubles the size of the backing array in order to add length... after that it grows by 25% each time

## SLices--Part3, Taking slices of slices

Make a slice of strings with length of 5 and capacity of 8 ... 

Multiple slice values can share a backing array, so that the backing array is hte only thing that needs to be escaped to the heap... the slice values can stay on the stack...

If you don't know your length, you shouldn't be slicing.

Slice with length in mind... get the value you want to start with plus your length, slike slice(2:[2+2 aka 4]) rather than having to think about going from your starting to point to an index not including

Slice values are like a unique view of the core data structure (array)

If two slices point to the same backing value, you can have side effects from modifying values in those slices

Three index slices help reduce side effects
slice2 := slice1[2:4:4]

Built in function copy can also be used

## Slices--Part 4, slices and references

Pointer semeantics give us levels of efficiency but we also have to make sure we're very clean with data updates/mutations

Any time there's a call to append in code, immediately put the breaks on the code review because they can cause side effects

## Slices--Part 5, strings and slices

Strings in Go are UTF-8 based... the entire language is UTF-8

UTF-8 is a three-layer character set... bytes at the bottom, code-points in the middle (a 32-bit or 4-byte value) and on top characters (1 to 4 code-points)

A string has a pointer to the underlying array of bytes and the length of the underlying array

In Go, rune is really just an alias for type int32

Every array in Go is just a slice waiting to happen

## 3.4 Maps

Maps are just key-value pairs with a hashing algorithm underneath... 

THe builtin function make allows you to make slices, maps and channels

Maps are not usable in its zero value state, it must be constructed in its literal form.

WHen you iterate over a map it's random (un-ordered)

Built-in function delete() allows you to remove a key from a map

Use a map when you want to get to data quickly based on a key

## Lesson 4: Decoupling

## 4.1 Methods--Part 1 (Declare & Receiver Behavior)

We want to minimize cascading changes that rip through the codebase... that's where decoupling comes in

Decoupling is all done through behavior... behavior is where we do design, architecture and decoupling

Start from the concrete data and move up to bhevaior/decoupling

TOo many developers work the other way, starting with behavior/decoupling... if you start there you are guessing

*A method is a function that has a receiver*

*A receiver is a parameter. Think of it that way*

We need to learn when a piece of data should have behavior... it should be the exception, not the rule... which is a different paradigm from OOP

Most of the time Go wants to separate state from behavior

Functions should be the first choice until you need methods

WHen should a piece of data have behavior?

Normally value/pointer semantics don't hit go developers in the face until we get to methods

Should I use a value or pointer receiver when implementing a method?

We must be consistent with our semantics... once teh semantic is chosen, either everything is value or pointer... the code you write has to respect the semantic

## 4.1 Methods- Part 2 (value and pointer semantics)

These general guidelines will work for you most of the time

There are builtin types(strings, numerics, bool), reference types (slices, maps, channels, interface) and user-defined types (structs)

If you're working with builtin types (strings,numerics,bool) you should be using value semantics. No pointers to strings/numerics/bools. Strings are immutable, they're designed to be copied. 
This includes fields in a struct
An exception is for marshalling/unmarshalling SQL

For reference types() you should also use value semantics. Exception: you may take the address of a slice or map only if you're sharing it down the callstack to a function named decode or unmarshal... those require pointer semantics... other than that, everybody should get a copy of those slice/map values

For user-defined types (structs) you have to choose which semantic is in play.
If you're not sure what to use then use pointer semantics.
If you can use value semantics, then use them.

Do not make copies of values that pointers point to, that is a violation of semantic law

## 4.1 Methods--Part 3 (Function/Method Variables)

Methods don't really exist... all we have is state and functions... methods is syntactic sugar to make it seem like data has behavior

We want data having behavior to be the exception, not the rule

Setters and getters are not an API, they don't add value... 

Functions in Go are values (they're typed values)

Copies have to be allocated... we don't know about it at compile time, this is happening at runtime

When you decouple a piece of concrete data in Go, you're going to have the cost of indirection and allocation

We want to be sure that cost is worth it, we don't want to blindly decouple

Remember, allocaiton is number 2 on our list of performance concerns. But if decoupling is adding value (minimizing cascading changes) you take that cost all day long

## 4.2 Interfaces -- Part 1 (Polymorphism)

Polymorphism means you write a certain program that behaves differently depending upon the data it operates on.

Polymorphism means a piece of code changes its behavior depending on the concrete data it depends on.

When should a piece of data have behavior? One good reason is when you need polymorphism/decoupling... wnat to process all different types of data with a single piece of code.

An interface type is not real, there's nothing concrete about an interface type (unlike struct, which has real data you can manipulate)

Interfaces only define a method-set of behavior. They define a contract of behavior.

Interfaces should always be about behavior, not things.

Let the concrete data drive everything we do, even through the decoupling.

Interface types are valueless

Pass me any piece of concrete data that satisfies the reader interface, implements this contract, has the full suite of behavior/ method sets

We store concrete data inside of interface values ... though interfaces are valuleless, through the mechnaism of storing we have someting more concrete.

the copy of the data is stored inside the interface as a pointer

An interface is a two-word data structure. The second word holds the pointer to the piece of data. The first word holds a pointer to the iTable ... where it describes teh type of file being stored in the interface and a function pointer to the concrete implementation of the interface.

Indirection and allocation, that is what decoupling costs us.

## 4.2 Interfaces -- Part 2 (Method Sets and Address of Value)

Interface types are valueless... if a function signature asks for an interface type it actually wants any concrete type that implements the interface

There are rules around method-sets, and those rules are there to protect our software.

The rules of method-sets:
1. If you're working with a value of type T, only those methods using value receivers belong to the method-set for that value
2. If you're working with a pointer of type T, then pointer receiver and value receiver methods are available

## 4.3 Interfaces -- Part 3 (Storage by Value)

Decoupling is inherently an allocation type of operation, that's not unique to Go ...

## 4.3 Interfaces -- Part 4 (Embedding)

A good way to think about this is to create an inner type/ outer type relationshiop ... this leads to inner-type promotion, allowing access to things in the inner type to the outer type.

Inner-type promotion gives you a sense of type re-use but you can use it for much more than that...

Embedding does not create a sub-typing relationship ... this isn't based derived classes like in OOP ... the outer value satisfies contracts that the inner value does with inner-type promotion

if an outer type ALSO implements an interface that the inner type does, then there is no promotion ... the outer type will override the inner types implementation

Only at compile time are things being accessed promoted up

Embedding is for composition, not type reuse

## 4.4 Exporting

Exporting is kind of the encapsulation piece of Go ...

The basic unit of compilation in Go is a package, which in Go is a folder ... encapsulation ends at the folder level. Every folder represents a static library, our smallest unit of compilation

I always want to see one file named after the package name

The folder name should match the package name if you're being a good Go citizen.

Any capitalized identifier is exported.

## 5.1 Composition (Grouping Types)

Composition is something you'll be focused on a lot as a Go developer ...

First topic is grouping ...

There's no sub-typing/sub-classing in Go

**Go is about convention over configuration** .. Go says configuration is limiting

Go is about not who we are (say Animals as a type) but about what we do (hinting at interfaces, I think)... 

We want to be able to find smells in code ...

There is some cost to DRY (do not repeat yourself) ... sometimes a little duplication of code saves you coupling costs

Interfaces should define behavior, not persons/places/things

Concrete types should be used for persons/places/thing

You should try only to declare types for something new or unique ... we want to avoid using aliases ... if there's no method-set associated with a type you may not need it.

Remember constansts of a kind can be implicitly converted

If you define a type you should be creating values of that type ... if you're not using values of the type then you created a pure abstraction ... that's smelly 

## 5.2 Decoupling -- Part 1

A lot of you have been taught to start with the interface behavior ... I want you to do the opposite.

Remember, the  problem is solved in the concrete, not in the abstract

Remember, the problem is the data.

I want to see anywhere from 70 to 80% code coverage before you can say you're done.

Is the code decoupled from the change we expect to happen?

Decoupling is a refactoring for me, we solve in the concrete first then refactor to decouple

Developers have issues breaking problems down (what do I need to solve step by step)

Many software developers don't understand how to create a layered API ... instead of solving everything in a few functions, instead we want a layered approach.

A three-layer model:
- Primitive layer ... write this layer so it is testable. Remember, I'm working in the concrete. Code that is testable usually means the data we're passing in is reproducible and the data coming out is testable.
- Lower Level ... sits on top of the primitive API that does higher level stuff ... should be testable in its own right. These layers are often unexproted ...
- High level ... where you're trying to do as much as you can for the user to make their life better.

I don't want you to be worried about throwing code away... refactoring is the best

## 5.2 Decoupling -- Part 2




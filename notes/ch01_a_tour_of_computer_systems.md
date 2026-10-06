## 1.1: information is bits and context 
* we store one single character (say, ASCII) in 8 bit (1 byte) of informations. Because... 2^8 = 256. No wonder why `char` is the smallest data type in C. This 256 slots is really enough to store a lot of characters configurations. 
* we can use `man ascii` to display it. 'a' starts at 97, 'A' starts from 65.
* yeah, it really depends on the context. A program (that deals with translating another program to a different form) can interpret `10101011` differently with other program. That's why it requires context/metadata.
* bro this means every source code can be defined as information in computer science, lol it's a trivial yet cool facts imo

## 1.2: programs are translated by other programs into different forms
* C (high level programming) source code ---(_compiler driver_)---> _executable object program/files_ (machine-language instructions)
* `hello.c` ----(`cpp`: spit out all libraries shi needed)----> `hello.i` ----(`cc1`: ast lexer stuff)----> `hello.s` ----(`as`: relocate object programs/binary)----> `hello.o & printf.o` ----(`ld`: linker. execute object program)----> `hello`
* `preprocessor + compiler + assembler + linker = compilation system`
* i thought we do buffet style to take a few codes on the library, instead it's LITERALLY stacked on top of it. Maybe because it's hard af to write program to detect which part of the codes is needed for a specific usecase. (`gcc - E <filename>.c -o <filename>.i`)

## 1.3: it pays to understand how compilation systems work
* the coolest part is that how a trivial decision, such as parantheses orders, library compilation orders, etc... really matters so that it can compile faster, or even perform faster in hardware
* "he shell is a command-line interpreter that prints a prompt, waits for you to type a command line, and then performs the command" PEAKK AFF!!


## 1.4: processors read and interpret instructions stored in memory
* `BUS`: this lane literally just moves A CHUNK OF BITS/INFORMATIONS, which is what we call it as `word`. It can be 4 bytes (32 bits) or 8 bytes (64 bits)
* `I/O Devices`: uhhh... it's self explanatory ig
* `MEMORY`: lil bro just realize why is it random (because sometimes we aint know when a process will end, that's why no matter how tidy informations inside a ram at first will eventually become sooo chaotic. It's fundamentally to handle real world human complexity bro)
* `MEMORY`: yea DRAM kinda reminds me of latch and how to traps electrons on a gates (i forgor) 
* sooo... basically, we have shell program is executing, we type shi like `./hello` and shell knows what to do. It's like it (asks kernel to) retreives shi from disk. Stores it to rAM (via DMA?), wait for his turn to be executed, then... the cpu does the heavy lifting (yea, that same stuff like PC, file registers, ALU bla bla bla) then we display it via graphic adapter

## 1.5: cache matter
* as the title said, cache matter. A lot. Maybe it's all about distance and its underlying technology behind a storage and ofc it has tradeoff. Idk what's the components that makes it slower (but bigger) except the physical distances, engineering systems, and its components. well, yea, that's all ik i guess (so far)

## 1.6: storage devices form a hiarerchy
* remote server storage (basically it's a huge goofily slow disks on other computer) 
* local disk (SSD/HDD? yea, that's it)
* DRAM! the multiple black chess-formed with greenish board
* SRAM L3
* SRAM L2
* SRAM L1
* REGISTER! WORDS AGAIN!
* honestly idk what's with the notion behind this. Why do we end up using hiarerchy architecture? Why do we just use 3 caches? i am sure it's mix of industry, economy, and a bunch of trial and error

## 1.7: the operating system manages the hardware
* okay, again... so... OS is basically software that bridges between programs (that we often use in our daily life) and hardware. 
* it's all about one simple idea: `abstraction`. so, everything that conceptually exists doesn't actually exists when we see in raw hardware perspective
  * abstract `I/O disk` ---> `files`
  * abstract `I/O disk + main memory` ---> `virtual memory`
  * abstract `processor` ---> `processess`
* let's trace what's happen when we type `./hello`:
  * `[before write]:` say we only have only few processes at a time, one of them is shells 
  * `[during write]:` we type `.`, then `/`... until we finally have `./hello` (everytime we write one char, we interupt and ask OS to save the context of previous process TO PRIORITIZE YOUR TYPING)
  * `[after write] :` enter. shell (somehow) detects it
  * `[after write] :` shell do `syscall`
  * `[after write] :` OS saves shell's context
  * `[after write] :` OS creates new `hello` process (and maybe `hello` ask to do syscall to to call `display` files). well, idk.
  * `[after write] :` once all finished, OS will return shell context to CPU, and so on 
* hmm... threads is conceptually a subprocess. Why do we make threads? Because we can share memory WAY EASIER than with other process. No context switch required.
* virtual memory in a nutshell:
    ```
    (0xFFFFFFFF) kernel vmem         -> it's like how they know where to to syscall, i guess
    (0xFA324BA3) stack               -> every time we call a function, that's exactly when we use it.
    (0x412FAE34) shared library      -> uhh... idk but it said that it's related to dynamic linkers
    (0x02424FFF) heap                -> memory that can expands and shrink dinamically on malloc and free demand
    (0x00000000) program code & data -> linking (again) and loading. Global variable?  
    ```
* the beauty of files relies on how simple and how timeless this idea is because we treat every single I/O stuff as sequeces of bytes. Like... API?

 ## 1.8: systems communicate with other systems using networks
 * this should be heavily related to OS because we treat networking as files too, right?
 * so sad we aint talking about something deeper throughout this chapter (dont worry, we WILL learn this intentionally on chapter 11)

 ## 1.9: concurrency and parallelism
 * yo i just know that in a multiprocessor, we have two L1 cache. One for instruction, one for data. Shi is lit tho ngl
 * we have three levels of parallelism:
    * `threads-level:` we operate a few threads/process at a time 
    * `instruction-level:` we have multiple instruction at a time (cool, i thought parallelism, or concurrency is all about juggling process)
    * `SIMD (my fav):` uh... it's self explanatory, right? a single instruction can operates multiple data  

## 1.10: summary
* js realize how beautiful amdal's law when you can visualize it on a similar problem (taco bells truck distance)
* so... amdhal is just about... "given that this component contribute for like x% of the overall systems, and you make it y faster, what's the overall effect?"
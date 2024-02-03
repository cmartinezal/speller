# Speller
Program in C that spell-checks a file. CS50 Problem Set 5

## Problem to Solve
For this problem, you’ll implement a program that spell-checks a file, a la the below, using a hash table.

<img width="359" alt="Screenshot 2024-02-02 at 17 47 57" src="https://github.com/cmartinezal/speller/assets/84383847/69c8bdb9-8171-43d2-bdf3-d664d88d8ab8">


## Background

Theoretically, on input of size n, an algorithm with a running time of n is “asymptotically equivalent,” in terms of O, to an algorithm with a running time of 2n. Indeed, when describing the running time of an algorithm, we typically focus on the dominant (i.e., most impactful) term (i.e., n in this case, since n could be much larger than 2). In the real world, though, the fact of the matter is that 2n feels twice as slow as n.

The challenge ahead of you is to implement the fastest spell checker you can! By “fastest,” though, we’re talking actual “wall-clock,” not asymptotic, time.

In `speller.c`, we’ve put together a program that’s designed to spell-check a file after loading a dictionary of words from disk into memory. That dictionary, meanwhile, is implemented in a file called `dictionary.c`. (It could just be implemented in `speller.c`, but as programs get more complex, it’s often convenient to break them into multiple files.) The prototypes for the functions therein, meanwhile, are defined not in `dictionary.c` itself but in dictionary.h instead. That way, both `speller.c` and `dictionary.c` can `#include` the file. Unfortunately, we didn’t quite get around to implementing the loading part. Or the checking part. Both (and a bit more) we leave to you!

## Specification

Alright, the challenge now before you is to implement, in order, `load, hash, size, check`, and unload as efficiently as possible using a hash table in such a way that `TIME IN load`, `TIME IN check`, `TIME IN size`, and `TIME IN unload` are all minimized. To be sure, it’s not obvious what it even means to be minimized, inasmuch as these benchmarks will certainly vary as you feed `speller` different values for dictionary and for `text`. But therein lies the challenge, if not the fun, of this problem. This problem is your chance to design. Although we invite you to minimize space, your ultimate enemy is time. But before you dive in, some specifications from us.

- You may not alter `speller.c` or `Makefile`.
- You may alter `dictionary.c` (and, in fact, must in order to complete the implementations of `load, hash, size, check,` and `unload`), but you may not alter the declarations (i.e., prototypes) of `load, hash, size, check,` or `unload`. You may, though, add new functions and (local or global) variables to `dictionary.c`.
- You may change the value of N in `dictionary.c`, so that your hash table can have more buckets.
- You may alter `dictionary.h`, but you may not alter the declarations of `load, hash, size, check`, or `unload`.
- Your implementation of `check` must be case-insensitive. In other words, if `foo` is in dictionary, then check should return true given any capitalization thereof; none of `foo, foO, fOo, fOO, fOO, Foo, FoO, FOo, and FOO` should be considered misspelled.
- Capitalization aside, your implementation of `check` should only return `true` for words actually in `dictionary`. Beware hard-coding common words (e.g., `the`), lest we pass your implementation a dictionary without those same words. Moreover, the only possessives allowed are those actually in `dictionary`. In other words, even if `foo` is in `dictionary`, `check` should return `false` given `foo's` if `foo's` is not also in `dictionary`.
- You may assume that any `dictionary` passed to your program will be structured exactly like ours, alphabetically sorted from top to bottom with one word per line, each of which ends with `\n`. You may also assume that `dictionary` will contain at least one word, that no word will be longer than LENGTH (a constant defined in `dictionary.h`) characters, that no word will appear more than once, that each word will contain only lowercase alphabetical characters and possibly apostrophes, and that no word will start with an apostrophe.
- You may assume that `check` will only be passed words that contain (uppercase or lowercase) alphabetical characters and possibly apostrophes.
- Your spell checker may only take `text` and, optionally, `dictionary` as input. Although you might be inclined (particularly if among those more comfortable) to “pre-process” our default `dictionary` in order to derive an “ideal hash function” for it, you may not save the output of any such pre-processing to disk in order to load it back into memory on subsequent runs of your spell checker in order to gain an advantage.
- Your spell checker must not leak any memory. Be sure to check for leaks with `valgrind`.
- The hash function you write should ultimately be your own, not one you search for online.


## How to Test

How to check whether your program is outting the right misspelled words? Well, you’re welcome to consult the “answer keys” that are inside of the `keys` directory that’s inside of your `speller` directory. For instance, inside of `keys/lalaland.txt` are all of the words that your program should think are misspelled.

You could therefore run your program on some text in one window, as with the below.

```sh
./speller texts/lalaland.txt
```

And you could then run the staff’s solution on the same text in another window, as with the below.

```sh
./speller50 texts/lalaland.txt
```

And you could then compare the windows visually side by side. That could get tedious quickly, though. So you might instead want to “redirect” your program’s output to a file, as with the below.

```sh
./speller texts/lalaland.txt > student.txt
./speller50 texts/lalaland.txt > staff.txt
```

You can then compare both files side by side in the same window with a program like diff, as with the below.

```sh
diff -y student.txt staff.txt
```

Alternatively, to save time, you could just compare your program’s output (assuming you redirected it to, e.g., student.txt) against one of the answer keys without running the staff’s solution, as with the below.

```sh
diff -y student.txt keys/lalaland.txt
```

If your program’s output matches the staff’s, diff will output two columns that should be identical except for, perhaps, the running times at the bottom. If the columns differ, though, you’ll see a > or | where they differ. For instance, if you see
```text
MISSPELLED WORDS                                                MISSPELLED WORDS

TECHNO                                                          TECHNO
L                                                               L
                                                              > Thelonious
Prius                                                           Prius
                                                              > MIA
L                                                               L
```
that means your program (whose output is on the left) does not think that Thelonious or MIA is misspelled, even though the staff’s output (on the right) does, as is implied by the absence of, say, Thelonious in the lefthand column and the presence of Thelonious in the righthand column.

Finally, be sure to test with both the default large and small dictionaries. Be careful not to assume that if your solution runs successfully with the large dictionary it will also run successfully with the small one. Here’s how to try the small dictionary:

```sh
./speller dictionaries/small texts/cat.txt 
```

## Getting Started

Let's start to use this project.

## Prerequisites

A compiler for C must be installed

## Installation

To execute the project open the terminal and go to the project folder. Then compile the code with a C compiler and execute the file generated:

```sh
make speller
./speller dictionaries/small texts/cat.txt 
```



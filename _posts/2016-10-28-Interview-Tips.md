---
title:  "Interview Tips"
excerpt: "Tips for interviews that I've gathered"
categories:
  - Blog
tags:
  - CODE_DEBUG_LIFE
use_math: false
---

I have been sent interview tips from some companies and they prove quite helpful to read and think about. Here is a list for quick reference.

A Quora Post on getting better prepared for data structure/algorithm questions in an interview. [Link](https://www.quora.com/How-can-one-be-well-prepared-to-answer-data-structure-algorithm-questions-in-interviews). Some other posts discussed in this post:

* [ABC - Always Be Coding](https://medium.com/always-be-coding/abc-always-be-coding-d5f8051afce2#.dzxncni3u). Good general tips on what mentality to take on when approaching an interview. Also some great links for basic data structure and algorithm complexity.
* [Know Thy Complexities](http://bigocheatsheet.com). Good overview of complexity and some common data structure. I don't even know them all, should look more into this.
* [How to Ace an Algorithms Interview](https://www.palantir.com/2011/09/how-to-rock-an-algorithms-interview/). Page from Palantir. Great resource. They have a series of this:
    * [The Coding Interview](https://www.palantir.com/2011/10/the-coding-interview/)
    * [How to Rock a Phone Interview](https://www.palantir.com/2012/09/how-to-rock-a-phone-interview/).
    * [HOW TO ACE A SYSTEMS DESIGN INTERVIEW](https://www.palantir.com/2011/10/how-to-ace-a-systems-design-interview/)

[Top 10 Algorithms for Coding Interviews](http://www.programcreek.com/2012/11/top-10-algorithms-for-coding-interview/). Good nice resource that organize coding questions by topics. Systematic approaches to tackle coding questions are important.

Google Software Engineer Prep Doc - [link](https://docs.google.com/document/d/1hxnrh7nm24IqtFXsSQqwv4Arx4cxlD9t29cfpKQRRx8/edit?usp=sharing).

#### Google Coaching Session Keynotes

Some keynotes from Google Coaching session (and some are just me, be warned):

What to expect in a technical interview:

* Short introduction
* "The meat" or a technical assessment
* Close the discussion with your questions

How to prepare for the interview:

* Review algorithm and data structure.
* Practice writing code on the white board. (Google's 4 official languages: C++, Java, Go and Python)
* Read about interviews online. Yes, go online and read about interview experiences

What are evaluated:

* Do you have the right questions to ask.
* Quality of the code example.
* What is the thought process
    * In developing an algorithm
    * In coming up with a data structure
* Do you know how to communicate well with others

Objectives of the interview:

* Demonstrate your strength and abilities.
* Connect with your interviewer (by asking questions and making assumptions)
* "Help" the interviewer know me.
* Learn about the interviews and Google (or any other company)
* Are "Google" good enough / someone you want to work for.

(Hiring process in Google is not to compete with any specific peers but with the Google standard that is established in the hiring process.)

In developing a solution, you should keep in mind that

* Demonstrate how you approach the problem solving. Think out loud - what assumptions are made?
* Some interview questions are in-depth and hard. How do you handle complicated problem?
* The right answer is nice but not always necessary - the thought process is more important.

In answering a coding question, before writing down actual code, you should

1. Understand the question (of course)
2. Come a simple test example to confirm your understanding. An ideal example is rich but not tedious. And keep the example simple.
3. Disambiguate the input and output of the function you're going to write. (If it is a design question, write/draw down the design and talk through them before defining any classes/members/functions).
4. State and clarify assumptions: are there any memory or performance requirements?
5. Clear corner cases.
6. Write down function signature.

More generally, you should propose a working solution and refine later.

* Get the first solution that works. (I'm not sure about this tip here, interview time is precious, so you shouldn't waste any, but it doesn't mean you should just brute force your way through everything. Think and plan/design carefully before writing out elegant code in one pass is always more impressive than struggling to get your indices right in front of the white board IMO. Balance your time in planning and implementing - spare two or three minutes on coming up with a better solution. I have done this for a hard problem and come up with nothing other than brute force in the end, but it didn't stop me from acing that interview. Remember, be extravagant when you can afford it, what are you saving those three minutes for anyways?)
* Run through at least one or two examples to check for correctness.
* Check again for edge cases. If you find edge cases yet you don't want to deal with it (like invalid inputs), at least make a note/comment there. And it is fine to do that, interview time is precious.
* Try to clean up code after first pass.
* Ask interview if he/she has questions before refinement. Something like "what do you think, is there something that I can improve?".
* Lastly, ask if you have time to find a better solution. Rinse and repeat.

Some notes on writing good code:

* Come up with concise example, communicate and understand, look out for corner cases.
* Use signature name (e.g. `isValidCase()`, `findShortestPath`), be clear about your objective in the signature.
* Use descriptive var name. Unless it's `i`, `j` in `for` loops, you're expected to give the variable a more descriptive name than `N`, `map`. For example, `int size = str.size()` is just easier to understand than `int N = str.size()`. Don't make the names too long either, or you'll struggle to write them down in the interview.
* Remember that the interviewer may take a photo of the whiteboard to transcribe your code for hiring committee. So
    * Do NOT make a mess on the board. No matter how well you communicated with the interviewer, he may forget some details about your code, and a messy board will not help him remember.
    * DO NOT MAKE a mess! Be consistent with notations, var names and signatures. Write out comments if you have to.
    * This explains why planning is important - you're more likely to create a complete mess when you don't have a good design/plan.
* Check for typos.
* Do not over concern yourself with the optimal solution, come up with what you have.
* Be concerned about the readability of your code.

You don't have to explain every step when you write out the code - the interviewer can read. Explain when necessary and focus on writing the code.

Some side notes:

* If you propose more than one solutions, you should be willing to discuss performance tradeoffs of them and why you choose what you choose in the end. For example, is the solution time-aware or space/memory-constraint?
* If you don't know a function call, you can discuss it and make assumptions before using it. For example: "I don't know whether it's `stack.top()` or `stack.front()` in C++ but it should return the next element in the stack, I am going to stick with `stack.top()`, is that OK?".
* Some unacceptable practice is to call a magical function that may or may not exist to solve your problem. For example, I want to print out all the permutation of a string `str`, so I am going to call `next_permutation(str)` to do it for me:
    * First of all, you invalidated the purpose of this coding question.
    * You're not demonstrating any valuable ability of yours other than memorizing some function calls that may or may not exist.
    * What should you do? Explain how this function works and tell your interviewer that you're more than willing to implement it yourself. He/she may not ask you to implement it, but he/she will probably ask you how it works in great details. Be ready to crush those questions as if you've just implemented the functions a hundredth time. E.g. "yes, I will be more than happy to explain how `next_permutation()` works, in fact, I have implemented it myself several times for practice. The function takes ......".
    * Even then, you may be expected to implement the function instead. Roll up your sleeves and crush the question to impress your interviewer - this is not a time loss, it is an opportunity to show your true understanding of how coding works.
* When the questions are open-ended, be sure to ask a lot of question. For example, sort some number. You can then ask:
    * Are these number special?
        * Are they integers?
        * Are they in certain range? (You can consider using a bucket of finite elements for counter to sort the numbers.)
        * Are they unique? (How about radix sort here?)
    * How are the numbers stored?
        * Are they given to me in an array?
        * In a linked list? In a queue?
        * Are they distribtued over the network?
        * In some remote database that is costly to read/write.
    * Are the numbers presorted? (Maybe a selection sort will do just fine).
    * Is there any memory constraints?
    * Is there any time constraints?
    * Everyone can say quick sort and merge sort - it does not impress anyone. Demonstrate your ability to understand different algorithms and their tradeoffs. More importantly, demonstrate your ability to understand when to use the specific solution.

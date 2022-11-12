Vadim Victor Kim  
CSE 15L  
11/10/2022

# Lab Report 4 - VIM

## **Part 1**
After openning the document `DocSearchServer.java` in Vim, we can find and replace the start variable to be named base through following keystrokes:

```
:
3,30
s
/
start
/
base
<Enter>
```

The `:` keystroke allows us to begin typing commands in Vim. If you pressed the correct key, you will see similar cursor at the bottom:
![Alt text](Screen%20Shot%202022-11-10%20at%206.53.38%20PM.png)

The `3,30` is the range of lines we are looking through to find and replace the text we want:
![Alt text](Screen%20Shot%202022-11-10%20at%206.55.00%20PM.png)

We then add `s` to show that we are searching and doing search and replace.

We then separate the following arguements with `/`.

![Alt text](Screen%20Shot%202022-11-12%20at%202.07.04%20PM.png)

In this case, the first arguement is the word we are trying to replace, and the second arguement is the word we are replacing it with.

Thus we are trying to replace word "start" with word "base" between lines of 3 and 30!

We then hit `<Enter>` and see Vim replace it for us in under 20 keystrokes!

Before:
![Before](Screen%20Shot%202022-11-12%20at%202.09.33%20PM.png)

After:
![After](Screen%20Shot%202022-11-12%20at%202.10.12%20PM.png)

## **Part 2**
- Time to perform tasks by having to `scp` the files over to the remote machine: ~32 seconds.
- Time to perform tasks by using `Vim` on the remote machine: ~15 seconds.

**Which of these two styles would you prefer using if you had to work on a program that you were running remotely, and why?**

- I think I would still prefer to use `VsCode` in conjunction with using `scp`. While it is considerably slower, the task does not take into account having to learn how to do things in vim.

**What about the project or task might factor into your decision one way or another? (If nothing would affect your decision, say so and why!**

- If the change is small, like fixing a typo in the comment or changing value of one character by some amount, it is faster and easier to do it through `Vim`.

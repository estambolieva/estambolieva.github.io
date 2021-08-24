---
date: 2021-08-24 11:42:00
layout: post
title: Job interviewer - If you have only 1 question
subtitle: 
description: What to ask at a technical interview
image: https://images.unsplash.com/photo-1602516297586-312f705402cb?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=967&q=80
category: startup
tags:
  - technical interview
  - startup
author: estambolieva
---

**tldr;** If you had only one question to judge the quality of the technical candidate for your startup, what would that question be?

This is the choice of a question of Asen who I chatted to some minutes ago.

> We have two numbers - 36 and 48. Write a function which receives as an input one of these numbers, and returns the other. **Important**: You are not allowed to use any of these - if clauses, loops and data structures. 

### If you had just one question


### Here are 3 example solutions

*Input*


Input: 36, Output: 48.


Input: 48, Output: 36.



[1. Use sum](#sol-disk-array)

[2. Use a string](#sol-string)

[3. Use text files](#sol-text-file)


#### Use sum <a name="sol-disk-arrayr"></a>

* sum up the two numbers
* receive the input number
* return the sum of the two numbers minus the input number

```py
two_num_sum = 36 + 48

def return_the_other_number(this_number, two_num_sum):
  return two_num_sum - this_number
```

#### Use a string <a name="sol-string"></a>

* Store the two numbers in a sequence in a string.
* Remove the input number from that string
* Return the remaining string


```py
def return_the_other_number(this_number):
    this_str_number = str(this_number)
    num_string = "3648"
    
    return int(num_string.replace(this_str_number, ""))
```

#### Use text files <a name="sol-text-file"></a>

* create two text files - named `<number>.txt`. The content of the file would be the other number
* return the calue written in the text file with the name of the input number


```
# 36.txt
48
```

```py
def return_the_other_number(this_number):
    filename = str(this_number) + ".txt"
    
    with open(filename, "r") as fin:
        output = fin.read()

    return int(output)
```


**Photo Credit**

Unsplash/[Jac Alexandru](https://unsplash.com/@rolls0ut)

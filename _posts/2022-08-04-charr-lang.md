---
layout: post
title: "Programming language: CharrLang"
description: "On this post, I talk about my programming language"
date: 2022-08-04
tags: CharrLang
---

During the past few days I've been writing a pythonic compiled language, Charr(Lang), and as such I'm here to talk about it.

Most of what I'll cover is also covered in the <a href="https://github.com/charlotte-2222/charr-lang/blob/master/README.md">repository documentation</a>, but I also wanted to include additional information such as conception and resources.

# CharrLang Conceived
The main purpose of embarking on this adventure is to add a project to my resume that will cause me to stand out more, essentially the appeal to a recruiter.

Next in line, I wanted to gain a deeper understanding of decisions behind language design. With design, there's always a compromise to be made between readability, performance, and reliability.

### For instance, lets look at common logical operators.

I opted for the C++ route of equality operators:
Operator: `==` representing equality, `!=` for inequality.
Even mathematically focused languages like Matlab and Julia use C-style logical operators.

That said - an argument can be made for safer and more sensible syntax replication. 

>= / == can  lead to confusion between equality and assignment in statements such as if(a=b)

>Person XYZ believes = should be equality, just like in non-programming usage, and assignment can be <- or :=

The real flaw in C++ is not the = vs == syntax, but the fact that = returns a value, that can be used in a conditional expression. The return value of an assignment is rarely used, so just defining the return value of an assignment expression to be the void type and not allowing it as a conditional expression turns 99% of incorrect uses into compile errors. Incorrectly using == when an assignment is desired could exist, but rarely occurs in practice.
If = is chosen as equality only and := or <- for assignment, this introduces a high risk that a habitual programmers accidentally uses = when an assignment is desired, which will not result in a compile error, hence this option will just move from one problem to another.
The last option is to use == for equality and := or <- for assignment. This will catch all accidental uses at the expense of increasing their likelihood to appear, so this is also not an improvement.

### My familiarity with concepts
In the end, as I get more familiar with flushing out this language; and the development of something like this as whole - my familiarity with concepts like:
- recursion
- closures
- garbage collection
- reference management
- typing
- data structures

...and how these all work together will not only increase, but become more fluid in practice. It's a learning process, but it allows be to utilize and access these facets of language far more easily than reading a textbook or watching a lecture.

##### An analogy
If you were to learn Spanish, you don't simply pick up a English->Spanish dictionary and read it. You must get involved with the inner workings of the the language, the syntax, the semantics - what words mean, how an inflection might change that meaning and context, and eventually; you have to learn by *doing.*


### Writing a compiler...
...will teach you *a lot* about computers. 


## Summary of why:
There's a lot of reasons, starting with *"I need a job"*, and ending somewhere with the fact that there's a difference between the programmer who uses the tools, and the one who writes them.

---


# Tools that I used

First of all, it's really important to note that going into a project like this you might want a decent grasp of the language you're using. Other then that, watching a few YouTube videos and reading blogs/various literature on the concepts will help get you started.

I spent a good chunk of my weekend studying up on these concepts and eventually found <a href="https://sly.readthedocs.io/en/latest/sly.html#writing-a-parser"> SLY(Sly Lex Yacc)</a>.

The link provides all of the information necessary, but in short:
Sly is a Python library for writing parsers and compilers. It's not exactly a framework, and as is described - it's barebones. It simply provides you with the bare-minimum tools for success. The rest is up to you.

### The `Lexer`
One of the provided tools(classes) is a Lexer, which breaks input text into tokens (specified by Regex rules.)

Here is one such example from CharrLang -
```py

    NAME['if'] = IF
    NAME['elif'] = ELIF
    NAME['else'] = ELSE
    NAME['while'] = WHILE
    NAME['do'] = DO
    NAME['break'] = BREAK
    NAME['out'] = PRINT
    NAME['in'] = INPUT
    NAME['inc'] = INC
    NAME['dec'] = DEC
    NAME['nothing'] = PASS
    NAME['and'] = AND
    NAME['or'] = OR

```

```py

    # Extra action for newlines
    def ignore_newline(self, t):
        self.lineno += t.value.count('\n')

    def error(self, t):
        print("Illegal character '%s'" % t.value[0])
        self.index += 1
```



### The `Parser`
This fun little thing is what recognizes language syntax (that you specify). You use the two together.


Here is an example from CharrLang


```py

    precedence = (
        ('right', COLON),
        ('left', OR, AND),
        ('left', EQ, LT, GT, NE, GTE, LTE),
        ('left', PLUS, MINUS),
        ('left', TIMES, DIVIDE),
        ('left', POW),
        ('left', MOD),
        ('right', UMINUS),
        ('left', WHILE, DO),
        ('left', IF, ELIF, ELSE),
        ('left', PRINT, INPUT),
    )

```

```py
 @_('WHILE expr DO LBRAC statements RBRAC')
    def statement(self, p):
        return ('while', p.expr, p.statements)

    @_('PASS')
    def statement(self, p):
        return ('pass',)

    @_('BREAK')
    def statement(self, p):
        return ('break',)
```


<hr>


# Running CharrLang

Running Charr is rather simple at the moment. Of course, it still has plenty of work to go through - but it's in a decent spot right now (ver0.0.2)

I don't consider it a true compiler, nonetheless.

#### Compiler/CLI
![](/img/22-8-4-charr/Pasted%20image%2020220804141748.png)
#### 'Running' a .charr file. Long way to go.
![](/img/22-8-4-charr/Pasted%20image%2020220804141830.png)
#### Shell 
![](/img/22-8-4-charr/Pasted%20image%2020220804142302.png)

<hr>

I won't go over the general syntax and everything that I've already covered in the current documentation on GitHub, however if you'd like to play around a bit in the <a href="https://replit.com/@charlotte-2222/charr-lang?v=1">shell</a>


# Final Note

Last night I actually *"dreamt in code"*, and thought of a way to fix a bug I'd had in CharrLang for short period (That had been driving me insane).

This type of thing happens every so often when I obsess over things, and I've definitely been obsessive over this; to the point where both my partners have tried getting my attention in various ways (*spicy various*) and they've simply gone ignored, albeit accidentally.

Sorry you two, I've transcended horny - I'm with the code gods now. Baphomet is my homie now.
<br>
Oki doki, now that I've got all of this out of my system and have put out a serious blog post for once, it'll probably be back to the regularly scheduled bad-content. ✌️
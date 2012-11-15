---
layout: default
title: Language Acquisition and Programmers?
permalink: LanguageAcquisition
category: People
description: Creating better programmers using language instruction techniques.
summary: At some point almost everyone in the software industry wonders why there is such a vast separation between the best programmers and the worst.  Many programmers believe that it is simply a matter of talent and that poor programmers can not be trained to be substatially better.  My experience as an English teacher has shown me some eerie similarities between programmers and learners of a second language.  Can research in Language Acquisition help programmers?
---
## Language Fluency

### Why Language Acquisition?

Before I begin this topic, let me spend a brief amount of space discussing 
my background.  I would primarily describe myself as a programmer with
a penchant for solving problems. I see programming as a literary activity
which is applied to solving specific problems.  My desire to solve problems
led to my interest in process improvement and people development.  Finally,
I grew interested in teaching and I ended up teaching English for 5 years
in Japan.  This is probably a fairly odd progression for a programmer and
if you are interested to see what makes me tick, I invite you to read
my post describing [my philosophy](../AboutMe).

5 years teaching English seems like a long time, but in reality teaching is
an incredibly difficult discipline and 5 years was barely enough for me to
become somewhate adequate as a teacher.  Almost everyone has some experience
in the average high school setting, so it is easy to think that teaching
is all about controlling the classroom and presenting the material.  Indeed,
this is a large part of teaching, but the thing that grabbed my attention
was one particular problem.  By the end of high school, my students had
spent 6 years studying English.  The knew thousands of words of vocabulary.
They knew how to conjugate verbs, how to form the various tenses, how
to use passive voice, and any number of other impressive things.  But they
couldn't hold any kind of conversation in English.

To me this is incredible, but it is backed up by my own experience learning
French.  I had 13 years learning French with exactly the same results.
In fact, my family even speaks French.  Why is it that I was never able
to learn to speak it?  At first I thought it was simply a lack of talent.
Some people can learn other languages and some can't, I thought.  However,
the fact that I am now fluent in the Japanese language is evidence of
the fact that my belief was incorrect.

In fact, I now believe that if you can speak one language, you can aqcuire
any number of languages, provided that you put yourself in a position to
do so.  The problem is not a lack of talent, but rather an incorrect
choice of focus when we are learning.  In the realm of language acquisition
research, there is a theory which states that there are actually 2 ways
to learn something: "learning" which enables you to remember; and 
"acquisition" which allows you to use.  Traditional language classes focus
on learning, sometimes at the expense of acquisition.  The result is that
the student knows a lot *about* the language, but is unable to *use* the
language.

### Language Lawyers and Pasters.

Very early in my career, I was accused of being a "language lawyer" in C++.
A language lawyer is someone who knows every detail about a programming
language, but is unable to program idomatically.  In my case, I was very
enthusiastic about the features of C++ and was keen to try to use them
in any way I could.  However, the result of this creativity was impenetrable
code.  There were others on my team who had a much lower level of knowledge
about C++, but who were writing code that was approachable by everyone.

On the other side of the spectrum from language lawyers are people I will
call "pasters".  A paster is someone that constantly tries to find code
that does what they want and then pastes that code into the application
along with some minor modifications.  These people rarely fully understand
the code that they are writing.

Neither language lawyers nor pasters are desirable on a software team.
Ideally, what we would prefer are people who can *fluently* write code
that is both understandable and idomatically correct for the situation.
We also want programmers who are able to intuitively choose appropriate
designs without undue time and effort.  Such programmers will be
much more efficient with their time.  Indeed, it has often been reported
that there can be as much as a 100:1 difference between the best and
worst programmers.

### Can We Teach Programming?

It is my opinion that any person who has good communication abilities
in their own language is able to learn to program at a very high level.
It is true that talent makes a difference, but I believe that just like
fluency in human languages  can be taught, so can fluency in programming
languages.  However, we do not focus on the correct aspects when we are
teaching.

Language lawyers and pasters have analogs in human language learning
environments.  Most people who score highly in foreign language studies
at high schools are likely to be language lawyers.  They can tell you
the meaning of thousands of words of vocabulary.  They can explain
how to form any kind of sentence you ask.  However, they can not carry on
a conversation, even at a child like level (like a child of say 4 or
5 years old).

Similarly, if I ask my students to create a short piece of writing,
many will search their text books for similar pieces and replace vocabulary
with relevant words.  The result is something that is hardly decipherable
because it is not using correct idioms for the context.  Often there
are also large numbers of errors simply because the student didn't understand
the passage in the first place.

My point is that the problems we find with programmers are exactly the
same problems I found with my English students.  I believe that the
solution is also the same.  We must teach programmers how to be fluent
in the languages they are using.  Not only do we need to show them
the syntax and grammar for a language, we need to show them appropriate
idioms for a variety of different situations. Finally, we need to
get them to *acquire* these idioms rather than just *learning* them.
(Anyone who has been frustrated by a colleague using design patterns
as some kind of recipe book may identify with this situation).

### The Rules of Acquisition.

In my post, entitled [Rules of Acquisition](../RulesOfAcquisition), I
detail the factors that I believe affect acquisition of linguistic skills.
Here I will discuss how I believe this affects programming.  Acquisition
is a very powerful tool for improving programming ability.  We do not want
programmers who methodically apply rules in order to create code that
runs.  We want programmers who can intuitively pick appropriate designs
given the context of the situation.  We also want programmers who
are able to immediately see when code is idomatically incorrect when
they encounter it.  As I discussed in the
[three rings of programming](../ThreeRings), it is not enough to merely make
code work.  It must also be intuitively easy to understand when others
read it.

Their are two main problems I see with programmers who lack fluency in
programming.  The first is that they do not intuitively use idiomatic
expressions that other programmers use.  Instead, they will either tend
to use their own quirky expressions (often a language lawyer), or they
will apply common expressions inappropriately without fully understanding
the situation (often a paster).  The other main problem I see is that many
programmers do not have a fully functional monitor.  They can not tell the
difference between appropriate and inappropriate code.  Often their only
criteria for success is that the code appears to run correctly.

The solution to both problems is the same.  Programmers need to read an
enormous amount of idiomatically correct code.  In our education system,
production is prioritized over comprehension.  Students are asked to
write considerably more code than they are asked to read.  When a student
graduates and starts working, they are also asked to produce code.  Rarely
is there time to simply read code.  Even if a programmer becomes fluent,
they often develop their own idiomatic expressions rather than adopting
a common set of expressions with an outside group.

The problem is compounded because these programming styles are
haphazardly mixed throughout projects.  It's like having a document
written in dozens of different dialects.  Even if you read it, it's
hard to acquire one of the dialects because the expressions are not
used consistently.

The best thing a team can do to improve the performance of its members
is to consistently read each other's code.  When you see problems you
must correct the code and bring the issue to the attention of the author.
Doing this, the team will not only develop an internally consistent dialect
within the team, but will also develop programmers who are fluent in
that dialect.  They will be able to intuitively choose appropriate designs
without undue planning.

The enemy of this solution is a lack of vigilence.  If inappropriate
code is not corrected, not only does it lead to a confusing code base,
but it also cause programmers to acquire these poor programming practices.
The more a person reads and understands code written in a certain way,
they more they will tend to create code in that way.  We must be
extremely careful to avoid this.

Another important point is that programmers must fully understand code
that they are reading.  If they do not understand the code, they will
never acquire the ability to intuitively create those kinds of designs.
It is not enough to simply "get the gist" of a piece of code.  Programmers
should read for 100% comprehension (As an aside, many researchers will
argue that 95% comprehension is acceptable, but it is easier to aim for
100%).  If the code is not understood, they should ask for an help.

Finally, my last piece of advice is likely to be controversial.  Comments
that explain how code works will be counter productive to acquisition
of the constructs.  If code can be understood through the comments,
then the tendency will be to avoid reading the code.  If the code is not
read, the code will not be acquired -- only the comments.  This is extremely
important in my opinion.  Code must be understandable without comments.
Comments should rarely be used as explanation, but rather for warning about
expectations and potential problems with using the code.


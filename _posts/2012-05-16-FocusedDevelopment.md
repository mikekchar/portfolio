---
layout: default
title: Focused Development
permalink: FocusedDevelopment
description: How to save money by focusing development.
---
## Saving Lots of Money

Fred Brooks wrote the now famous paper, 
"[No Silver Bullet](http://www.cs.nott.ac.uk/~cah/G51ISS/Documents/NoSilverBullet.html)" 
several decades ago.  In his paper, he deftly 
explained why there is no development tool that will accelerate development
to get an order of magnitude improvement in productivity.  To make a long
story short, the problem is that the majority of effort in development
is actually gathering requirements and verifying that those requriements
meet customer needs.  Even if you could reduce programming time
to nearly nothing, you would still only experience a small improvement
in development speed.  Despite this truth, there are ways to increase
the amount of value delivered to the customer in the same amount of
development time.

The key to achieving this seemingly impossible goal is actually quite
simple.  We reduce the amount of effort expended on things
that the customer does not value.  To some degree we can do that
with process changes. There are many activities in a software team
that are not related to customer value.  For example, reporting
status of team members.  Such status is necessary for tracking
development, but it does not add value to the customer.  

Often when organizations are looking for ways to improve their
performance, they concentrate on these kinds of changes.  However,
as I stated above, there is a limit to the returns that process change
can have on development time.  So instead of concentrating on
process, an effective team should be concentrating on <em>what</em>
they are building rather than <em>how</em> they are building it.

It stands to reason that an application that does one tenth of
the functionality can be developed ten times faster than an
application which does more.  In reality, even more gains can
be made.  Simple applications are easier to manage and require
much less communication than complex ones. In Fred Brooks' other seminal work,
"[The Mythical Man Month](http://en.wikipedia.org/wiki/The_Mythical_Man-Month)",
he explains the dramatic cost of adding more resources to a project.

Concisely, the key to dramatic improvements in development speed
is reducing the scope of the project.  This immediately raises the
question of how one can effectively reduce the scope of a project
without compromising market viability.  In my post on
"[Requirements and Expectations](/2012/04/19/requirements)" 
I discuss the difference between a requirement and expectation.

When gathering requirements for development, mistakes are incredibly
costly.  Every piece of functionality added to the system not only
increases the amount of development time needed, but also makes the
system more complex.  This complexity increases the cost of development.

The easiest way to ensure that you don't undertake unnecessary
development is to test your requirements frequently. The easiest
way to do that is to build a working system and allow the user to
interact with it.  If it is done frequently enough, development on
unproductive features can be terminated before they take too much
time.  Newly discovered features can also be prioritized over
features with lesser value.

Most so called Agile development methodologies use short iterations
in order to facilitate this kind of requirements discovery.  However,
it is crucial to repeatedly test the requirements at the end of every
iteration with a user.  Failure to do so throws away the biggest
opportunity to reduce development cost.



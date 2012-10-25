---
layout: default
title: Problems with Model View Controller (MVC)
permalink: MVCProblems
category: Programming
description: Why is there business logic in my UI code even though I use MVC?
summary: MVC is a good idea, but if not used carefully it often fails to separate concerns.  When using widget libraries that use MVC the most obvious approaches often end up with business logic stranded in the UI code.  Unlike chocolate and peanut butter, the mix is undesirable.
---
## MVC isn't helping as much as I thought it would

Model-View-Controller (MVC) is by far the most popular design pattern in use
for UI design.  To be honest, I don't really tend to think of it as
a design pattern because the roles of the classes are very loosely defined.
In the event that you aren't aware of this popular approach, I will
describe it briefly.

### What is MVC

MVC is a method to achieve separations of concerns between the UI and
business logic of a program.  Very frequently programmers will
embed business logic code in UI code.  It is understandable why this
would be done.  From the perspective of attempting to write the
initial code, it is easy to envision what should be done by organizing
the code based on how the information is presented to the user.
The problem comes when data from one part of the program needs to
access information from another part of the program.  If there is
no relation in the UI, the complexity becomes very difficult to manage.

MVC attempts to circumvent this problem by creating a separation between
underlying data and it's presentation to the user.  The data along
with business logic (the model) is held in one place and the presentation
(the view) is held in another.  In fact there is one other separation:
the controller.  The controller allows the user to manipulate
model objects.  This image from [Wikipedia](http://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller) illustrates the collaboration between
the parts well.

![Model View Controller Image](../images/500px-MVC-Process.svg.png "MVC Overview")

### Example of MVC

Let's take a trivial example to illustrate MVC: that of a simple text
entry box.  On startup, our program will read a line of text from a
file and display it to the user. The user can edit the string and
when finished, the string will be written to disk again.

At the heart of the program is a simple string.  We need to be able
to read data from a text file, and write it back out again.  None of
these things requires a UI of any sort.  This is called the model
object.  Most languages contain a String object that will do nicely
for this model object.

But we also need to display the string to the user. This is the job
of the view object.  We can create a StringView object that, when
passed our model String, displays it to the user. This is the extent
of the StringView's role.  Input is not handled by the view objects
in MVC.

Since we need to get input from the user we need a StringController
object that, when passed our model String, allows the user to modify
it.  Again this is the extent of the StringController object.

Of course there is a small amount of housekeeping that needs to be done.
If the String object is modified, we need to notify the StringView
to display the changed string to the user.  You also usually need to
provide some indication of what the StringController is editing in
the StringView, showing the text insertion point, for example.  This
all tends to complicate things, but the basis of MVC is this.

These days, almost all UI widget libraries use MVC under the hood.
Frequently, the presentation of MVC outside the widget libraries is
mashed up, though.  For example, the widget view is almost always
combined with the widget controller into a single object.  There
may or may not be a model object built in to the widget either.
Some widgets may expect the programmer to supply a model object
that can be used with the view, while others may supply their own
model object.  Though each widget library gives a different
look to the programmer, underneath they are all pretty much MVC.

### Bring On the Problems!

Let's try to write our small program again, but this time using
a widget library.  Our widget library has been implemented using
MVC, so this should make our job easier, right?  There is a
TextEntry widget that contains a StringBuffer for the model
object. When the StringBuffer changes, the TextEntry widget
is automatically updated.  When the TextEntry widget is
displayed on the screen, a TextController is automatically
created that allows the user to update the contents of
the StringBuffer.  Why, we haven't written anything and
the program is 90% done!  What could go wrong?

There's only one thing left to do.  We need to read the contents
of the text widget from a file at the beginning and then write
it out again once the user is finished.  However, the StringBuffer
in the TextWidget can't read or write to disk.  But that's easy
to fix.

Ideally we would simply subclass the StringBuffer and add the
functionality that we need.  Unfortunately, the TextEntry
automatically creates the StringBuffer and there is no facility
for creating our own buffer.  Modifying TextEntry to allow
separate initialization of the StringBuffer is simply beyond the
scope of our project.  Even if we have source code for the widget
library, maintaining a fork of the library is not worth it.

The next most obvious approach would be to subclass the TextEntry
and add the functionality there.  We can simply initialize the
contents of the StringBuffer from disk when we display the
TextEntry.  When we stop displaying it we can write the StringBuffer
out again.  This is the approach I've seen in almost every program
I've looked at.

Let's think for a second, though.  What have we actually done?
Is our business logic actually separate from the UI?  In fact, we
have actually *embedded* our business logic into a subclass of
the UI.  This is precisely what we were trying to avoid.  If
we need a different UI for a different platform, for instance,
we have to remember to rewrite the code for writing the buffers
out to disk.

The next approach would be to seal off the UI entirely.  In this
case instead of inheriting from TextEntry, we simply use a TextEntry.
When we display the TextEntry, we initialize the StringBuffer with
the contents of the file.  When we are finished with the TextEntry
we query the StringBuffer and write out the contents to disk.  Unfortunately,
this approach isn't any better than the previous one.  UI specific code
is still interspersed with model specific code.

The last approach I will discuss here is to create yet another layer
of MVC.  In this case we revert back to using our simple String class
for our model object.  We create a StringView class that contains
a TextEntry.  We write logic in the StringView class that allows us
to update the TextEntry when the String changes.  Similarly, we write
logic that allows us to update the String when the StringBuffer in
the TextEntry changes.

This approach has a lot of advantages.  First it allows you to truly
separate the model and business logic from the UI. Also, by using
a Bridge pattern, you can easily implement the UI on as many
different platforms as you want.  The disadvantage is that the
amount of work necessary to keep the business logic's model objects synced
with the UI's model objects is substantial.  Most widget libraries also
don't give you direct access to the controllers, making that
syncronization more difficult.  In the end, though, the benefits
dramatically outweigh the costs in a complex project.

### What's next?

By way of providing an introduction to my upcoming blog post, there
is one more problem.  While it is desirable to move as much business
logic into the model objects as possible, there is often a fair amount
of presentation logic in a program.  For example, when we are in the
context of loading a file, we have a few model objects and a few
UI widgets that we need to deal with. However, we don't need to
deal with every model object or UI widget in the system.  We just need
a FileName object and a File object on the model side.  Similarly
we need a FileChooser widget on the UI side.  The File object, especially,
will have different collaborators in this context than it might
in another context (parsing the file, for instance).  It would
be nice if we could find a place to put this logic without polluting
either the model objects or the widgets.  My next installment will
introduce an idea for maintaining this context.



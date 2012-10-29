---
layout: default
title: Introduction to Model-Context-Interaction
permalink: MCIIntroduction
category: Programming
description: Removing Business Logic from UI Code through a Mediator
summary: As I detailed earlier, MVC alone can have problems keeping UI code separated from business logic.  In this post I describe a solution based on Martin Fowler's Model-View-Presenter (MVP) patter.  It involves using a Mediator that represents the context in which the program operates.
---
## Where should I describe what my program does?
In my discussion on [problems involving MVC](../MVCProblems), I discussed how
the Model View Controller pattern does not usually solve problems
for application developers.  While it is incredibly helpful to implement the
underlying widget library using MVC, the developer is forced to build
another layer of MVC in his application in order to get the kind of
separation between business logic and UI that is desired.  Not only
that, but there is often a considerable amount of logic about how
the program operates which seems to lie somewhere between the model
and the UI.

Probably an example is in order.  Let's consider the case of a simple text
editor.  This text editor has a window into which the user can type
text.  If they hit a certain keystroke, a list of files is displayed
to the user.  Upon selecting a file, the text editor loads the contents
of the file and puts it in the window.

We can easily separate the model objects from the the UI.  On the model
side, we need a TextBuffer, and a File object.  On the UI side we
need a TextFrame and a FileSelectionDialog box.  This is all well and
good, but where do we represent the relationships between these objects?
Where do we tell the program what it is supposed to *do*?

We could, perhaps, put code in the UI layer that interacts with the
TextFrame controller and listens for the keystroke to open the
FileSelectionDialog.  On consideration, though, does this code *really*
belong in the UI code?  We have a story that specifies the the
user must be able to load a file.  Isn't this functionality "business
logic"? If we code it entirely in the UI layer, it will be easy to
lose it (and very difficult to unit test it).

If it's business logic, perahaps we can put the code in the model layer.
We could create a whole set of abstract classes that model the interactions
that the user can perform, hook it up to the UI and have the model
classes act like a controller.  But this is likely to be very brittle.

Taking a page out of 
[Martin Fowler's Model View Presenter](http://www.martinfowler.com/eaaDev/ModelViewPresenter.html),
my personal position is that there is another layer of code that should
be responsible for this logic. I call this layer the Context.

### Representation of the User's Context

The "Context" in Model Context Interation (MCI) represents the
context the user finds themself in in the program.  In our previous
example, there are 2 contexts.  The first context we could call the
TextEditing context.  In this context, the TextFrame is displayed
and when the user inputs/edits text, the TextBuffer model object
is updated.

The second context could be called the FileLoading context.  In this
context, the FileSelectionDialog is displayed.  When a user
selects a file from the dialog, a File is opened and it's contents
are placed in the TextBuffer.

As you can see, each context has access to a certain number of model
objects.  The TextEditing context has access to the TextBuffer;
the FileLoading context has access to a File and the TextBuffer.
Each context also has access to user interface objects. TextEditing
has access to the TextFrame and FileLoading has access to the
FileSelectionDialog.

In MCI, contexts are actually represented by a separate object.
These objects contain references to the necessary model and
user interface objects.  Not only that, but they implement
the business logic that tells the program what to do in that
context.

For example, FileLoading contains the code that instantiates a file
object, loads the contents and copies it into the TextBuffer.
TextEditing doesn't have to do very much in our example, but if you
wanted to implement searching, for instance, you could put that
code in this context.

### Interacting with the UI

So far we've found a place to put business logic that tells the
program what it is supposed to do in different contexts, but
how do we link the model objects to the UI objects?  In MCI,
this is the responsibility of the Interaction.

An Interaction is simply a contract between the Context
and the UI objects.  It specifies what requests the
Context may make on the UI objects.  Ideally,
it also specifies what requests that the UI objects
can make on the Context (though this complicates implementation).

Although it is not necessary, I usually put all of my UI objects for
a particular context into a single container (a VBox, for instance).
I then create an Interaction that specifies what requests the
Context can make on the UI objects.

A good example of this would be the UI for the FileLoading Context.
We use a FileSelectionDialog.  This dialog is obviously made up of
many UI objects that are contained in a single dialog box.  Even
though the dialog box is very complex, at the moment we are only
interested in making a single request of it: Please get a file
name from the user.

Thus my Interaction for the FileLoading context is very simple.
It is simply a single method that requests a filename.  When the
context invokes this method, the FileSelectionDialg is displayed,
the user selects a file, and the file name is returned to the
Context.  The Context then uses that information to create a File
object and load the contents of the file.

For the TextEditing Context, things are a little more complex.
We need to be able request that the TextFrame opens.  We also
need to be able to request that the TextFrame is updated with
the contents of the TextBuffer when it changes (for example,
when a file is loaded).  In addition to making requests of
the UI, we also need to be able to react to requests from
the UI.  In this case, we need to update the TextBuffer whenever
the text in the TextFrame is updated.

### Entering and Exiting Contexts

Contexts have lifetimes.  The program does not always stay in the same
context, so we will be entering new contexts and exiting them when
they are finished.  In the case of the TextEditing context, we want
to enter it when the program starts and exit it when the program
ends.

In the case of the FileLoading context, we want to enter the
context when the user presses a certain key.  We then want to
exit the context when we have finished loading the file.  However,
we have not yet specified where the code for entering the
FileLoading context should exist.

In fact, it depends on the program, but normally I will create
a new context for this kind of functionality.  We can call it
the CommandSelection context.  The CommandSelection context is
also entered at the start of the program and exited at the end
of the program.  The role of the CommandSelection context is
simply to start new Contexts.

For UI, the ComandSelection context may require a set of KeyAccelerators,
and/or a MenuBar.  It defines a set of commands and when the UI
objects detect a certain key stroke, they request the Interaction
to run the approapriate command in the CommandSelection context.
As I said, these commands usually simply enter a new Context.  In our 
program we need a command to enter the FileLoading context.  The File 
Loading context, automatically exits when it is finished loading the file.

It is important to understand that Contexts are not modal.  TextEditing
and CommandSelection are both active during the entire lifetime
of the program.  When CommandSelection enters the FileLoading
context, all three Contexts are active at the same time.

### Advantages and Disadvantages

There are several advantages to MCI.  The main advantage is in clearly
separating Model implementation from business logic from UI.
We can implement the UI objects any way we want and as long as
they adhere to the Interaction interface, they will work.  We can
even create a bridge pattern to allow different UI implementations
on different platforms.

While this advantage is large, the bigger advantage is in creating
testable UIs.  Each user interaction context now has an Interaction
describing the responsibilities of the UI objects and the business
logic.  We can easily write tests to verify that the UI objects perform
it's responsibilities.  We can also write tests that simulate the
UI to independently test the business logic.

There are also a few disadvantages to this approach.  The main one is
wordiness.  Planning all the Contexts and implementing all of the
Interactions can be a lot of typing in some languages.

Another somewhat strange result of using MCI is that business logic
is usually no longer Object Oriented.  Instead of organizing your
program around data structures and defining the operations they
provide, your rather organize your program around activities in
the program.  The focus of the Contexts is on "how" the activity
will be performed rather than on "what" is required.  After a considerable
amount of thought, I've concluded that this kind of procedural logic
suits user interaction description better than OO.  It can be
somewhat jarring when you encounter it in an otherwise completely
OO based program.

I have implemented an example Framework that provides MCI for
Java and Swing in my [Daifuku](https://github.com/mikekchar/Daifuku)
project.  It is still under development, but it may give you some
idea of how you might implement it yourself.



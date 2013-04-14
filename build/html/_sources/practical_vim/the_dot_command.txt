The Dot command
****************

This command which is the **"."** on the keyboard basically repeats the last change.
But, from the time I came across this in the book I have quickly come to realize
this is for too powerful, because it does exacty what it advertises.

The **"."** records the actions after we enter the *insert* mode.

Another cool thing in this tip is the usage of **A**. What this basically does is,
moves the cursor to the end of the line and switch into *insert* mode.

The above two commands in combination can save one a lot of keystrokes.

Another important way to handle repeated commands with the use of the *dot* command is by using f{char}

For example::

    var foo = "method("+argument1+","+argument2+")";

Using *f{char}* which here would be f+ would immediately jump to the first 
instance of the *+* and after doing any changes we want using *;* would help 
us find the next instance of *+* and the dot command would help repeat our 
changes.

When these two are used in tandem, can reduce the repetetive work a developer 
needs to do.

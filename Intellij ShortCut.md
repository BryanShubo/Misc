##Navigate
```
1. Ctrl+F12 : list all methods and fields in the class
1. Ctrl+B : navigate to the declaration (This is almost always followed by Ctrl + Alt + Left to get back to where I was (Ctrl + Alt + Right works to “go forward” again)
Ctrl + Alt + B, (Go to implementation)
2. Ctrl+N	Go to class
Ctrl+Shift+N	Go to file
Ctrl+Alt+Shift+N	Go to symbol
Ctrl+H	Type hierarchy
Ctrl+Q open JavaDoc

```


##Create
```
1. Create jUnit Test: Ctrl + Shift + T or Naviage->Test

Use Code completion in Find and Replace panes. Start typing the search string, press Ctrl+Space, and select the appropriate word from the suggestion list.
Use the recent history of searches: with the search pane already open, click find1 to show the list of recent entries.
With the search or replace pane already opened, use Ctrl+R or Ctrl+F to toggle between panes. So doing, the search and replace strings are preserved.
To cancel operation and close the pane, press Escape.
Use multiple selection. For example, if a certain string has been highlighted as a search result, it is possible to add an occurrence of this string to the multiple selection by clicking add_selection_icon (Alt+J) , delete an occurrence from the multiple selection using remove_selection_icon (Shift+Alt+J), or add all the found occurrences to the multiple selection using select_all_occurrences_icon (Ctrl+Shift+Alt+J).

```

##Search
```
14. Alt + F7 : Find usages.
Ctrl+Shift+A : find action


ALT+SHIFT+F10 => Enter arguments for main method


```

##Editing
```

Shift+Delete deletes the entire line (will 'cut' it to clipboard)

Ctrl+Shift+O  reformat code
Ctrl + Alt + T: Surround code block. Another useful stuff.

Ctrl+Shift+J to join lines (pull content of next line up to current line).


Alt + Ins: Works consistently to insert anything. (Add a new class, method etc)

A related navigation shortcut is . Press it when the caret is at the method name of an interface, and you get a pop-up list of all the places where this method is implemented, and you can select which one you want to go to (if there is only one implementation, you go straight there). The same goes for overridden methods.

The opposite of this is Ctrl + U (Go to super-method/super-class). If the caret is at the implementation of a method in an interface (indicated by the little green interface-symbol in the left gutter), this shortcut takes you to the interface itself.

When I want to see all the places where a method or variable is used (which I want to do a lot), I use Ctrl + Alt + F7 (Show usages). This gives you a pop-up list of all the usages, and you can easily navigate to each one. I prefer this over Alt + F7 (Find usages), which gives you the same information, but in a separate pane below.

To find classes, I use Ctrl + N (Go to class), which lets you search using only the capital letters in the class name (“camel humps”), and * as wildcard.

Yet another shortcut I use, both when reading and writing code, is Ctrl + P (Parameter info) at the arguments of methods and constructors, to see the types and names of the parameters.

When it comes to writing code, I use Ctrl + space (Basic code completion) a lot to auto-complete method names, variable names etc (or simply to see which methods are available for a certain object, by trying to auto-complete directly at the dot following the name of the object).

For searching in the current file I use Ctrl-F (Find - probably the least surprising shortcut in this list), F3/Shift + F3 (Find next/previous) to repeat the search, and Ctrl + Shift + F (Find in path) to search in the whole project.

Ctrl + W (Select successively increasing code blocks) is handy when selecting chunks of code. Repeatedly pressing it selects more and more of the code. Useful when searching, indenting, commenting out code etc.

If there are errors in the file, F2/Shift + F2 (Next/previous highlighted error) will jump to them.

I use the sequence Alt + C, N (Show Changes View) to see which files in the project I have modified compared to the subversion repository. To diff the current file against the version in the subversion repository, I use the sequence Alt + C, S, Y (Compare with the Same Repository Version). In the diff view, I use F7/Shift + F7 to navigate between the changes.

When not in the diff view, I use Ctrl + Shift + Alt + Up/Ctrl + Shift + Alt + Down to jump to the parts of the file that have been changed compared to the checked-out version. At each modification point, you see the corresponding part in the checked-out version in a pop-up window.

Finally, I run JUnit tests using Ctrl + Shift + F10.
Edit: One really useful shortcut that I've only started using in the last few months is Ctrl + E. It brings up a pop-up with the 15 most recently used files, and you just arrow down to the one you want and hit enter to navigate to it.


	
Some of the time savers:

Alt + Enter : show intention actions (like Eclipse quick fix)
Ctrl + Alt + V : introduce variable (never type the left hand side of an assignment again)
Ctrl + Shift + Space : smart completion ( even two levels down since IntelliJ 8 )
Ctrl + W : select succesively increasing code blocks. Kind of obvious but a real time saver!

To create a documentation comment for a method or function

Place the caret before the declaration.
Type the opening block comment /**, and press Enter.
Add meaningful description of parameters and return values.

```

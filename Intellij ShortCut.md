
```
1. control+F12  => list all methods in the class
2. control + N => pop out a search box for searching a class
3. ctr +alt+shift+N => pop out a search box for any symbol
4. Go to Declaration. Use this to navigate to the declaration of a class, method or variable used somewhere in the code: Ctrl+B
5. Introduce Variable Refactoring, to create a variable from an expression. This expression may even be incomplete or contain errors. Since version 8, IDEA intelligently selects a likely expression when no text is selected: Ctrl+Alt+V
6. To open any file, not just classes: Ctrl+Shift+N
7. Comment/Uncomment current line or selection: Ctrl+/ and Ctrl+Shift+/
8. Quick JavaDoc Popup to show the JavaDoc of the method or class at the text cursor: Ctrl+Q (Ctrl+J on Mac OS X)
9. Smart Type Completion to complete an expression with a method call or variable with a type suitable in the current Context: Ctrl+Shift+Space

10. Rename refactoring to rename any identifier. Can look in comments, text files and across different languages too: Shift+F6

11. Select in Popup to quickly select the currently edited element (class, file, method or field) in any view (Project View, Structure View or other): Alt+F1

12. Highlight Usages in File. Position the text cursor on any identifier without selecting any text and it will show all places in the file where that variable, method etc. is used. Use it on a throws, try or catch keyword to show all places where the exception is thrown. Use it on the implements keyword to highlight the methods of the implemented interface: Ctrl+Shift+F7

13. By far my favourite all purpose shortcut is Ctrl+Shift+A

It does a search as you type through all the commands in intellij. Not only that but when you find the command you want it also displays the corresponding shortcut key next to it!

14. Alt + F7 : Find usages.

Ctrl + Shift + Enter - automatically completes the code statement you are typing, inserting the quotation marks, brackets, curly braces and other punctuation as necessary.



Ctrl + F11 invokes a dialog with all alphanumeric keys on the keyboard. Selecting one empty will add the current line to bookmarks and mark the line with selected key.

Shift + F11 invokes a list of bookmarks. Pressing a key takes to associated bookmark.



Shift+Delete deletes the entire line (will 'cut' it to clipboard)

Ctrl+Alt+L to reformat and optimize imports

Ctrl+Shift+J to join lines (pull content of next line up to current line).


Alt + Ins: Works consistently to insert anything. (Add a new class, method etc)
Ctrl + Alt + T: Surround code block. Another useful stuff.



Here are the Intellij IDEA keyboard shortcuts I find most useful (listed in roughly the order of usage for me):

The shortcut I use the most is Ctrl + B (Go to declaration), to see what a method does, where a variable is declared etc. This is almost always followed by Ctrl + Alt + Left to get back to where I was (Ctrl + Alt + Right works to “go forward” again).

A related navigation shortcut is Ctrl + Alt + B, (Go to implementation). Press it when the caret is at the method name of an interface, and you get a pop-up list of all the places where this method is implemented, and you can select which one you want to go to (if there is only one implementation, you go straight there). The same goes for overridden methods.

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

```

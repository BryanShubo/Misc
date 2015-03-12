##Navigate
```
1. Ctrl+F12 : list all methods and fields in the class
1. Ctrl+B : navigate to the declaration (This is almost always followed by Ctrl + Alt + Left to get back to where I was (Ctrl + Alt + Right works to “go forward” again)
Ctrl + Alt + B, (Go to implementation)
Ctrl + U (Go to super-method/super-class)
2. Ctrl+N	Go to class
Ctrl+Shift+N	Go to file
Ctrl+Alt+Shift+N	Go to symbol
Ctrl+H	Type hierarchy
Ctrl+Q open JavaDoc

I use Ctrl + Alt + F7 (Show usage
14. Alt + F7 : Find usages.

Ctrl + P (Parameter info) at the arguments of methods and constructors

If there are errors in the file, F2/Shift + F2 (Next/previous highlighted error) will jump to them.


I use the sequence Alt + C, N (Show Changes View) to see which files in the project I have modified compared to the subversion repository. To diff the current file against the version in the subversion repository, I use the sequence Alt + C, S, Y (Compare with the Same Repository Version). In the diff view, I use F7/Shift + F7 to navigate between the changes.
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

Ctrl+Shift+A : find action


ALT+SHIFT+F10 => Enter arguments for main method
I run JUnit tests using Ctrl + Shift + F10.


```

##Editing
```

Shift+Delete deletes the entire line (will 'cut' it to clipboard)

Ctrl+Shift+O  reformat code
Ctrl + Alt + T: Surround code block. Another useful stuff.

Ctrl+Shift+J to join lines (pull content of next line up to current line).

Alt + Enter : show intention actions (like Eclipse quick fix)

Ctrl + Alt + V : introduce variable (never type the left hand side of an assignment again)
Ctrl + Shift + Space : smart completion ( even two levels down since IntelliJ 8 )
Ctrl + W : select succesively increasing code blocks. Kind of obvious but a real time saver!

To create a documentation comment for a method or function: Place the caret before the declaration. Type the opening block comment /**, and press Enter. Add meaningful description of parameters and return values.

```

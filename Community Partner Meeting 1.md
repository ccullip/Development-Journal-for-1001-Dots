## Notes from Daniel

* Possible areas to protect: for loops, while loops, if statements, parentheses, and curly braces are the most important
* Possibly use a repeat function instead of a for loop (better for middle school and early high school)
* How to delete parts of the code (if curly braces are protected, how should the whole block be deleted?)
    * Highlight whole block, click at beginning of block, need something intuitive
* Ability to add blocks and scaffold at will by 9 Dots (group blocks as well)
* Ability to make certain parts of code read only or all of it editable for more advanced coders
* Make parts of for loop uneditable (like semicolons inside expression part) but allow other parts to be edited
* Error checking and colors/design not as important right now but in the future possibly should be implemented
* Insert blocks just by editing dictionary (autonomize the program)
* Use a parser (esprima? recast? escodegen?) to get locations of keywords??

## Remaining questions
* Should we use Recast or Esprima/Escodegen? (Escodegen seems to only allow reformatting? Ruins comments and whitespace)
* Does Josh agree with the top priorities for read-only?
* Most important part to focus on right now is to figure out the parser?
* "Clean up code" button that uses esprima/escodegen or recast?
* Any quick changes to design?
* How should backspace work? Backspace button? Highlight whole block? Click at beginning of block?

## Notes from Josh 

* Definitely Key Word and Brackets+Parenthesis, Must be paired together cannot delete parenthesis separately.
* Delete Whole Block (Using Brackets).
* leave behind conditionals.
* Highlight Feature --> backspace once, highlight the block, then delete whole block.
* Undo is not priority, but inserting is more important, or an autocomplete.
   -> type half of a snippit and then show a list of blocks available.
* limit the autocomplete, like lock behind some functions behind autocomplete.
* Auto indentation, helps students make better more read-able code: auto-formatting.
* Automatic formating after enter. Probably a button so students can see the difference.
* Put our code together in a single/mutliple file(s) --> parceljs. Control the files.
* Visually connect the blocks, so the students understand which block is what, and have different colors to show what text is not            editable.
* Double press Delete/Backspace to confirm that the student wants to removed code.
* The Parser should help identify the parts of the code that we would want to control.
* Don't worry about toggle-able read-only. 
* Block making process to be more streamline.

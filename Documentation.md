## Project Overview

Programming education for students usually begins with a block-based coding program such as Scratch. As students progress into text-based programming around the middle-school level, many experience difficulties with typing, syntax errors, and formatting. To smooth this transition, we have created a platform that provides some of the familiarity of block-based coding while integrating a text editor that limits compiler errors. Teachers can easily customize blocks of code that students can enter into the editor with a mouse click, and common mistakes such as deleting a parenthesis or a curly brace will not be allowed. The vision for the project is that the platform will be able to be adapted for a variety of situations to ensure maximum flexibility in the classroom.

Our text editor is built for Typescript with the Monaco editor developed by Microsoft. Along with prohibiting deleting parenthesis and curly braces, we focused on making the student experience as streamlined as possible. To add pre-defined blocks of code, students select the insert position with their cursor then click the desired button. Deleting a snippet of code is as easy as pressing backspace twice after the last curly brace of the block. The first keypress highlights the code that will be deleted and the second keypress confirms this action. Students can also insert these blocks through autocomplete. Formatting, such as adding a space between an assignment operator and a value, is automatic. 

 The code blocks are modeled as objects contained in a dictionary. Each object has various components such as button text, button color, and the code snippet, that can be modified through changes to this file. Teachers can easily customize the website to their curriculum by adding or removing blocks from the dictionary, without making any direct changes to the HTML or CSS. 
 
 
 
 
 ## System Documentation
 
 ### Table of Contents
 [index.html](#index)  
 [create-editor.js](#createeditor)  
 [globals.js](#globals)  
 [templates.js](#templates)  
 [brick-editor.js](#editor)  
 
 
 <a name="index"/>
 
 ### index.html
 
 * Loads templates.js, globals.js, bundle.js, brick-editor.js, loader.js, and create-editor.js.  
 * Calls addBlocksHTML function that populates editor with blocks from templates.js.  
 * Contains editor container, button container, and resetToParsed button in the body.  
 
 
 <a name="createeditor"/>
 
 ### create-editor.js
 
 * Creates the editor, editor theme, and editor text.  
 * Adds commands to catch backspace and delete.  
 * Adds function to catch changing cursor selection.  
 * Creates autocomplete items from templates.  

 
 <a name="globals"/>
 
 ### globals.js

 * Contains global variables such as editor and editorState.  
 * EditorState is updated after any change.  


 <a name="templates"/>
 
 ### templates.js
 
 Dictionary containing the blocks that will be added to the button container.  
 <u>Structure:</u>  
 <b>"blockName"</b> : "IF" <i>(name to display on the button)</i>  
 <b>"code"</b> : "if (i == true) {\n\t// do something \n}" <i>(code that will be inserted into the editor)</i>  
 <b>"buttonColor"</b> : "#ff3399" <i>(color of block)</i>
 
 
 <a name="editor"/>
 
 ### brick-editor.js
 
 [Adding Blocks](#adding)  
 [AST Functions](#ast)  
 [Deleting Blocks](#deleting)  
 [Editor Interface](#interface)  
 [Helper Functions](#helper)  
 
 <a name="adding"/>  
 
 #### Adding Blocks  
 ---  
 ##### *addBlocksHTML*  
 * Populates the button container with blocks from templates.js upon loading window.  
 ##### *buttonHandler*  
 * Handler for adding ith block to editor  
 * Calls addBlock
 * Resets cursor after after updating buffer  
 ##### *addBlock*
 * Calls findPreviousSibling and findClosestParent
 * Adds the desired block to the AST
 * Returns string of editor text to buttonHandler  
 
 <a name="ast"/>  
 
 #### AST Functions  
 ---  
 ##### *findClosestCommonParent*  
 * Given two cursors, finds the parent node that contains both cursors
 * Given one cursor, finds the parent node
 * Returns the parent node <i>(Note: must be BlockStatement or Program)</i>  
 ##### *findClosestCommonDeletableBlock*  
 * Given two cursors, finds the node that contains both cursors and can be deleted
 * Given one cursor, finds the closest node containing the cursor that can be deleted
 * Returns the deletable node <i>(Note: cannot be BlockStatement or Program)</i>  
 ##### *findPreviousSibling*  
 * Calls findClosestParent to obtain parent node
 * Loops through parent node to find sibling node before cursor
 * Returns the previous sibling node  
 ##### *cursorAtEndOfBlock*  
 * Returns true if cursor is at the end of a block  
 ##### *cursorAtStartOfBlock*  
 * Returns true if the cursor is at the start of a block  
 
 <a name="deleting"/>  
 
 #### __Deleting Blocks__  
 ---  
 ##### *backspaceHandler*  
 * Called when backspace key is pressed  
 * If selection, calls onRangeDelete
 * If no selection, calls onPointBackspace
 ##### *deleteHandler*  
 * Called when delete key is pressed
 * If selection, calls onRangeDelete
 * If no selection, calls onPointDelete
 ##### *onPointBackspace*  
 * If the editor text is parsable, one of the following scenarios will occur:
     * If cursorAtEndOfBlock is true, the block will be highlighted. If the block is already highlighted, it will be deleted.
     * If the cursor is to the right of a parenthesis or brace, do not backspace and call flash.
     * Backspace the character.
 * If the editor text is unparsable but the cursor is on the same line as the last parsable state, then the character will only be backspaced if it is inside a conditional or on a line not containing a conditional.  
 ##### *onPointDelete*  
 * If the editor text is parsable, one of the following scenarios will occur:
     * If cursorAtStartOfBlock is true, the block will be highlighted. If the block is already highlighted, it will be deleted.
     * If the cursor is to the left of a parenthesis or brace, do not delete and call flash.
     * Delete the character.
 * If the editor text is unparsable but the cursor is on the same line as the last parsable state, then the character will only be deleted if it is inside a conditional or on a line not containing a conditional.  
 ##### *onRangeDelete*  
 * If the editor text is parsable, then call deleteSelected to find node to be deleted.
 * If the block is already highlighted, delete the block. Otherwise highlight the block.
 ##### *deleteSelected*  
 * Call closestCommonDeletableBlock 
 * Return node that contains both cursors
 ##### *deleteBlock*  
 * Deletes the block  
 ##### *backspaceChar*  
 * Manually backspaces a character through string manipulation  
 ##### *deleteChar*  
 * Manually deletes a character through string manipulation  
 
 <a name="interface"/>  
 
 #### Editor Interface  
 ---  
 ##### *setValue*  
 * Uses executeEdits to update the editor text
 * Preserves undo/redo stack <i>(Note: editor.setValue destroys the undo/redo stack)</i>
 ##### *resetToParsed*  
 * Resets the editor value to the last parsable state which is stored in editorState.parsableText  
 ##### *getCursor*  
 * Retrieves the cursor position from the editor
 * Offsets column by one to account for the differences in column numbering between recast and monaco.  
 ##### *getSelected*  
 * Returns the selection positions if a selection exists in the editor  
 ##### *positionFromStart*
 * Returns the number of characters from the beginning of the string to before the cursor
 ##### *positionFromEnd*
 * Returns the number of characters from after the cursor to the end of the string
 ##### *highlight*  
 * Highlights a block
 ##### *unhighlight*  
 * Unhighlights a block
 ##### *flash*  
 * Flashes the editor when invalid action occurs <i>(Example: Attempting to delete a parenthesis)</i>  
 
 <a name="helper"/>  
 
 #### Helper Functions  
 ---  
 ##### *isBetweenCursors*  
 * Returns true if a cursor is between two other cursors
 ##### *spansProtectedPunctuation*  
 * Returns true if the text between two cursors contains protected parentheses or braces  
 ##### *getSurroundingProtectedParen*  
 * Returns the cursors outside of the protected paretheses  
 ##### *getSurroundingProtectedBrace*  
 * Returns the cursors outside of the protected braces  
 ##### *onDidChangeCursorSelection*  
 * Called whenever the cursor moves
 * Unhighlights text if highlighted
 * Checks for pasting, cutting, and selection replacing
 ##### *updateEditorState*  
 * If the text is parsable, updates values in the editorState global variable  
 
 

 

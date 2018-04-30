#### Documentation needed:
 * User documentation possibly (tutorials for students). May be better for 9 dots staff to create this.
 * System documentation (for teachers/developers at 9 dots, (parser, dictionary))
 * Project overview (short summary of why it was created, what it can do (autocomplete, adding/deleting blocks, etc), similar to readme)
 * Design decisions (include with project overview, for 9 dots, but not vital as is subject to change)

### Project Overview

Programming education for students usually begins with a block-based coding program such as Scratch. As students progress into text-based programming around the middle-school level, many experience difficulties with typing, syntax errors, and formatting. To smooth this transition, we have created a platform that provides some of the familiarity of block-based coding while integrating a text editor that limits compiler errors. Teachers can easily customize blocks of code that students can enter into the editor with a mouse click, and common mistakes such as deleting a parenthesis or a curly brace will not be allowed. The vision for the project is that the platform will be able to be adapted for a variety of situations to ensure maximum flexibility in the classroom.

Our text editor is built for Typescript with the Monaco editor developed by Microsoft. Along with prohibiting deleting parenthesis and curly braces, we focused on making the student experience as streamlined as possible. To add pre-defined blocks of code, students select the insert position with their cursor then click the desired button. Deleting a snippet of code is as easy as pressing backspace twice after the last curly brace of the block. The first keypress highlights the code that will be deleted and the second keypress confirms this action. Students can also insert these blocks through autocomplete. Formatting, such as adding a space between an assignment operator and a value, is automatic. 

 The code blocks are modeled as objects contained in a dictionary. Each object has various components such as button text, button color, and the code snippet, that can be modified through changes to this file. Teachers can easily customize the website to their curriculum by adding or removing blocks from the dictionary, without making any direct changes to the HTML or CSS. 
 
 ### System Documentation
 
 #### Table of Contents
 [index.html](#index)  
 [create-editor.js](#createeditor)  
 [globals.js](#globals)  
 [templates.js](#templates)  
 [brick-editor.js](#editor)  
 
 
 <a name="index"/>
 
 #### index.html
 
 Loads templates.js, globals.js, bundle.js, brick-editor.js, loader.js, and create-editor.js.  
 Calls addBlocksHTML function that populates editor with blocks from templates.js.  
 Contains editor container, button container, and resetToParsed button in the body.  
 
 
 <a name="createeditor"/>
 
 #### create-editor.js
 
 Creates the editor, editor theme, and editor text.  
 Adds commands to catch backspace and delete.  
 Adds function to catch changing cursor selection.  
 Creates autocomplete items from templates.  

 
 <a name="globals"/>
 
 #### globals.js

 Contains global variables such as editor and editorState.  
 EditorState is updated after any change.  


 <a name="templates"/>
 
 #### templates.js
 
 Dictionary containing the blocks that will be added to the button container.  
 <u>Structure:</u>  
 <b>"blockName"</b> : "IF" <i>(name to display on the button)</i>  
 <b>"code"</b> : "if (i == true) {\n\t// do something \n}" <i>(code that will be inserted into the editor)</i>  
 <b>"buttonColor"</b> : "#ff3399" <i>(color of block)</i>
 
 
 <a name="editor"/>
 
 #### brick-editor.js
 
 

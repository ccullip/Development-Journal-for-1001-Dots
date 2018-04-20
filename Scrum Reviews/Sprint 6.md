### What we were planning to do:
* Add undo button when unparsable
* Revert back to last correct version when button is pressed
* Autocomplete
### What we have done:
* Autocomplete works but not yet implemented
* Added undo button and revert back to last stage when button is pressed
* Changed highlighting to no pop-up box
* Restrict deletion of () and {}
* Use executeEdits instead of editor.setValue to preserve undo/redo stack
### What we could’ve done better:
* More work on the uneditable parts of code
### What was not done, and why?
* The rest of the autocomplete -- other time commitments
* Finish the PR for undo and autocomplete branch

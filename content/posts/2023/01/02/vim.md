---
title: "Vim"
date: 2023-01-02T15:25:30-05:00
draft: false
tags: [vim]
---

Vim is a free and open-source, screen-based text editor program.\
Use the built in tutorial program by using `vimtutor`.

Vi stands for Visual. It is a text editor that is an early attempt to a visual text editor.\
Vim stands for Vi IMproved and is an implementation of the Vi standard with many additions.

| Key | Shortcut |
|----|----|
|hjkl| These keys can be used in place of arrow keys|
| u | Undo |
| ctrl + r | Redo |
| :wq | Write and Quit |
| :q | Quit |
| :q! | Quit and Dismiss Changes |

## Insert Mode
| Key | Shortcut | Shift |
|----|----|----|
| esc | Exit insert mode |
| i | Insert before the cursor | Insert start of the line |
| a | Insert after the cursor | Insert end of the line |
| o | Insert new line below cursor | Insert above current line |
| ea | Insert text at the end of the word |

## Editing
| Key | Shortcut | Shift |
|----|----|----|
| r | Replace a single character |
| s | Delete a character and insert mode |
| ce | Delete the word and enter insert mode |
| cc | Delete line and enter insert mode |
| ci" | Change inner quotations marks | 
| %s/oldword/newword/g | Replace all occurances of a word |
| . | Execute the command you just did |

## Visual Mode
| Key | Shortcut | Shift | 
|----|----|----|
| v | Enter visual mode | Mark in line mode |
| ctrl + v | Mark in block mode |
| aw | Mark a word |
| d | Deletes what is selected and leaves visual mode |
| y | Copy | 
| yy | Copy line |
| dd | Cut the entire line |
| p | Paste before | Paste after |

## Delete
| Key | Shortcut | Shift | 
|----|----|----|
| d | Delete what is selected | Delete the rest of the line from cursor |
| d$ | Delete the rest of the line from cursor |
| dd | Cut the entire line |
| #dd | Delete multiple lines |
| :#,#d | Delete a range of lines |
| dd | Delete line |
| dw | Delete word |
| ctrl + w | Delete word before cursor |
| d2w | Delete 2 word |

## Navigation
| Key | Shortcut | Shift | 
|----|----|----|
| % | Jump to closing bracket |
| t* | Jump to before the * |
| f* | Jump to the * |
| zz | Center the cursor |
| b | Move to start of a word |
| w | Move to start of next word |
| e | Move to the end of the word |
| 0 | Jump to the start of the line | 
| $ | Jump to the end of the line |

## Searching
| Key | Shortcut | Shift | 
|----|----|----|
| /buh | Search forward for a word|
| ?buh | Search backward for the specified pattern |
| n | Move the search in the same direction | Move the search in the opposite direction | 

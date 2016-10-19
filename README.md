Vim refresher
======================
2016-10-17



Some refresher notes about vim


Modal editing
--------------------
- normal mode: navigate the structure of the file
- insert mode: editing the file
- visual mode: highlight portions of the file to manipulate at once
- ex mode: command mode



Shortcuts
--------------

- hjkl: instead of arrows
- ^E - scroll the window down
- ^Y - scroll the window up
- ^F - scroll down one page
- ^B - scroll up one page
- H - move cursor to the top of the window
- M - move cursor to the middle of the window
- L - move cursor to the bottom of the window
- gg - go to top of file
- G - go to bottom of file
- w - go to the beginning of the next word
- b - go to the beginning of the previous word
- e - go to the end of the next word
- u - undo
- ctrl + r - redo
- dd / yy: delete/yank the current line
- D/C - delete/change until end of line
- ^/$ - move to the beginning/end of line
- I/A - move to the beginning/end of line and insert
- o/O - insert new line below/above current line and insert
- p/P - paste the clipboard below/above the current line
- m{posName}/`{posName} - mark/goto the caret position with name {posName}




The secret sauce
----------------------

- text objects and motions
- the DOT command
- macros


### text objects and motions

text objects:
- w: words
- s: sentences
- p: paragraphs
- t: tags (html/xml)


motions:
- a - all
- i - in
- f/F - find forward/backward
- t/T - find 'til forward/backward (stop just before it reaches the actual character)
- / - search forward (up to the next match)
- ? - search backward (up to the next match)


#### Mix with commands

- d: delete (also cut)
- c: change (delete, then place in insert mode)
- y: yank (copy)
- v: visually select
- >: indent


{number}?{command}{text object or motion}

- diw: delete in word
- caw: change all word
- yi): yank all text inside parentheses
- ci): change all text inside parentheses
- di[: delete all text inside square brackets
- da[: delete all text inside square brackets, AND the square brackets
- dt(space): delete until the space
- va": visually select all inside double quotes, including double quotes
- c/ot: change all until the next occurrence of 'ot'
- cc: change current line
- c6j: change 6 lines below (down), including the current line
- yypVr= - copy the current line (yy), paste it below (p), select it (V) and replace it with = symbols (r=)
- %s/#/"/g - replace all sharps (#) by double quotes (") in the document

### the DOT command

- .: Repeats the last motion

For instance ci', change the text inside quotes, then you can repeat this motion again in other locations.


### macros

A sequence of commands recorded to a register.


#### record a macro

- q{register}
- (do the things)
- q

#### play a macro
- @{register}




Ctrl+r{register} (Insert mode): insert the content of {register}




Commands
-----------------
- general
	- :h {expression} - display help for {expression}
	- :wall - write all
	- :e - edit a file
	- :normal! {expression} - execute the {expression} exactly as typed
- windows
	- :sp - split window by drawing an horizontal line
	- ctrl+w s - alias for :sp
	- :vsp - split window by drawing a vertical line
	- ctrl+w v - alias for :vsp
	- :res {n} - resize current window so that it spans {n} lines
	- ctrl+w (x2) - move between the panes
	- ctrl+w = - resize all windows to an equal size
	- ctrl+w o - open the current window so that it takes the whole screen
	- ctrl+w c - close the current window
	- ctrl+w {h|j|k|l} - jump to the window on the {left|down|up|right} side
	- ctrl+w {number}? +/- - increase/decrease the size of the current window by {number} lines
- registers	
	- :registers - list the registers
	- "{register}yiw - copy the current word to register {register}
	- "{register}p - paste the content from register {register}
- buffers
	- :ls - list the buffers
	- :ls! - list the buffers, including hidden buffers
	- :b{buffer} - go to buffer {buffer}
	- :b# - go to the last buffer
	- :bd{buffer,...}? - delete the current buffer, or the specified {buffer}
	- :22,24bd - delete buffers 22 to 24
	- :%bd - delete all buffers
	- :find - go to a buffer
	- :edit - edit to a buffer
	- :bnext - go to the next file in the buffer
	- :bn - go to the next file in the buffer
	- :bp - go to the previous file in the buffer
	- :bufdo {command}- execute {command} on all files in the buffer
	- :bufdo g/"\s*Hithere/d - delete the Hithere expression in all files in the buffer
- args	
	- :n - go to next thing in the arg list
- tabs:
	- :tabedit {file} - open the {file} in a new tab
	- :tabs: list all tabs
	- gt - go to the next tab
	- gT - go to the previous tab
	- {i}gt - go to tab number {i}, starting at 1 left to right


Plugins
--------------
- top 5
	- vundle: plugin manager
	- nerdtree: file drawer
		- :NERDTree - open the nerd tree
		- i - open split
		- q - quit
		- s - open vsplit
		- cd - change to the  directory under cursor
		- C - change root to the directory under cursor
		- B - list the bookmarks
		- :Bookmark {name} - create the {name} bookmark
	- ctrlp: fuzzy file finder
	- fugitive: git tool
	- syntastic: syntax checker / linter

- motion
	- Surround
		- delete change add surrounding things
		- ds" - delete the surrounding quotes
		- cs"' - change surrounding double quotes with single quotes
		- ysiw" - add surrounding double quotes to the inner word 
		- csth2 - change the surrounding tag with h2
	- Commentary
		- toggle comments
		- cml - comment the line to the right (l)
		- cmj - comment the line below (j), including the current line
		- cmip - comment the paragraph
	- ReplaceWithRegister
		- griw: replace the inner word with the register
	- Titlecase
		- gti': title case inside single quotes
		- gtip: title case the inner paragraph
	- Sort-motion
		- gsip: sort the inner paragraph
	- System-copy
		- cpi' - copy all inside single quote
		- cpip - copy all inside paragraph

- custom text objects
	- Indent
		- describe an indented section
		- cmii: comment the inner indented section
		- cmai: comment the inner indented section (and sublevels)
	- Entire
		- cmae:	comment the entire document
		- dae:	delete the entire document
	- Line
		- cil: change inner line (without the leading indentation)
	- Ruby block





Configuration
---------------------

set relativenumber





Features without plugins (just for fun)
=================

- fuzzy file search
- tag jumping
- autocomplete
- file browsing
- snippets
- build integration



.vimrc
----------

https://github.com/mcantor/no_plugins/blob/master/no_plugins.vim

```vim
" BASIC SETUP:

" enter the current millenium
set nocompatible

" enable syntax and plugins (for netrw)
syntax enable
filetype plugin on

" FINDING FILES:

" Search down into subfolders
" Provides tab-completion for all file-related tasks
set path+=**

" Display all matching files when we tab complete
set wildmenu

" NOW WE CAN:
" - Hit tab to: find by partial match
" - Use * to make it fuzzy

" THINGS TO CONSIDER:
" - :ls shows the recently opened files (in your buffer)
" - :b lets you autocomplete any open buffer
" - :b substring of a line result by :ls directly jumps to the corresponding file 
" for instance, if :ls gives you two results:
" - file_one.txt
" - file_two.php
" you could jump to file_two.php by typing :b hp (or any substring of file_two.php)




" AUTOCOMPLETE:

" The good stuff is documented in |ins-completion|

" HIGHLIGHTS:
" - ^x^n for JUST this file
" - ^x^f for filenames (works with our path trick!)
" - ^n for anything specified by the 'complete' option

" NOW WE CAN:
" - Use ^n and ^p to go back and forth in the suggestion list



```








Related
-------------
- [vim decent navigation](https://github.com/lingtalfi/vim-decent-navigation)
- [vim survivor kit](https://github.com/lingtalfi/vim-survivor-kit)
- [vim refresher notes](https://github.com/lingtalfi/vim-refresher-notes)





Sources
-------------
- videos
	- https://www.youtube.com/watch?v=5r6yzFEXajQ
	- https://www.youtube.com/watch?v=XA2WjJbmmoM
	- https://www.youtube.com/watch?v=wlR5gYd6um0
	- Your First Vim Plugin: https://www.youtube.com/watch?v=lwD8G1P52Sk
	- Stephen Belcher - Registers (Intermediate): https://www.youtube.com/watch?v=sf1prtd_2E8
	- Working with many files step 1: https://www.youtube.com/watch?v=5-Uaeps421w
	- Working with many files step 2: https://www.youtube.com/watch?v=NSTSz8riL2M
	- Working with many files step 3: https://www.youtube.com/watch?v=U0CZsdzNJCQ
	- Vim Essential Plugin: NERDTree: https://www.youtube.com/watch?v=CPu9mDpSYj0
- pages
	- Basic Mapping: http://learnvimscriptthehardway.stevelosh.com/chapters/03.html 






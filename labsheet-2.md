# Labsheet 2: Using the VIM editor in command line

___

## Objectives

1. To understand the basics of vim editor.

## Theory  
  
Vim is a highly configurable text editor built to make creating and changing any kind of text very efficient. It is included as `vi` command with most UNIX systems and with macOS. It is one of the most ubiquitous, popular and recognizable text editor in the world, particularly known for its steep learning curve among beginners. However, it has many benefits, including:

1. persistent, multi-level undo tree
2. extensive plugin system
3. support for hundreds of programming languages and file formats
4. powerful search and replace
5. integrates with many tools

## Activity

### Creating and editing a file with vim

Vim has two modes: 1. Command mode, and 2: Insert mode. The command mode is used to insert commands that does various things, such as saving, overriding, appending, deleting, creating and updating files. The insert mode is used to actually insert text into the file. Insert mode is entered by pressing `i` on the keyboard, while the command mode is accessed by pressing the `esc` key.

1. Opening terminal via `⌘ + space` and entering `terminal`,
2. Changing to the necessary directory with `cd /path/to/directory`,
3. Entering the command `vi filename.txt` to create and open a new text file with vim,
![Editing with vim](/images/vi-enter.png)
4. Clicking on the `i` key to enter the `insert` mode and entering the text,
5. Clicking on `esc` once done to enter the command mode, and entering `:w` to write the text,
![Editing with vim](/images/vi-edit.png)
6. Entering `:wq` to exit.

## Observation and Conclusion

Hence, we observed and learnt how to use vim, a powerful text editor on the shell on UNIX based systems.

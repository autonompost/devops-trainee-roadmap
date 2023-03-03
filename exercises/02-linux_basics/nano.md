# Nano Editor Tutorial

1. Go to you home directory: _cd_
2. Create a new file with: _touch nanofile.txt_
3. Open the file in Nano: _nano nanofile.txt_
3. Edit the file: Once you have the file open in Nano, you can start editing it. You can move the cursor around the file using the arrow keys, and you can insert or delete text using the usual keyboard shortcuts. Nano displays a menu of basic shortcuts at the bottom of the screen to help you get started.
4. Save the changes: To save the changes you've made to the file, simply press Ctrl+O (that's the "O" key, not zero) to write the file to disk. You'll be prompted to confirm the filename - just press Enter to use the same filename as before.
5. Exit Nano: When you're finished editing the file, you can exit Nano by pressing Ctrl+X. If you've made changes to the file that you haven't saved yet, you'll be prompted to save them before exiting.

## The configuration file

Nano also has a configuration file. The documentation for the options can be found at [nanorc files](https://www.nano-editor.org/dist/latest/nano.html#Nanorc-Files)

```shell
nano ~/.nanorc # this opens nano with the existing or a new file for .nanorc in your $HOME directory
```

Example: Add the following line, then save and quit the editor
```shell
set linenumbers
```

Open your _nanofile.txt_ again and you should have line numbers on the left side. Exit the file and delete it
```shell
rm nanofile.txt
```
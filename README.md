vim-watch_for_changes
=====================

Make vim ultra sensitive about external changes to files

Note:
=====

This is not my vim script. I've taken it from [a very helpful page on the Vim wiki](http://vim.wikia.com/wiki/Have_Vim_check_automatically_if_the_file_has_changed_externally).

I've merely turned it into a plugin so that it plays nicely with [Vundle](https://github.com/gmarik/vundle). I was previously manually loading it with an absolute path via Vundle, and it was breaking for other people that used my vim config, [of which there are a couple](https://github.com/gee-forr/vim-files/stargazers)

Instructions:
=============

If you are using a console version of Vim, or dealing
with a file that changes externally (e.g. a web server log)
then Vim does not always check to see if the file has been changed.
The GUI version of Vim will check more often (for example on Focus change),
and prompt you if you want to reload the file.

There can be cases where you can be working away, and Vim does not
realize the file has changed. This command will force Vim to check
more often.

Calling this command sets up autocommands that check to see if the
current buffer has been modified outside of vim (using checktime)
and, if it has, reload it for you.

This check is done whenever any of the following events are triggered:
* BufEnter
* CursorMoved
* CursorMovedI
* CursorHold
* CursorHoldI

In other words, this check occurs whenever you enter a buffer, move the cursor,
or just wait without doing anything for 'updatetime' milliseconds.

Normally it will ask you if you want to load the file, even if you haven't made
any changes in vim. This can get annoying, however, if you frequently need to reload
the file, so if you would rather have it to reload the buffer *without*
prompting you, add a bang (!) after the command (WatchForChanges!).
This will set the autoread option for that buffer in addition to setting up the
autocommands.

If you want to turn *off* watching for the buffer, just call the command again while
in the same buffer. Each time you call the command it will toggle between on and off.

WatchForChanges sets autocommands that are triggered while in *any* buffer.
If you want vim to only check for changes to that buffer while editing the buffer
that is being watched, use WatchForChangesWhileInThisBuffer instead.

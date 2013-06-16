# MiniBufExpl

This is a fork of [Bindu Wavell][]'s [MiniBufExpl][] plugin for [Vim][].

[Federico Holgado][] started this fork and made lots of improvements. It is
currently maintained by [Techlive Zheng][], the development has been moved to
[@techlivezheng's repo][], only new version will be released to [@fholgado's
repo][].

[Vim]: http://vim.org
[MiniBufExpl]: http://www.vim.org/scripts/script.php?script_id=159
[Techlive Zheng]: http://techlivezheng.me
[Federico Holgado]: http://www.fholgado.com
[@fholgado's repo]:https://github.com/fholgado/minibufexpl.vim
[@techlivezheng's repo]: https://github.com/techlivezheng/vim-plugin-minibufexpl

## The Story

>The reason why I took it upon myself to improve MiniBufExplorer is a matter of
need. I am a User Interface designer who spends a lot of time writing front-
end code. I recently found Vim and fell in love with it. During my search for
the plugins that would help me the most, I came across MBE. I loved it
initially, but quickly saw that it had some major flaws.

>After using MBE for some time, I have been able to identify some areas that
needed some dire attention from a usability standpoint. I am doing my best to
fix those issues without adding "feature bloat" or other unnecessary things to
MBE. I am always open to suggestions and discussion as to what we can do to
improve this great plugin.

>I would also like to thank [Bindu Wavell][], who is the plugin's original
creator and [Oliver Uvman][], who like myself has been hacking at MBE to make
needed improvements. My goal is to consolidate the code and act as the
maintainer so that any further changes from contributors can be found in a
single location.

[Bindu Wavell]: http://www.wavell.net
[Oliver Uvman]: https://github.com/OliverUv

-- Federico Holgado

>This is a very useful plugin, being able to see the buffer status in a
tab-like fashion while you are working with mutiple buffers is very pleasant.
Since @fholgado began to improve this plugin, lots of new features has been
added, it's great. Meanwhile, there are still some annoying bugs that haven't
been fixed for a long time, so I decide to step out and do something.

-- Techlive Zheng

## Improvements in Version 6.5.0

### Bugfixes

Squashed almost every known bugs due to the relase of version 6.5.0, for more
details, please check out the 6.5.0 milestones.

* https://github.com/fholgado/minibufexpl.vim/issues?milestone=1&page=1&state=closed
* https://github.com/techlivezheng/vim-plugin-minibufexpl/issues?milestone=1&page=1&state=closed

### Buffer With No Name

Buffer without a name would be shown as `[1:--NO NAME--<timestamp>]` now.

### User Interface Change

Options, commands and key bindings have some changes, please see changelog for
more details.

### Cycle Buffer in MRU Fashion

As a long expected feature, command ':MBEbf' or ':MBEbb' could be used to cycle
the buffer forwards or backwards in the most recently used order.

### Handle Buffers with Duplicate Name

Mechanism for checking buffers with duplicate name has been totally refactored,
it is now more efficient.

Mechanism for generating unique name for these buffers has been refactored too,
each buffer should be uniquely identified now.

    ./test             -->  test
    ./alpha/foo/test   -->  alpha/foo/test
    ./alpha/bar/test   -->  alpha/bar/test
    ./beta/new/test    -->  beta/-/test
    ./omega/old/test   -->  omega/old/test
    ./omega/test       -->  omega/test

### MBE Window is Local to Tab Page

Open or close MBE window in one tab page would not interfere another. Commands
':MBEOpenAll', ':MBECloseAll' and ':MBEToggleAll' have been introduced to mani-
pulate MBEs in all tab pags.

### Preserve Window Entering History

Previous versions of MBE will interfere the window entering history on updating,
this behavior has caused many incompatibilities with other plugins. It should
be fixed now, 'wincmd p' would work as usual.

### Quit MBE if No More Normal Window Open

MBE now will be closed if all the other open windows are plugin windows.

### Delete/Wipeout/Unload Buffers Preserving the Window

Commnad ':MBEbd', ':MBEbw' or ':MBEbun' could be used to delete/wipeout/unload
buffers just as ':bd', ':bw' or ':bun', but the window that previously holding
them will be preserved.

## Improvements in Previous Versions

### Current Buffer Highlighting

Previously, MBE would only tell you if a buffer was currently visible in the
editor like such:

![][current_buffer_old]

[current_buffer_old]: http://dl.dropbox.com/u/118650/mbe/screenshots/current_buffer/old.png

Now, MBE shows you the buffer that is currently visible _and_ active in the
editor. Here is an animated GIF that shows the current buffer highlighting in
action:

![][current_buffer_new]

[current_buffer_new]: http://dl.dropbox.com/u/118650/mbe/screenshots/mbe1.gif

### Duplicate Buffer Names

If you are an MBE user, I am sure you are familiar with the following
scenario:

![][dup_buf_names_old]

[dup_buf_names_old]: http://dl.dropbox.com/u/118650/mbe/screenshots/dupe_buf_names/old_fade.png

The problem is that buffers with the same filename do not get differentiated,
and it makes it very hard to find the buffer you are trying to edit. The
simple solution is to show a parent directory that is different between all
buffers like such:

![][dup_buf_names_new]

[dup_buf_names_new]: http://dl.dropbox.com/u/118650/mbe/screenshots/dupe_buf_names/new_fade.png

Let me explain how it works. Let's observe 2 files that have the same
filename.

    /Users/fholgado/Sites/website1/css/style.css
    /Users/fholgado/Sites/website2/css/style.css

You'll notice both files have the same filename _and_ are in a folder called
'css'. This happens all the time in web development projects.

In order to differentiate the two files, MBE now crawls up the directory tree
and finds the first parent directory that differs from both files, which in
this case is 'website1' and 'website2'. MBE will now show you these 2 files as
such:

    [1:website1/style.css][2:website2/style.css]

### Buffer States

It is always important to be able to see at a glance what buffers are modified
and need to be saved. MBE now shows you respective colors whether the buffer
is modified or not modified.

![][buffer_status]

[buffer_status]: http://dl.dropbox.com/u/118650/mbe/screenshots/save_states/new.png

**Most importantly**, MBE now updates the buffer states immediately after
making changes, instead of the previous behavior that only updated buffer
states when switching buffers.

### Status Line Clutter

Previously, the MBE buffer would use the same statusline that is currently
configured for Vim. This adds a lot of visual clutter to MBE and does not add
any functionality, since the status line is showing information for a buffer
that does not contain any real content.

![][stauts_line_clutter_old]

[status_line_clutter_old]: http://dl.dropbox.com/u/118650/mbe/screenshots/status_line/old.png

MBE now uses it's own custom Status Line format to reduce the unwanted
information. This line is customizable and can even be empty.

![][status_line_clutter_new]

[status_line_clutter_new]: http://dl.dropbox.com/u/118650/mbe/screenshots/status_line/new.png

### Window Auto Resizing

Previously, the MBE buffer made the automatic window resizing using the ctrl +
w + = command in Vim. Many of you have seen the following picture:

![][window_auto_resizing_old]

[window_auto_resizing_old]: http://dl.dropbox.com/u/118650/mbe/screenshots/window_resizing/old.png

MBE now maintains it's buffer size both in horizontal and vertical mode when
using window resizing commands. Now you can take a Vim tab that looks like
this:

![][window_auto_resizing_new1]

[window_auto_resizing_new1]: http://dl.dropbox.com/u/118650/mbe/screenshots/window_resizing/new1.png

And turn it into something like this without worrying about the MBE window
becoming large as well:

![][window_auto_resizing_new2]

[window_auto_resizing_new2]: http://dl.dropbox.com/u/118650/mbe/screenshots/window_resizing/new2.png

### Customizing Colors

Here are all the color additions to customize MBE's new features. You can add
the following to your Color file and customize the color accordingly:

    " MiniBufExpl Colors
    hi MBENormal               guifg=#808080 guibg=fg
    hi MBEChanged              guifg=#CD5907 guibg=fg
    hi MBEVisibleNormal        guifg=#5DC2D6 guibg=fg
    hi MBEVisibleChanged       guifg=#F1266F guibg=fg
    hi MBEVisibleActiveNormal  guifg=#A6DB29 guibg=fg
    hi MBEVisibleActiveChanged guifg=#F1266F guibg=fg

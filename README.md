# MiniBufExpl

I've been working on improving [MiniBufExpl][], a plugin for [Vim][].

[Vim]: http://vim.org
[MiniBufExpl]: http://www.vim.org/scripts/script.php?script_id=159

## The story: Why am I doing this?

The reason why I took it upon myself to improve MiniBufExplorer is a matter of
need. I am a User Interface designer who spends a lot of time writing front-
end code. I recently found Vim and fell in love with it. During my search for
the plugins that would help me the most, I came across MBE. I loved it
initially, but quickly saw that it had some major flaws.

After using MBE for some time, I have been able to identify some areas that
needed some dire attention from a usability standpoint. I am doing my best to
fix those issues without adding "feature bloat" or other unnecessary things to
MBE. I am always open to suggestions and discussion as to what we can do to
improve this great plugin.

I would also like to thank [Bindu Wavell][], who is the plugin's original
creator and [Oliver Uvman][], who like myself has been hacking at MBE to make
needed improvements. My goal is to consolidate the code and act as the
maintainer so that any further changes from contributors can be found in a
single location.

[Bindu Wavell]: http://www.wavell.net
[Oliver Uvman]: https://github.com/OliverUv

## Improvements

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

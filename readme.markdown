# MiniBufExplorer

I've been working on improving MiniBufExplorer, a plugin for [Vim][1].

   [1]: http://vim.org

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

I would also like to thank [Bindu Wavell][2], who is the plugin's original
creator and [Oliver Uvman][3], who like myself has been hacking at MBE to make
needed improvements. My goal is to consolidate the code and act as the
maintainer so that any further changes from contributors can be found in a
single location.

   [2]: http://www.wavell.net/
   [3]: https://github.com/OliverUv

## New and Improved Features

  1. Highlight currently active buffer
  2. Show differentiating parent directory with multiple buffers with the same filename
  3. Custom non-intrusive status line
  4. Update buffer name color according to buffer state (modified or unmodified) immediately after changes are made
  5. Prevents resizing of MBE buffer by window resizing commands

## Features Overview

### Current Buffer Highlighting

Previously, MBE would only tell you if a buffer was currently visible in the
editor like such:

![][6]

   [6]: http://dl.dropbox.com/u/118650/mbe/screenshots/current_buffer/old.png

Now, MBE shows you the buffer that is currently visible _and_ active in the
editor. Here is an animated GIF that shows the current buffer highlighting in
action:

![][7]

   [7]: http://dl.dropbox.com/u/118650/mbe/screenshots/mbe1.gif

### Duplicate Buffer Names

If you are an MBE user, I am sure you are familiar with the following
scenario:

![][8]

   [8]: http://dl.dropbox.com/u/118650/mbe/screenshots/dupe_buf_names/old_fade.png

The problem is that buffers with the same filename do not get differentiated,
and it makes it very hard to find the buffer you are trying to edit. The
simple solution is to show a parent directory that is different between all
buffers like such:

![][9]

   [9]: http://dl.dropbox.com/u/118650/mbe/screenshots/dupe_buf_names/new_fade.png

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

### Buffer Save States

It is always important to be able to see at a glance what buffers are modified
and need to be saved. MBE now shows you respective colors whether the buffer
is modified or not modified.

![][10]

   [10]: http://dl.dropbox.com/u/118650/mbe/screenshots/save_states/new.png

**Most importantly**, MBE now updates the buffer states immediately after making changes, instead of the previous behavior that only updated buffer states when switching buffers.

### Status Line Clutter

Previously, the MBE buffer would use the same statusline that is currently
configured for Vim. This adds a lot of visual clutter to MBE and does not add
any functionality, since the status line is showing information for a buffer
that does not contain any real content.

![][11]

   [11]: http://dl.dropbox.com/u/118650/mbe/screenshots/status_line/old.png

MBE now uses it's own custom Status Line format to reduce the unwanted
information. This line is customizable and can even be empty.

![][12]

   [12]: http://dl.dropbox.com/u/118650/mbe/screenshots/status_line/new.png

### Window Resizing

Previously, the MBE buffer made the automatic window resizing using the ctrl +
w + = command in Vim. Many of you have seen the following picture:

![][13]

   [13]: http://dl.dropbox.com/u/118650/mbe/screenshots/window_resizing/old.png

MBE now maintains it's buffer size both in horizontal and vertical mode when
using window resizing commands. Now you can take a Vim tab that looks like
this:

![][14]

   [14]: http://dl.dropbox.com/u/118650/mbe/screenshots/window_resizing/new1.png

And turn it into something like this without worrying about the MBE window
becoming large as well:

![][15]

   [15]: http://dl.dropbox.com/u/118650/mbe/screenshots/window_resizing/new2.png

### Customizing Colors

Here are all the color additions to customize MBE's new features. You can add
the following to your Color file and customize the color accordingly:
    
    			" MiniBufExpl Colors
    			hi MBEVisibleActive guifg=#A6DB29 guibg=fg
    			hi MBEVisibleChangedActive guifg=#F1266F guibg=fg
    			hi MBEVisibleChanged guifg=#F1266F guibg=fg
    			hi MBEVisibleNormal guifg=#5DC2D6 guibg=fg
    			hi MBEChanged guifg=#CD5907 guibg=fg
    			hi MBENormal guifg=#808080 guibg=fg

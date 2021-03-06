
# ensime-vim

[![Join the chat at https://gitter.im/ensime/ensime-vim](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/ensime/ensime-vim?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![Build Status](https://drone.io/github.com/yazgoo/ensime-vim/status.png)](https://drone.io/github.com/yazgoo/ensime-vim/latest)
[![Coverage Status](https://coveralls.io/repos/yazgoo/ensime-vim/badge.svg?branch=master&service=github)](https://coveralls.io/github/yazgoo/ensime-vim?branch=master)

ENSIME for the Editor of the Beast (Vim)

# demo

![alt tag](https://raw.github.com/yazgoo/ensime-vim/master/doc/demo.gif)

# howto

You need `websocket-client` python package:

    $ sudo pip install websocket-client

You should also export your BROWSER variable, for example in your bashrc:

    export BROWSER=firefox

All the following commands should be run from your scala directory.

First you need ensime sbt plugin:    
    
    $ echo 'addSbtPlugin("org.ensime" % "ensime-sbt" % "0.1.7")' \
        >> ~/.sbt/0.13/plugins/plugins.sbt

Then, generate .ensime file:

    $ sbt gen-ensime

Then install vim plugin, with [Vundle](https://github.com/VundleVim/Vundle.vim),
by adding to your .vimrc:

    Plugin 'ensime/ensime-vim'

Or if you're using neovim, with [vim-plug](https://github.com/junegunn/vim-plug)
by installing neovim python module:

    $ pip install neovim

and by adding to your .nvimrc:

    Plug 'ensime/ensime-vim'

Then by doing a :PlugInstall and a :UpdateRemotePlugins under neovim

Finally, launch vim with the file(s) you want to edit:

    $ vim src/scaloid/example/HelloScaloid.scala

# event handling

Under neovim, for all commands except autocomplete, events are only handled when you move your cursor (CursorMoved event).
Under vim, we use [CursorHold](http://vim.wikia.com/wiki/Timer_to_execute_commands_periodically) event.

# using ensime-vim

[User documentation](doc/ensime-vim.txt) is available, you can also load it inside vim via:

    :help ensime-vim

# developer howto

vim plugin is generated from neovim plugin.
You should install neo2vim ruby gem:

    $ gem install neo2vim

Then you should do your modifications to:

    rplugin/python/ensime.py 
    
And export them to vim plugin format via:

    $ neo2vim rplugin/python/ensime.py ftplugin/scala_ensime.vim

All merges should be done on dev branch before being merged onto master

# integrating with your own plugin

It is possible to register callbacks and send events to ensime.
Check [this plugin example](https://github.com/yazgoo/ensime-vim-typecheck).

# developer info

Needs some love. Please get in contact if you would like to help! There was some old work that is no longer compatible with the ENSIME server but it may serve as a good starting place:

* https://github.com/megaannum/vimside
* https://github.com/jlc/envim
* https://github.com/psuter/vim-ensime \ https://github.com/andreypopp/ensime

Reference launch script is https://gist.github.com/fommil/4ff3ad5b134280de5e46 (only works on Linux but should be adaptable to OS X)

Tmux
=======

Install
-----------

    brew install tmux

Command
-----------

    man tmux                        Commands Manual
    tmux list-keys                  lists out every bound key and the tmux command it runs
    tmux list-commands              lists out every tmux command and its arguments
    tmux show-options -g            show current global session options

#### Session
    tmux                                    create a session, default start with name 0
    tmux new -s <session name>              create a session with name
    tmux ls                                 list sessions
    tmux attach -t <session name>           reattach
    tmux kill-session -t <session name>     kill session
    
#### Server
    tmux kill-server                        kill server and clients, destroy all windows/sessions

Shortcuts
-----------

In tmux, hit the prefix ctrl+b (my modified prefix is ctrl+a) and then type key:

#### Pane
    |                   split vertical 
    _                   split horizontal
    
    arrows              jump between panes
    {                   move the current pane left
    }                   move the current pane right
    
    [ + finger swipe    scroll pages
    
    z                   toggle into full-screen
    Space               toggle pane layout (直橫切換)
    Ctrl + arrows       resize
    
    q                   show pane numbers
    d                   detach from session
    x                   kill pane

#### Window
    c                   add new Window
    &                   kill the current window
    
    <window number>     jump between windows

#### Session
    s                   show session list/ switch session
    $                   rename

#### Misc
    ?  list shortcuts
    :  prompt mode


Custom hotkeys
-----------

vim ~/.tmux.conf

    # set the prefix to ^a.
    unbind C-b
    set -g prefix ^a
    bind a send-prefix

    # Binding a key for “last-window”
    bind-key C-a last-window

    # pane splitting
    unbind % # Remove default binding since we’re replacing
    bind-key | split-window -h
    bind-key _ split-window

    # vi-style controls for copy mode
    setw -g mode-keys vi

    # Highlight active window
    set-window-option -g window-status-current-bg yellow

    # Automatically set window title
    setw -g automatic-rename

    # Set window notifications
    setw -g monitor-activity on
    set -g visual-activity on

    # Set status bar
    set -g status-bg cyan

    # Enable scroll pane under cursor on mouse up and enter copy mode
    set-option -g mouse on
    bind-key -T root WheelUpPane select-pane -t =\; copy-mode -e\; send-keys -M

    # https://github.com/tmux/tmux/issues/543
    set -g default-shell $SHELL 
    set -g default-command "reattach-to-user-namespace -l ${SHELL}"

    # Enable copying using Cmd+C in copy mode
    bind-key -t vi-copy MouseDragEnd1Pane copy-pipe "reattach-to-user-namespace pbcopy"

    # Increase scrollback buffer (default is 2000)
    set-option -g history-limit 60000


Just remember that after every modification, tmux must be refreshed to take new settings into account.
This can be achieved either by restarting it or by typing in:

    tmux source-file .tmux.conf


Reference
-----------

* [Tmux: A Simple Start](https://www.sitepoint.com/tmux-a-simple-start/)
* [The tao of tmux](http://tmuxp.readthedocs.io/en/latest/about_tmux.html#the-tao-of-tmux)
* Brief introduce && Custom hotkeys [PART 1](http://blog.hawkhost.com/2010/06/28/tmux-the-terminal-multiplexer/) / [PART 2](http://blog.hawkhost.com/2010/07/02/tmux-%e2%80%93-the-terminal-multiplexer-part-2/)
* https://wiki.frugalware.org/index.php/Tmux

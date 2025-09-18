# Set true color
set-option -sa terminal-overrides ",xterm*:Tc"

# Mouse interaction enabled
set -g mouse on

# Start windows and panes at 1, not 0
set -g base-index 1
set -g pane-base-index 1
set-window-option -g pane-base-index 1

# Set <prefix> key
unbind C-b
set -g prefix C-Space
bind C-Space send-prefix

set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'christoomey/vim-tmux-navigator'

#set -g @plugin 'fabioluciano/tmux-tokyo-night'

#set -g @plugin "janoamaral/tokyo-night-tmux"


#rose_pine tmux theme
#set -g @plugin 'rose-pine/tmux'
set -g @rose_pine_variant 'main'
set -g @rose_pine_host 'off'
set -f @rose_pine_battery_status
set -g @rose_pine_date_time '%Y-%m-%d %H:%M:%S'

run '~/.tmux/plugins/tpm/tpm'

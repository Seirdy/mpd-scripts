mpd-scripts
===========

A collection of useful MPD scripts, written in bashism-free POSIX shell.

`media-control`
---------------

`media-control` wraps [Playerctl](https://github.com/altdesktop/playerctl) and
[mpc](https://github.com/MusicPlayerDaemon/mpc). If MPD is running, this "translates"
Playerctl commands (`play-pause`, `previous`, `next`) to mpc commands; otherwise, it
forwards commands to Playerctl. This is useful for binding [XF86Audio\*
keys](http://wiki.linuxquestions.org/wiki/XF86_keyboard_symbols) to prioritize MPD
over other MPRIS players.

When forwarding commands to Playerctl, it adds `$HOME/.local/lib` to
`$LD_LIBRARY_PATH` and `$GI_TYPELIB_PATH` if Playerctl has been installed with prefix
`$HOME/.local`

`start-music` and `stop-music`
------------------------------

`start-music` starts MPD and mpDris2. `stop-music` stops these, as well as
[kunst](https://github.com/sdushantha/kunst),
[cava](https://github.com/karlstav/cava),
[ncmpcpp](https://github.com/arybczak/ncmpcpp),
[clerk](https://github.com/carnager/clerk),
[cantata-dynamic](https://github.com/CDrummond/cantata/blob/master/playlists/cantata-dynamic),
and [projectMSDL](https://github.com/projectM-visualizer/projectm).

MPD, mpDris2, and cantata-dynamic are managed by Systemd. Yes, I know, I know...

Smart playlists
---------------

Scripts in the "smart-playlists" directory utilize MPD's pseudo-standard "rating"
sticker, taking values from 1-10. Programs such as
[cantata](https://github.com/CDrummond/cantata), [gmpc](https://gmpclient.org/),
[ncmpy](https://github.com/cykerway/ncmpy), and
[clerk](https://github.com/carnager/clerk) use this sticker.

`mpd-playlist-above-rating` takes an integer argument from 0-10, and outputs a
playlist containing tracks above the given rating.

`mpd-playlist-unrated` outputs a list of tracks without a "rating" sticker. This is
useful for listening to music in your library you haven't heard yet.

`mpd-playlist-smart` generates a playlist skewed towards your favorite tracks,
intended to be played with shuffle. The playlist is built according to one rule: the
number of times a track appears is equal to its rating minus 5 (or 0, whichever is
greater). As a result, tracks must contain a rating of at least 6 to be added. Tracks
rated 6/10 appear once, while tracks rated 10/10 appear four times. The higher you
rate a track, the more likely it is to appear in this playlist. It requires
`mpd-playlist-above-rating`.

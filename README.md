# jukebox

`jukebox` is a small command-line music tool for `youtube-dl` that does a few useful things.

`jukebox` tries to adhere to the Unix philosophy. Please suggest improvements,
provided that they suit this philosophy.

## dependencies

- `bash`
- `jq`
- `youtube-dl`
- a Unix filter (default `fzf` but this can be configured)
- a music player (default `afplay` but this can be configured)

## example usage

Add a song to the default directory ~/jb/songs configurable through
`$JB_SONG_DIR`:

    $ cat 'https://youtube.com/...' | jb a

Select a song using the default filter fzf and play it using the default
player afplay:

    $ jb s1 | jb p

Use `vis -` as a Unix filter and select multiple songs to shuffle and play
(uses shuf from GNU coreutils):

    $ JB_MULTI_FILTER="vis -" jb s | shuf | jb p

## playlists

Playlists are just plaintext files that contain IDs. To make a playlist from a
filter selection:

    $ mkdir -p ~/jb/playlists
    $ jb s > ~/jb/playlists/classical-music

To play the playlist, pipe it into jukebox to play:

    $ cat ~/jb/playlists/classical-music | jb p

To play it shuffled, just shuffle the lines of input:

    $ cat ~/jb/playlists/classical-music | shuf | jb p

To skip a song, interrupt the process with ^C.

## todo

- [ ] remove all appearances of a song in playlists when the song is deleted from the library

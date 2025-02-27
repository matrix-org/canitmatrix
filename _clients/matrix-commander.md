---
title: matrix-commander
display_order: 10
categories:
 - client
description: Simple CLI-based Matrix client for sending and receiving with support for end-to-end encryption, emoji verification and much more
author: 8go
language: Python
license: GPL-3.0-or-later
# pick your license from https://spdx.org/licenses/
# valid categories are client, server, as (application service), sdk (client sdk), bot, and other
repo: https://github.com/8go/matrix-commander # your source code repository
room: None # "#my-first-matrix-projects-room:homeserver.tld" # nb the quotes are needed as rooms start with #
thumbnail: /docs/projects/images/matrix-commander.svg
screenshot:
# screenshot: /docs/projects/images/upload-a-bigger-image-for-your-project-page-to-the-images-subfolder.png
featured: true
platforms:
    - linux
    - macos
    - windows
client_type: terminal
features:
    Room directory: no
    Room tag showing: yes
    Room tag editing: no
    Search joined rooms: no
    Room user list: no
    Display Room Description: yes
    Edit Room Description: no
    Highlights: no
    Pushrules: no
    Send read markers: yes
    Display read markers: no
    Sending Invites: yes
    Accepting Invites: yes
    Typing Notification: no
    E2E: yes
    Replies: no
    Attachment uploading: yes
    Attachment downloading: yes
    Send stickers: no
    Send formatted messages (markdown): yes
    Rich Text Editor for formatted messages: no
    Display formatted messages: yes
    Redacting: no
    Multiple Matrix Accounts: yes
    New user registration: no
    voip: no
    Message editing: no
    Room upgrades: no
maturity: Released # Options are: Released, Stable, Late Beta, Beta, Early Beta, Late Alpha, Alpha, Early Alpha, or Not actively maintained
SDK: matrix-nio
---

# matrix-commander

Simple but convenient CLI-based Matrix client app for sending and receiving.

- `matrix-commander` is a simple command-line [Matrix](https://matrix.org/)
  client.
- It is a simple but convenient app to
    - send Matrix text messages as well as text, image, audio, video or
      other arbitrary files
    - listen to and receive Matrix messages
    - perform Matrix emoji verification
- It exclusively offers a command-line interface (CLI).
- Hence the word-play: matrix-command(lin)er
- There is no GUI and there are no windows (except for pop-up windows in
  OS notification)
- It uses the [matrix-nio](https://github.com/poljar/matrix-nio/) SDK
- Both `matrix-nio` and `matrix-commander` are written in Python 3

# Summary

This program is a simple but convenient app to send and receive Matrix
messages from the CLI in various different ways.

Use cases for this program could be
- a bot or part of a bot,
- to send alerts,
- combine it with cron to publish periodic data,
- send yourself daily/weekly reminders via a cron job
- send yourself a daily song from your music collection
- a trivial way to fire off some instant messages from the command line
- to automate sending via programs and scripts
- a "blogger" who frequently sends messages and images to the same
  room(s) could use it
- a person could write a diary or run a gratitutde journal by
  sending messages to her/his own room
- as educational material that showcases the use of the `matrix-nio` SDK

## End-to-end Encryption

End-to-end encryption (e2ee) is enabled by default. It cannot be turned off.
Wherever possible end-to-end encryption will be used.

## Sending

Messages to send can be provided
1) in the command line (-m or --message)
2) as input from the keyboard
3) through a pipe from stdin (|), i.e. piped in from another program.

For sending messages the program supports various text formats:
1) text: default
2) html:  HTML formatted text
3) markdown: MarkDown formatted text
4) code: used a block of fixed-sized font, ideal for ASCII art or
   tables, bash outputs, etc.
5) notification
6) split: splits messages into multiple units at given pattern

Photos and images that can be sent. That includes files like
.jpg, .gif, .png or .svg.

Arbitrary files like .txt, .pdf, .doc, audio files like .mp3
or video files like .mp4 can also be sent.

## Listening, Receiving

One can listen to one or multiple rooms. Received messages will be displayed
on the screen. If desired, optionally, you can be notified of incoming
messages through the operating system standard notification system, usually a
small pop-up window.

Messages can be received or listened to various ways:
1) Forever: the program runs forever, listens forever, and prints all
   messages as they arrive in real-time.
2) Once: the program prints all the messages that are waiting in the queue,
   i.e. all messages that have been sent in, and after printing them the
   program terminates.
3) Tail: prints the last N read or unread messages of one or multiple
   specified rooms and after printing them the program terminates.

## Verification

The program can accept verification request and verify other devices
via emojis. Do do so use the --verify option and the program will
await incoming verification request and act accordingly.

# Examples of calling `matrix-commander`

```
$ matrix-commander.py #  first run; this will configure everything
$ # this created a credentials.json file, and a store directory
$ # optionally, if you want you can move credentials to app config directory
$ mkdir $HOME/.config/matrix-commander # optional
$ mv -i credentials.json $HOME/.config/matrix-commander/
$ # optionally, if you want you can move store to the app share directory
$ mkdir $HOME/.local/share/matrix-commander # optional
$ mv -i store $HOME/.local/share/matrix-commander/
$ # Now you are ready to run program for a second time
$ # Let us verify the device/room to where we want to send messages
$ # The other device will issue a "verify by emoji" request
$ matrix-commander.py --verify
$ # Now program is both configured and verified, let us send the first message
$ matrix-commander.py -m "First message!"
$ matrix-commander.py --debug # turn debugging on
$ matrix-commander.py --help # print help
$ matrix-commander.py # this will ask user for message to send
$ matrix-commander.py --message "Hello World!" # sends provided message
$ echo "Hello World" | matrix-commander.py # pipe input msg into program
$ matrix-commander.py -m msg1 -m msg2 # sends 2 messages
$ matrix-commander.py -m msg1 msg2 msg3 # sends 3 messages
$ df -h | matrix-commander.py --code # formatting for code/tables
$ matrix-commander.py -m "<b>BOLD</b> and <i>ITALIC</i>" --html
$ matrix-commander.py -m "- bullet1" --markdown
$ # take input from an RSS feed and split large RSS entries into multiple
$ # Matrix messages wherever the pattern "\n\n\n" is found
$ rssfeed | matrix-commander.py --split "\n\n\n"
$ matrix-commander.py --credentials usr1room2.json # select credentials file
$ matrix-commander.py --store /var/storage/ # select store directory
$ # Send to a specific room
$ matrix-commander.py -m "hi" --room '!YourRoomId:example.org'
$ # some shells require the ! of the room id to be escaped with \
$ matrix-commander.py -m "hi" --room "\!YourRoomId:example.org"
$ # Send to multiple rooms
$ matrix-commander.py -m "hi" -r '!r1:example.org' '!r2:example.org'
$ # Send to multiple rooms, another way
$ matrix-commander.py -m "hi" -r '!r1:example.org' -r '!r2:example.org'
$ # send 2 images and 1 text
$ matrix-commander.py -i photo1.jpg photo2.img -m "Do you like my 2 photos?"
$ # send 1 image and no text
$ matrix-commander.py -i photo1.jpg -m ""
$ # send 1 audio and 1 text to 2 rooms
$ matrix-commander.py -a song.mp3 -m "Do you like this song?" \
    -r "!someroom1:example.com" "!someroom2:example.com"
$ # send a .pdf file and a video with a text
$ matrix-commander.py -f example.pdf video.mp4 -m "Here are the promised files"
$ # listen forever, get msgs in real-time and notify me via OS
$ matrix-commander.py --listen forever --os-notify
$ # listen forever, and show me also my own messages
$ matrix-commander.py --listen forever --listen-self
$ # listen once, get any new messages and quit
$ matrix-commander.py --listen once --listen-self
$ matrix-commander.py --listen once --listen-self | process-in-other-app
$ # listen to tail, get the last N messages and quit
$ matrix-commander.py --listen tail --tail 10 --listen-self
$ # listen to tail, another way of specifying it
$ matrix-commander.py --tail 10 --listen-self | process-in-other-app

```

# Interested?

- Go to the [matrix-commander repo](https://github.com/8go/matrix-commander/).

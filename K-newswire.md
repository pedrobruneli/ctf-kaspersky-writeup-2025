# K-newswire
**Category: WEB**

## Overview
We're given a website that shows to us a bunch of news in real-time and the goal is to find the secret news!

Unfortunately I do not have the website's code because it's down and i did not save, so I'll just tell what I did :(

## Dive into code

So first of all I need to know how this news is coming to us, and yes, is that what you are thinking, it's from an WebSocket made by Socket.IO.

The messages coming from that is all the news that appears in the frontend and the first message is a join to an "news" room, so ok, looks like we'll have to listen to something else to receive this "secret news".

Diving into the page source code I search to the join line and right next to it we also have another room called "secret_announcements", but wait, that's what we're looking for, easy right?

So all we have to do now is to make a script to emit a join to that room and listen to any events:

<img width="947" height="584" alt="image" src="https://github.com/user-attachments/assets/c5d0492d-019b-476c-83a1-856e478ad167" />

<img width="907" height="696" alt="image" src="https://github.com/user-attachments/assets/c243aaf3-ff89-4a51-a3ab-44c522e6b787" />

Obviously I have to call the k-newswire.task.sasc.tf socket, so that's why the link is there, and BINGO! We received the flag after that!

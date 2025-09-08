# Pythagoreus Temple
**Category: MISC**

## Overview
In this challenge we have an "web game" called pythagoreus temple, the first screen that we see:
<img width="1848" height="908" alt="image" src="https://github.com/user-attachments/assets/1b214dc7-3365-47be-a6e2-2c3eb0089a16" />

At first we see the message "your flag is inside, come and find it!. Bruh, you're an antic statue and can't move"
So all we need to do is to walk, right?
## Dive into the code
When we open the javascript of the page it looks like this:
<img width="1871" height="992" alt="image" src="https://github.com/user-attachments/assets/ffbc62de-64be-4526-a581-635060cc96ef" />

Pretty ugly, looks like it obfuscated, but don't worry, we can still debug this thing.

At some parts of the code we encounter this thing called "Babylon.js" and searching for this we find the library that made this game, so we making progress!

This time we want to search how the camera works because we want to walk and every game walking is just moving that camera.

Searching for "camera" in the babylon documentation we arrive at this section telling us that the Camera object has a position property, BINGO, now all I have to do is to find the camera object in the code, but wait...

<img width="714" height="309" alt="image" src="https://github.com/user-attachments/assets/573f64b5-41d9-4285-bae6-b6424e165f1d" />

We just need to check 400 thousand lines of obfuscated code... well... I guess that won't gonna work.

But one thing we notice also in docs, is that the camera must have a scene and the scene must have an engine attached to it, so searching for engine we can encounter this class of code:

<img width="671" height="284" alt="image" src="https://github.com/user-attachments/assets/fe8bbe61-e862-4109-acb6-d5de3c3feb37" />

An getScene, an after I debbuged it I found that this little monster `this[_0x420a95(_0x32e515._0x41e82d)]` carries the state of all cameras. So we found it! All we need to do now is to add an eventlistener that hears from user keyboard input and move the camera's position.

That getScene stuff is executed million of times so I just change the position a little to the character don't run out of the map and that's it, we can move now (with this horrible code).

<img width="1714" height="924" alt="image" src="https://github.com/user-attachments/assets/d3c62088-c44c-4e37-8c0c-2fb33880bbe8" />

Digging into the whole map we finnaly found the flag, inside the monkey's head... (it taked longer than I imagine...)

<img width="1331" height="875" alt="image" src="https://github.com/user-attachments/assets/64f84fdd-37b0-4404-9200-df0e4fc497bc" />

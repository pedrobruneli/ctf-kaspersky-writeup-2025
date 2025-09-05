# PhotoStock
**Category: WEB**

## Overview
We're given an url that leads us to a login and register page:

<img width="1905" height="888" alt="image" src="https://github.com/user-attachments/assets/edc1b060-2a70-4057-bb6e-43f94dc4e42d" />

Let's create an account to see what's inside:

<img width="1779" height="825" alt="image" src="https://github.com/user-attachments/assets/d709dcf5-6132-4ba3-be16-e245cee22fba" />

Okay, looks like we have to retrieve this blurried image and the flag will be inside that.

Also we have all the frontend and backend application code!

## Dive into code
First of all, what we wanna do is to unblur this image or enter in the administrator account!

Let's try the simpler one because cracking authentication isn't that easy, right? So let's check this code out and find how they blur the image.

So searching for anything in the code we find this function:

<img width="877" height="558" alt="image" src="https://github.com/user-attachments/assets/466126b4-9a04-47f2-82b6-6c16f90ae3de" />

Looks like they blur this in the backend (as imagined) and to check this they verify if the user is the image's owner or the image is public

<img width="605" height="199" alt="image" src="https://github.com/user-attachments/assets/d8c9c3f9-db65-4bf5-8255-521d2e16e3a6" />

So ok, guess we want either to change the note from adm account to ours or change the privacy to public. So let's try to check whatever the note's info changes.

Checking for the update controller we find that they check if the note's owner id is the actual user id retrieved from the JWT token, so let's keep searching for some other endpoints

<img width="802" height="349" alt="image" src="https://github.com/user-attachments/assets/c05a7845-92c9-43db-8200-2db8e0ce3210" />

Looking further I found these endpoint that changes the note visibility to public or private, ok that's interesting

<img width="1278" height="593" alt="image" src="https://github.com/user-attachments/assets/32129c60-a534-461f-9f46-dae1559881d0" />

One thing grabbed my attention, the endpoint receives either an array or the note id as a parameter, so the user can change the notes visibility all in one endpoint or if they wanna change a single note they can. But look at how the endpoint checks this, they do an if in this _json param and check if it's an array, if it's an array they iterate and check each note if the note owner's is the same as the user_id provided by the JWT. But if the _json object isn't an array they just check the id param passed by the endpoint:

<img width="954" height="380" alt="image" src="https://github.com/user-attachments/assets/ec02b991-c16c-430b-88ba-c7ec5a8180a6" />

Can you see any problem with this checking? Really? Check again before continue to the answer!

...

Ok so, I don't know a thing about ruby on rails (the backend language) but if they check the note's owner by that first if statement so what happens if I give an empty array called _json: [] and then give another field id with the actual administrator notes_id? Because they just check the owners if the _json field is not an array, so when I gave to them an empty array there's nothing to iterate so that's nothing to check and then this if statement ends without forbidden errors, and then they'll check if the id field exists and update this note_id without checking the note's owner!!

So let's try it out. First we need to get the adm note's id, that's easy, just get the get all notes endpoint and then pick the note_id from the response as shown bellow:

<img width="1899" height="899" alt="image" src="https://github.com/user-attachments/assets/b13e2699-67f6-4218-9baf-45d56af6d2dd" />

Perfect, so let's build the request we spoke before in postman. We do a patch request to the change privacy endpoint, put it to public and then pass the _json and id parameters:

<img width="902" height="705" alt="image" src="https://github.com/user-attachments/assets/fabc9641-7af5-4f34-97ff-5d7591a006c8" />

And BINGO! they returned 200 OK! So let's check if it worked

<img width="1854" height="762" alt="image" src="https://github.com/user-attachments/assets/ff20c35c-3903-4a57-83e9-6841910c9c38" />

There is! We got it! Of course this is only the test server, the real server is down when I wrote this thing, but all you have to know is that worked xD

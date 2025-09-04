<img width="1040" height="312" alt="image" src="https://github.com/user-attachments/assets/7189ac6a-ddb5-4e3f-a5a0-079f93ff91d9" /># OSecret
**Category: MISC**

## Overview
We're given an .zip file that was a backup made from areca backup, but there's a problem, this backup has one of the backup parts, and this file is encrypted with an password (the password was given in the challenge).

## Dive into
So first of all we need to know what's that areca backup, so searching for that is an backup tool (WOW!!!!), but how we recover this thing? Ok, we simply search for that in the docs.

Okay, we actually found our scenario, worst recovery case :), so all we have to do is to run this decrypt and run this unzip and EUREKA?!

<img width="1688" height="468" alt="image" src="https://github.com/user-attachments/assets/fd87d41e-a4a0-42d1-9680-bc4314b69cab" />

Obviously not, we get this error when trying to decrypt with both encrypt methods that shows to us in console

<img width="875" height="228" alt="image" src="https://github.com/user-attachments/assets/07b436b1-d80f-47dc-8219-81562e638d18" />

<img width="1047" height="566" alt="image" src="https://github.com/user-attachments/assets/18428774-75bb-4e3b-bda4-4d5f6350410d" />

Ok, so I guess we have to decompile this code to see what's going on.

Checking inside the code and inside the class that does the decrypt we see the class EncryptionPolicy:

<img width="1040" height="312" alt="image" src="https://github.com/user-attachments/assets/14765ea6-7537-4c46-b711-6a18ee94e3b5" />

Inside that EncryptionPolicy class we se that EncryptionConfiguration class also that chooses the method to decrypt the file:

<img width="1084" height="180" alt="image" src="https://github.com/user-attachments/assets/0435fc81-98dc-4140-962e-76d2cac7f7dc" />

And finnaly we arrive in that EncryptionPolicy class that has more than those algorithms showed before. So let's brute force until it works, and when we put the AES256_HASH_CBC algo we did it!!!

<img width="678" height="576" alt="image" src="https://github.com/user-attachments/assets/711c820e-395f-4a04-8ece-73106b7fcc69" />

BINGO, just unzip and got the flag as image (i do not have the print of the flag but trust me, it worked xD)

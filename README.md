# PasteSend
This is a script to automatically upload to/download from PasteBin without using their developer API. The developer API is nice; however, it requires registering for a key which is associated with your uploads, which you may or may not want. Alternatively, if you're interested in using the compress/encryption/base64 piece, the script allows you to either output to screen for easy copying or into a file.

# Interest
I was interested in creating this script because I've had times while conducting malware analysis where I wanted to get the data I'd collected or generated out of my VM safely. I was often relatively certain that I either hadn't activated the malware or had neutered it, but out of an abondance of caution I didn't want to use my credentials on any sites. Pastebin is a good option for this, but then your notes and research are exposed for the timeframe that the data is on the site.

# Three Main Ideas
1) Automate - Humans are stupid, and so is user input. The script tries to minimize problems by automating interacting with the Pastebin UI for both send and get functions, and for the various wrapping steps.
2) Safety/Privacy - Although I've never used Pasetebin to transfer anything sensitive, I still don't want other people to access what I upload. The data that you're transfering is zipped for size, AES encrypted for security (there is a default garbage key/iv, but you can either enter your own or use -random to generate using random.getbytes), and base64 encoded to paste safely. The script additionally enables Burn After Read mode in Pastebin, which theoretically destroys the data after read and doesn't list the upload in the public area.
3) Verification - Understanding why and how something might have gone wrong is important. The script outputs hashes at three points during the send and get functions to allow the user to verify the data: an MD5 of the raw data read from disk; an MD5 of the zipped data; and n MD5 of the base64 data.

# Future Direction
1) Change interaction framework - I initially attempted to use mechanicalsoup which has a really nice and easy way to inteact with website elements, and maintains website state. I ran into issues actually submitting the form and could only recieve 400's from Pastebin. I switched to using selenium which mostly works but relies on the ability to spawn a web browser and interact with the UI. This works mostly fine in a manual environment (where I just want to transfer notes), but doesn't work fine if you were to want to use this script via a service. Alternatively, it would obviously be possible to manually handle the cookies and form interactions.
2) Expand intermediary service options - Pastebin isn't the only site where a user can enter relatively arbitrary information. It should be possible to identify other sites where a user can upload and delete arbitrary data (blog comments, amazon reviews, etc).
3) Test on other platforms - I only tested on linux (specifically a Kali VM). The only problematic feature is selenium itself, which theoretically plays nice with other operating systems but again I didn't test that.

# Resources
* Video overview: https://youtu.be/40Tnvr04-jE
* Selenium's documentation - https://www.selenium.dev/
* Pastebin's API which we aren't using - https://pastebin.com/doc_api
* Pastebin's FAQ which lays out how you might get blacklisted/deleted by using this script - https://pastebin.com/faq
* MechanicalSoup documentation that was almost used - https://mechanicalsoup.readthedocs.io/en/stable/index.html

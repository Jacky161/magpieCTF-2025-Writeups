# The Notebook's Secret - Category: Web

>Another late night at the precinct, another piece of evidence to sift through. This time, it's Professor Richard Hash's research notebook. Your partner, Edward Cors, leans back in his chair. "I don't know, this feels like it's pointing straight at Hash. The guy's always preaching about transparency, about making everything public. Maybe he decided to take matters into his own hands." But something about the notebook catches your eye. The last entry, dated February 21st, 1933, one day before Krypto's murder, hints at an unexpected development. It seems Krypto and Hash were on the verge of announcing something big.
>
>SSH Port is 2222.

What I find already interesting is we're given an SSH port. Let's keep that in the back of our minds for now. Browsing to the link given reveals a Jupyter Notebook instance with a single notebook.ipynb. Inside this file lies some notes, presumably from Richard Hash, and some Python functions.

![Interesting Functions](img/JupyterNotebook_functions.png)
![Hash's Notes](img/JupyterNotebook_Hash_Notes.png)

Reading the notes, it seems like trying to get ahold of these "access credentials" could be a good idea. The find_research_files function seems to already be setup to look for backup files so perhaps it could help us here.

The question is, can we actually execute Python code? Adding a new cell, we can see that this is indeed the case. Let's try running the functions as given in the example usage.

![find_research_files function output](img/JupyterNotebook_find_research_files.png)

Seems like we do have some backup files! We can list the files in that folder to see a suspicious looking ".keys" folder. Inside this folder is supposed to lie an SSH private key which belongs to ckrypto's user. I would show you but seems like someone deleted it so I can't grab an image of it to show here. 

![Directory listing of the empty backup folder](img/JupyterNotebook_sabotaged.png)

Actually, if you want the true story, this folder was also completely empty when I first attempted the challenge. What I actually did back then was to inject my own SSH key into rhash's .ssh folder and SSHed in that way. I used this python snippet to do just that. 

![Injecting my own SSH key](img/JupyterNotebook_injectSSH.png)

After getting in and poking around for a while, I eventually found ckrypto's SSH key within that .keys folder which I assume is when the challenge was fixed. Since I was SSHed in, I was easily able to read the contents of the file and get the private key. The expected way to do this I would assume would be to use Python to print out the contents of the private key file within the .keys folder.

After getting the key one way or another, we can simply SSH into the machine, logging in as ckrypto, and using the private key we obtained.

```ssh ckrypto@challenges.magpiectf.ca -p 2222 -i <path to private key>```

After snooping around in ckrypto's home directory, we can find a suspicious looking `.private` directory, and within it, the flag!

![Directory listing of ckrypto's home directory and catting out the flag](img/ssh_ckrypto.png)

**Flag**: magpieCTF{cryp70\_k3y\_4cc3ss\_gr4nt3d}

#### SSH Start of ReadMe.md file...

# SSH Implementation 

I will
dDemonstrate how I implemented ssh security in my workflow. 

+ Briefly explain how to genarate a ssh key pair.
+ Talk about my config file for ssh keys on what servers.
+ sftp connecting securely,, and overview of commands. No password needed.
+ git config command and the resulting file .gitconfig . Briefly explained
+ GitHub repository created via browser and project folder coverted to git folder and pushed to new GitHub.
 
resource links and Media Webinars can be found [here](#user-content-mywebinars ) are provided at the bottom of this ReadMe file..

A video and audio webinar of this repository and a more in depth tutorial is available at:

http://blindheroes.org


    >You can quickly clone this GitHub repository by copy address in adressbar into clipboard. Paste it into the following command:

    `` $ git clone https://github.com/lewislwood/ssh-sftp-git-blind ``

Then if you want to follow along this tutorial, simply delete the hidden folder .git crated and the folder is no longer a git repository.

    ` $ sudo rm -r .git`


## SSH Key Generation

I will generate a key using the command below:

    `    > $ ssh-keygen -t ed25519 -C "lewislwood@gmail.com"  `

I will press enter on default location and change defaWhen prompted for filename and location I will enter "id_lewis-i9" which is the name of my computer that I gave it. The name can be anything.
 Now you will be prompted for a pass phrase. This is my desktop computer and I currently have no high secure items. Thus I opt for blank. On my laptop I will use one. Since it may be stolen someday.

 Two files will be created one with a .pub extension.
You could of used the default and it would have created default files in the default directory.
  default folder is     >/.ssh .  Now the     >/.ssh is the same as /home/lwood/.ssh since my username is lwood.
Now some hosts require I only have access to these files, thus I should apply 0700 rights to those files with the following:

    ` $  chmod 0700 /home/lwood/.ssh/* `

See the following link for additional information:

[github using ssh](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)

## Configuring Hosts to use SSH

Now we will need to create a config file and plae it in the     >/.ssh folder.   have included a sample one and placed it along with identity files for your reference.

 Structure of the file is Host reference name.  This is the name we will use to trigger the entry below: All items are indented that apply to that host reference name. 
You will see I use blindheroes.org as a reference name. The underlying  server name is actually ftp.jxxxxfei.me some ridiculous name. I specify username, identity file to use, and if I want it to ask for password.
  This makes my sftp and git to github easy and simple.
Here is a good quick reference I used:

[10 great host examples](https://gist.github.com/vrillusions/9538779)

### SFTP - Secure FTP Protocol

 Linux comes with Ftp and SFtp preinstalled, so why not use it. It supports scripting, and all the standard commands that other popular Ftp programs do. SFtp is so easy, especially if you already know command line linux commands.
 Because of the configuration for SSH we did in the previous section, it is really simple to connecct. 

 Just make sure you already uploaded the SSH id*.pub file to the site first. I used control Panel and then Authorized it. Only the "*.pub" version, the other is locally only. The 2 files will be compared at connection time to verify connection.
I do the following to connect:

    ` $ sftp blindheroes.org `

Once connected I can issue most standard linux commands. Those commands now work on the remote server. Prefix them with an l for local to do them local.
Example: pwd - present working directory on server.  lpwd  present working directory on local computer.
 cd - change directory on server.  lcd - change directory locally.

See following for a list of commonly used commands.

[10 SFTP commands](https://www.tecmint.com/sftp-command-examples/)

## Initial git configuration

This is done when you first start using git. You will want to set up a user name, email, editor, and handle crlf for windows vs mac systems.
Replace my name and email address of course and your editor of choice.
    ` $ git config --global user.name "Lewis Wood" `

    ` git config --global user.email lewislwood@gmail.com `

    ` $ git config --global core.editor notepad.exe`

    ` git config --global core.autocrlf true `

Use your favorite editor. If you use vscode the command is "code --wait". This tells git to wait for vscode to exit. You must use ""'s for values that have spaces in them. Autocrlf should be true for windows systems.

Now you can pull up the .gitconfig file with the following command and review your settings.

    ` $ git config --global -e `

## Create Local git repository

Now we will add a local git repository to the project folder. It will show up as a hidden folder named .git.

    ` $ git init   `

  Now enter the below command in order to add files in current folder and all subfolders. Excluding files in the .gitignore file.

    ` $ git add .   `
   Now create your first commit with a message. I use "my first commit"  

    ` $ git commit -m "my first commit" `

Now we need to add the GitHub repository to this local repo.  Notice "git remote" does not list any remote repositories.

[git reference](https://git-scm.com/docs)

## GitHub add SSH Key

In order to add an ssh key you will need to locate profile settings and ssh keys on it. For screen readers do the following:
+ Pres ctrl plus Home to go to top of page.
+Press letter "b" as in button twice for profile menu dropdown. Click to dropdown menu.
+ select Settings.
+ Do a ctrl plus "F" for find .  Search for "ssh"  
+ Click on the link ssh, it should be under password settings lik
+ This link should refresh and place you in the SSH key listing or say none if you have none.
+ Tab or cursor down to get to the add ssh key button or link.
+ On add ssh key screen/diaglogue enter title for the ssh key ( usually the device name you are setting it for).
+ Now locate your identity file *.pub file you want to use. Open in notepad or any test editor.
+ Select all and unselect any space characters at the end of the selection. I do "Home", then "Shift plus End", while holding shift key I unselct last cahracter until I hear a real character.  Now copy it.
+ Now return to the add ssh key page you have open and paste the key from the clipboard. Then press done button.
You should now see your ssh key in the list of available ssh keys. Congrats you are ready for secure git push and fetches.


## Create GitHub repository

We will create a GitHub repository. GitHub 
Enter title, but uncheck auto crate ReadMe.md and License.txt files. These files will complicate our later steps when we push them from our local repository.
now we need to copy the ssh link.  I find that by doing the following:
+  "R" for region or "D": for landmarks if using NVDA (I use Jaws so "R" is used"
+ "R" until I hear Repository region. 
+ Press letter "b" for button about 4 times until I hear button menu.
+ Activate the menu and make sure the ssh tab is selected. 
+ Now press "b" you should hear "copy buton" this will copy the link to the clipboard.

 Now return to project folder with local repository.
    ` $ git remote add origin <paste link here from github>`

     `  $ git remote  `

Your github link shoudl now appear as a remote for this local repository.
Now you will push and set the origin as the upstream  repo.

    ` $ git push --set-upstream origin master`
From now on all you have to say is 
    ` $ git push`
Origin will be assumed...

That is it.

<h4 id="mywebinars">Resources and Media Webinars</h4>

There are two YouTube video webinars available  @ the website article.

http://blindheroes.org

Each video is broken down into chapters. Screen reader users can quickly navigate YouTube Chapters with the Links List via f7. Once  the list is up, just press the number 0 to locate the 1st Chapter 00:00.  You can then just cursor down the list and choose the chapter you want to see.
Best way to find out about command line git commands is google. The command line manual is too complicated and cannot be navigated easily. with screen readers.
 Just type in google any of the following:
+ git remote
+ git Push
+ get fetch
git merge

[git branch workflow](https://git-scm.com/book/en/v2/Git-Branching-Branching-Workflows)
[github using ssh](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
[10 great host examples](https://gist.github.com/vrillusions/9538779)
[10 SFTP commands](https://www.tecmint.com/sftp-command-examples/)
[git reference](https://git-scm.com/docs)


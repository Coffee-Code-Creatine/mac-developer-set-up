# Introduction
Before we can begin our journey writing software we first need to build out a developer environment on our local machine. Generally speaking, I hold the opinion that Apple machines are easier to code on than just about any other operating system. To me, windows feels clunky, and linux distributions require a little more effort to get off the ground then most. Keep in mind I am not saying these other operating systems cannot be programmed on, nor am I saying that you should not program on them. I am just simply stating my preference.

That being said, as you might imagine I typically develop on a Mac. Here recently I updated my older machine to a new one and with it adopted an Apple Silicon chip. Now, the Apple Silicon chips are not adopted by everything just yet, and some things are a little tricky to set up. This blog post will not only walk you though what I use for local development, but how to set everything up and get it to play nice.

# The Goal
First things first, what are we going to do? We are going to take a brand new mac, with a fresh install of Mac OS and set it up for Java, Python, and Javascript development. A high level order of installation will go something like this.

- XCode
- Homebrew
- Zsh, Oh My Zsh & Iterm2
- Python and PyEnv
- Java, JEnv, and Maven
- Node and nvm
- Ngrok
- Github
- Intellij IDEA
- Pycharm
- VS Code


With these 10 or so things installed you will have a solid development environment set up, and have the IDEs needed to start writing code.

# Your Path
Your path is a system level variable that holds a list of directories. Great, what does that mean? When you run a command in your terminal, you typically use a form of shorthand, or a command name. For example, when you invoke maven with something like “mvn”. Your computer will understand “mvn” really means the maven script, and that script lives at some location on your machine. By adding that location to your path, your machine will pick up that command, and now understand what “mvn” means and where it lives. As we go through this document, we are going to be making a few changes to your path. In the event we mess something up, it is a good idea to have a backup of the original path. Getting that “backup” will be step one. First, open your terminal, this is where we will run commands. Second, open up text edit, this is where we will save the output. Once you have those two programs open, go ahead and run the following in the terminal.

```bash
echo $PATH
```

The output should look something like this.

```bash
/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin
```

Copy that output and save it in your text document.

# Xcode
XCode is a great IDE for writing native iOS apps, but as long as we are being honest, it isn't good for much else. So why are we downloading it? XCode is going to pull down quite a bit of build tools that we will need in order to run commands later down the line. Further to that point, the first time you open it, you will be asked to download CLI tools, and we are going to need those too. So for this step, we are going to open the App Store, and search for and install XCode. Now, XCode is a 12gb application, it is going to take some time to download and install. Be patient. Once you have it downloaded and installed, launch the application. A window should pop up asking to download command line tools. Click yes, and let this install.

# Homebrew:
As Apple machines don’t come with a package manager, we are going to need to install one. For us, this is going to be homebrew. What is a package manager you ask? Think of it as almost like a command line version of the app store, but rather than installing apps, it installs packages and build tools. In order to install it, run the following commands in your terminal. As a note, this install will ask for your password, this is ok.

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

This command is going to install homebrew, more than likely at the end there is going to be a caveats section telling you to run two commands. The first one will look something like this.

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/jacobdaigle/.zprofile
```

This command is going to place an eval script on your zprofile. This to say, when you launch your terminal, a script will be run to get home brew up and running. It should be noted that the second half of the script I have listed has “jacobdaigle”. This is my username, you will need to replace this with your own. Alternatively, it should be listed in that caveats section I mentioned, you should be able to copy it from there. The second command listed will look something like this

```bash
eval "$(/opt/homebrew/bin/brew shellenv)"
```

The first command in the caveats sesion put homebrew on our profile, and your profile will be ran each time we open terminal. However as our terminal was already open, we do need to run the same eval script for our current session. This is exactly what the second common does. After this command is executed, your path will be a little different. If you go ahead and run the echo command.

```bash
echo $PATH
```

Your path should now look something like this.

```bash
/opt/homebrew/bin:/opt/homebrew/sbin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin
```

Notice homebrew is now on your path.

# Zsh, Oh My Zsh and Iterm2
Long ago, Macs came installed with bash as the default shell. In this case, “shell” just means how the terminal runs commands. With the introduction of Catalina, we got zsh by default, however I never got out of the habit of installing zsh via homebrew, and then using Oh My Zsh on top to give me a few additional tools, as well as some aesthetic changes. This section will have some functional set up, and some aesthetic set up. The aesthetics are not needed, but they will make things easier. As we go though, I will call out the aesthetic bits. For now, let's get started with the functional. First up, installing zsh via homebrew by running the following script from your terminal.

```bash
brew install zsh
```

After zsh, comes Oh My Zsh, this can be installed by running the following script from your terminal.

```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Now, at this point we are going to have zsh and oh my zsh installed. We have completed the functional part of this set up. However, we can make things look and operate much nicer. So let's go ahead and do that. The first thing we are going to need to do is install iTerm2. This can be downloaded [here](https://iterm2.com/). All you have to do is download the app, and then open the file. Your mac will ask you if you want to open the application, go ahead and click yes, and you should be good to go. You now have iTerm2. At this point, I would suggest closing Terminal and running commands from iTerm2. It should be noted that from this point forward I will refer to iTerm2 simply as “the terminal”.

Next on the list of aesthetic changes is going to be changing the theme of Oh My Zsh. This can be done by changing the theme in “.zshrc” file. To open the “.zshrc” file from the terminal, run the following command.

```bash
vi ~/.zshrc
```

This will open the file from the terminal using vi, we will then need to scroll down until we find a line that reads.

```bash
ZSH_THEME="robbyrussell"
```

Go ahead and change that line to read.

```bash
ZSH_THEME="agnoster"
```

If you are unfamiliar with vi, you will need to press “i” to enter insert mode. You can then make your changes. Then you will need to press “esc” to exit insert mode, and then press “:wq”. This will save and close the file. From here you can restart the terminal, and the new theme will take effect.

Next on the list of aesthetic changes is going to be fonts. If you have done a little exploring in iTerm2 you may have noticed some of the characters are not displayed properly. Let's fix that, first we are going to need to install a few fonts. To do this, we need to download a collection from git, this can be done by running the following command from the terminal.

```bash
git clone https://github.com/powerline/fonts.git
```

From here we need to go into the font directory, and run the install script. This can be done by running the following two commands.

```bash
cd fonts
```

This will change the directory to be inside the fonts collection.

```bash
./install
```

This will install the fonts. Once the fonts are installed, we can delete the collection. We do this by going up one directory, and deleting the folder. We can do this by running the following command first.

```bash
cd ..
```

Once we are up one directory, we can run the following command to remove the font directory.

```bash
rm -rf fonts
```

From here, we will need to select one of the new fonts inside of iTerm2. We can do this by opening the preferences inside of iterm, command + , is a shortcut to open the preferences tab. Then we go to profile, and then text. I typically use “Meslo LG S for Powerline” as my font of choice.

Up next on the aesthetic list is colors. The base color scheme of iterm is nice, but the black on blue can be a bit tough to read. You can use a different default color scheme such as “Tango Dark” which solves this problem, but who does not like options? First we need to clone another collection from github, this one for colors. Go ahead and run the following command.

```bash
git clone https://github.com/mbadolato/iTerm2-Color-Schemes.git
```

Once you have the repo cloned, you can open the preferences of iTerm2, go to profiles and then colors. When you click the dropdown, you can select “import” and then select a color scheme of choice to import. The correct files for iTerm2 will be found at the following directory.

```bash
iterm2-Color-Schemes/schemes
```

It should be noted that we are not removing this collection, as we need it to be around for iTerm to use it. That said, you can move it to another location and reimport the color scheme if you so wish.

# Python and PyEnv
For python development we really don’t want to use our system version. In the event we mess something up in terms of builds, packages, or dependencies, it can be quite painful to get everything cleaned back up. To prevent this sort of pain we are going to use virtual environments. Think of them as little local installs of python for a project. In the event we mess something up, we can remove the virtual environment and create a new one. No fuss, no muss, no cuss. In addition to this safety, it also allows us to have multiple different versions if python installed on our machine. For this, I typically use pyenv. Pyenv can be installed via homebrew in our terminal. So go ahead and run the following command.

```bash
brew install pyenv
```

Once you have pyenv installed you will again get a caveats sesion with a few lines listed. These will need to be added to our zprofile. As we won’t be running these commands, just adding them to the profile, once we edit the profile we will need to “source” the profile, which really just resets the terminal. So let's knock that out. First we need to open the zprofile. We can do this from the terminal by running the following.

```bash
vi ~/.zprofile
```

From here we will need to add the following lines at the bottom. Keep in mind this is vi so we will need to go to the bottom, press “i” for insert mode, add the lines, then hit esc, and type “:wq” to save the file. The lines we want to add are as follows.

```bash
#Pyenv Set Up
export PYENV_ROOT=$HOME/.pyenv
eval "$(pyenv init -)"
```

The first line is just a comment to explain what we are doing. It effectively does nothing. The second like creates a variable for PYENV_ROOT, which is used by pyenv. The third line initializes pyenv. Once you have the changes added and saved, we need to source the profile. This can be done by running the following command from the terminal.

```bash
source ~/.zprofile
```

Now we should have pyenv installed and ready to go. At this point, we will also have shims added to our path. If you run the path command again.

```bash
echo $PATH
```

You should see something like this.

```bash
/Users/jacobdaigle/.pyenv/shims:/opt/homebrew/bin:/opt/homebrew/sbin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin
```

Note, you should see .pyenv/shims at the front of the path. This needs to be before your local bin. This way we get pyenv python before our system python. Once we have pyenv installed, we are going to want to install a version of python. At this point, we are going to go with the latest, which is 3.10.4. In order to install python we need to run the following command from the terminal.

```bash
pyenv install 3.10.4
```

Once this command terminates, we need to set this version of python to be our global version. This can be done by running the following command.

```bash
pyenv global 3.10.4
```

That is all there is to it, now you have pyenv installed and a version of python. By way of a sanity check if you run the following command.

```bash
python --version
```

You should get back 3.10.4 indicating you have a global version of python set. Then, for development, we can either use this version to make virtual environments, or we can install other versions of python and use that. Don’t worry, there will be another blog post on how to get started with python development.

# Java, Jenv and Maven
Java is going to be similar to installing python, in that we are going to be using a tool to manage different versions, much like pyenv, this will be called jenv. This will be installed via homebrew, on the terminal.

```bash
brew install jenv
```

Once homebrew installs jenv you will again see a caveats sesion with a few lines to put in your zprofile. Just like with pyenv, we will add these to the zprofile and then source the profile. First we need to open the zprofile with the following command.

```bash
vi ~/.zprofile
```

Then add the following lines. The first line is a comment explaining what we are doing. The second line adds pyenv to your path, and the third line will initialize jenv. Again, we are using vi, so once you open the file, press “i” to enter insert mode. Add these lines to the bottom, then press esc and type “:wq” to close vi.

```bash
#Jenv Set Up
export PATH="$HOME/.jenv/bin:$PATH"
eval "$(jenv init -)"
```

From here, all we have to do is source the zprofile with the following commands.

```bash
source ~/.zprofile
```

At this point, your path again will be updated. If you print your path again, by running the following.

```bash
echo $PATH
```

You should see something like this.

```bash
/Users/jacobdaigle/.jenv/shims:/Users/jacobdaigle/.pyenv/shims:/opt/homebrew/bin:/opt/homebrew/sbin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin
```

Notice jenv at the front. Now that we have jenv, we are going to want to enable the export and the maven plugins for jenv. To enable export, run the following command in your terminal.

```bash
jenv enable-plugin export
```

To enable the maven plugin run the following command in your terminal.

```bash
jenv enable-plugin maven
```

Now we are going to want to install a few different versions of java. We are going to go ahead and install the most popular. The commands you will want to run are as follows.

```bash
brew install java
brew install AdoptOpenJDK/openjdk/adoptopenjdk{11,14}
brew install AdoptOpenJDK/openjdk/adoptopenjdk8
brew install openjdk@17
```

This will install java as a whole, AdoptOpenJDK 8, 11, and 14, as well as java 17. Once we have the versions installed, we need to add them to jenv. This can be done with the following commands.

```bash
jenv add /Library/Java/JavaVirtualMachines/adoptopenjdk-14.jdk/Contents/Home
jenv add /Library/Java/JavaVirtualMachines/adoptopenjdk-11.jdk/Contents/Home
jenv add /Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk/Contents/Home
jenv add /opt/homebrew/opt/openjdk@17/libexec/openjdk.jdk/Contents/Home/
```

This will add 8, 11, 14, and 17 to jenv. The global version of java can then be set by running the following. This will set the java version to 14.0.

```bash
jenv global 14.0
```

We can test the java version by running the following.

```bash
java --version
```

We should get 14.0 back. Now that we have java set up, we are going to want to get maven set up as well. First step is to download maven from the website [here](https://maven.apache.org/install.html).

Once you have the maven directory downloaded, you are going to want to unzip it and place it in your macs /opt directory. The easiest way to do this is to open finder and press command + shift + G. This will bring up a “go to” window, here you will want to type /opt and then press enter. This will take you to the proper directory, and you can then drop and drop the maven files in.

Once you have moved the maven files, you will need to add the following lines to your zprofile. It should be noted, this line does contain the version of maven. For my example I have 3.8.5, if you downloaded a different version of maven, you will need to change the version as appropriate.

```bash
#Mvn set up
export PATH=/opt/apache-maven-3.8.5/bin:$PATH
```

Again, we can open the zprofile with the following command.

```bash
vi ~/.zprofile
```

Add the lines above by going to the bottom of the file, pressing “i” to enter insert mode, add in the lines, then press esc followed by “:wq”. Once the file is saved, source the zprofile by running the following command.

```bash
source ~/.zprofile
```

At this point, your path will have once again changed. If we print it with the following command.

```bash
echo $PATH
```

You will get something like this.

```bash
/opt/apache-maven-3.8.5/bin:/Users/jacobdaigle/.jenv/shims:/Users/jacobdaigle/.pyenv/shims:/opt/homebrew/bin:/opt/homebrew/sbin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin
```

Notice “mvn” now at the front.
That is it, you now have jenv, a few versions of java, and maven.

# Node and nvm
With python and java out of the way, the only other language specific is javascript. On the plus side, java script is pretty straightforward. Most folks who use javascript use node, and much like python and java there are many versions of it. To manage these versions we are going to use nvm or Node Version Manager. We can install nvm via homebrew by running the following command in the terminal.

```bash
brew install nvm
```

An extra bit we do have to do is create a directory at the root of the system to house the nvm goodies. This can be done by running the following command on the terminal.

```bash
mkdir ~/.nvm
```

Once you have nvm installed you are going to need to add a few things to your zprofile. The lines to add are as follows.

```bash
#NVM Set Up
export NVM_DIR="$HOME/.nvm"
[ -s "/opt/homebrew/opt/nvm/nvm.sh" ] && \. "/opt/homebrew/opt/nvm/nvm.sh"  # This loads nvm
[ -s "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm" ] && \. "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm"  # This loads nvm bash_completion
```

Again, we can open the zprofile with the following command.

```bash
vi ~/.zprofile
```

Add the lines above by going to the bottom of the file, pressing “i” to enter insert mode, add in the lines, then press esc followed by “:wq”. Once the file is saved, source the zprofile by running the following command.

```bash
source ~/.zprofile
```

At this point, your path will have once again changed. If we print it with the following command.

```bash
echo $PATH
```

You will get something like this.

```bash
/Users/jacobdaigle/.nvm/versions/node/v18.3.0/bin:/opt/apache-maven-3.8.5/bin:/Users/jacobdaigle/.jenv/shims:/Users/jacobdaigle/.pyenv/shims:/opt/homebrew/bin:/opt/homebrew/sbin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin
```

Notice “nvm” now at the front. At this point we should be able to install node by running the following from the terminal.

```bash
nvm install node
```

We can also install react by running the following.

```bash
npm install react --save
```

At this point, we have nvm to manage node versions, javascript by extension, and we even have react installed in the event we want to play with it.

# Ngrok
Ngrok is a dev tool and is quite nice to have. If you ever build anything that pushes events to a web server, slackbots are a great example of this, you will need something like ngrok. It is the piece of magic that will expose your local server to the internet so that various things can call it. This can be installed by homebrew with a single command via the terminal

```bash
brew install ngrok
```

That’s it, not path edits. Just homebrew.

# Github
Most likely, if you are writing code you are using some version of source control. If you are using git, or want to use git, you are going to need to add an ssh key to git. It should be noted, if you dont have a git account, now would be the time to make one ([github](https://github.com/)).  In order to generate one on your local machine, run the following two commands

```bash
ssh-keygen -t ed25519 -C "YOUR EMAIL"
pbcopy < ~/.ssh/id_ed25519.pub
```

The first command generates a key, when it asks for a passphrase I would actually suggest just leaving it blank. The second command copies the key to your clipboard so we can paste it later.

From there you are going to want to add your key to github. Open your github account [here](https://github.com/settings/keys). Go to the top right corner of any page, and click your profile photo. Click “settings”.

From the settings page, in the “access” section of the sidebar, click “ssh and gpg” keys. Click “new ssh key”. Give it a title, past the contents of your clipboard into the key field, and then click “add ssh key”.

That’s it, you should now be able to use git with ssh.

# Intellij IDEA
Intellij IDEA is going to be our java IDE or Integrated Development Environment of choice. Jetbrains offers two versions, the community and pro. If you can afford it, I’d suggest springing for pro. If you are ballin’ on a budget, go for the community. My tutorials will be using the pro version, but each “pro” feature used will have a “community” work around.

IDEA can be downloaded [here](https://www.jetbrains.com/idea/download/#section=mac), it’s just a simple app, download and open.

# Pycharm
Pycharm is going to be our python IDE or Integrated Development Environment of choice. Jetbrains offers two versions, the community and pro. If you can afford it, I’d suggest springing for pro. If you are ballin’ on a budget, go for the community. My tutorials will be using the pro version, but each “pro” feature used will have a “community” work around.

Pycharm can be downloaded [here](https://www.jetbrains.com/pycharm/download/#section=mac), it’s just a simple app, download and open.

# VS Code
VS Code will be our javascript IDE of Integrated Development Environment of choice. It is built by Microsoft, and at the time of writing this blog, was offered for free.

VS Code can be downloaded [here](https://code.visualstudio.com/download), it’s just a simple app, download and open.

# This, is where the fun begins.
If you are new to this, and you made it through all this in one sitting. Congratulations, I mean it,  it may not feel like it, but we did a lot. We took your clean mac and decked it out with the tools and programs needed to code. Java? Python? Javascript? Your machine is ready for all of them. So the only question worth asking now, which will we start with?

Stay curious my friends.
-C3

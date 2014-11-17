CarbonROM Source
===================

Getting Started
---------------
To get started with the CarbonROM sources, you'll need to get
familiar with [Git and Repo](http://source.android.com/source/version-control.html).


Create the Directories
----------------------

You will need to set up some directories in your build environment.

To create them run:

    mkdir -p ~/bin
    mkdir -p ~/CarbonROM


Install the Repository
----------------------

Enter the following to download the "repo" binary and make it executable:

curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo && chmod a+x ~/bin/repo

You may need to reboot for these changes to take effect. 
Now enter the following to initialize the repository:

    cd ~/CarbonROM


Repositories:
---------------

Before you continue --> run this in the terminal
----------------------------------------
    repo init -u https://github.com/CarbonROM/android.git -b lollipop && repo sync -f

*PLEASE NOTE THAT YOU MUST USE THE -f flag when repo syncing/initializing if you want to sync with our default -j8 setup as android.googlesource seems to like to reject your requests if you set your -jflag too high. 
if you wish to avoid this issue run it repo sync -j1 otherwise -f (force) is recommended so it will resync the repos it gets error codes on. Thank you and have a nice day.*


Building the System
---------------

Initialize the environment with the envsetup.sh script. Note that replacing "source" with a single dot saves a few characters, and the short form is more commonly used in documentation.

    . build/envsetup.sh
    lunch

Enter the number of the build you want to start and press enter

Build the Code:

    make carbon -j7 = Run Squisher/Run Opticharger
    make otapackage -j7 = No Squisher/No Opticharger


Submitting Patches
------------------
Patches are always welcome!  Please submit your patches via CarbonDev Gerrit!
You can do this by using these commands:

    Setting up for repo upload: (run these commands once)
    git config --global review.review.carbonrom.org.username <Your username registered at CarbonDev gerrit>
    git config --global review.review.carbonrom.org.email <Your email registered at CarbonDev gerrit>

    (From root android directory)
    . build/envsetup.sh
    repo start lollipop .
    (Make your changes and commit)
    repo upload .

Note: "." meaning current directory
For more help on using this tool, use this command: repo help upload

Make your changes and commit with a detailed message, starting with what you are working with (i.e. vision: Update Kernel)
Commit your patches in a single commit. Squash multiple commit using this command: git rebase -i HEAD~<# of commits>

To view the status of your and others' patches, visit [Carbondev Code Review](http://review.carbonrom.org/)

If you have any issues/questions please contact us in channel: #teamcarbon  server: irc.freenode.net

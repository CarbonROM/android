# CarbonROM Source

Thanks for choosing CarbonROM!

## Getting Started

To get started with the CarbonROM sources, you'll should be familiar with [Git and Repo](http://source.android.com/source/version-control.html).

## Create the Directories

You will need to set up some directories in your build environment. One is your local binaries folder (to install repotool) and the other is for your CarbonROM source.

To create them run:

```sh
mkdir -p ~/bin
mkdir -p ~/carbon
```

## Install dependencies

Building Android has many dependencies that you need. Just stick this in your terminal and run it.

```sh
sudo apt-get install git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev libgl1-mesa-dev libxml2-utils xsltproc unzip python
```

## Install repo tool

Enter the following to download the "repo" binary and make it executable:

```sh
curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```

You will need to add the `~/bin` folder to your path if you've not done so before.

Open your `.bashrc` file in your favourite editor, and add `PATH=~/bin:$PATH` to the end of it on a new line, then run `source ~/.bashrc` to update your environment.

```sh
sudo gedit ~/.bashrc
# add the line PATH=~/bin:$PATH to it
source ~/.bashrc
```

## Initialising the repository

Move to the CarbonROM working directory and initialise the repo using the manifest located here, then sync the repos. You may get a prompt about using color. Just choose yes or no and hit enter.

```sh
cd ~/carbon
repo init -u https://github.com/CarbonROM/android.git -b cr-8.0
repo sync -j8
```

Yes, the branch is `cr-8.0`. That's CarbonROM 8, which runs on Android 10. Not Oreo. 10. Ten. T-E-N. TEN.

### Troubleshooting

If you get an error about not locating your git details/email/name, you'll need to configure your details in the git config.

```sh
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

<!--  -f is default behaviour in new repotool
*PLEASE NOTE THAT YOU MUST USE THE -f flag when repo syncing/initializing if you want to sync with our default -j8 setup as android.googlesource seems to like to reject your requests if you set your -jflag too high.
if you wish to avoid this issue run it repo sync -j1 otherwise -f (force) is recommended so it will resync the repos it gets error codes on. Thank you and have a nice day.*-->


## Building the system

**macOS Users:** you **are** required to install `coreutils` from MacPorts before you continue.

Initialize the environment with the `envsetup.sh` script. Note that replacing "source" with a single dot saves a few characters, and the short form is more commonly used in documentation.

```sh
. build/envsetup.sh
lunch
```

Enter the number of the build you want to start and press Enter.

After, run the make command. The top one will build at a speed that is most suitable for your device. You can manually set a number of threads to build with by replacing `12` in the bottom command with the number of threads to use.

```sh
make carbon -j$(nproc --all)
# or
make carbon -j12
```

### Submitting Patches

Patches are always welcome!  Please submit your patches via CarbonROM Gerrit!
You can do this by using these commands:

### Set up

You need to set up your details. You only need to do this once.

```sh
git config --global review.review.carbonrom.org.username <Your username registered at CarbonROM gerrit>
git config --global review.review.carbonrom.org.email <Your email registered at CarbonROM gerrit>
```

### Creating and uploading patch

```sh
cd ~/carbon
. build/envsetup.sh
repo start cr-8.0 .
# make your changes and commit
repo upload .
```

### GPG signing

We will only allow GPG signed commits on our Gerrit/GitHub orgs, as well as require a signed push.

You can set up signed commits by setting up the key accoridng to these directions on the [Git-SCM Site](https://git-scm.com/book/en/v2/Git-Tools-Signing-Your-Work) and adding them to [Gerrit](http://review.carbonrom.org/#/settings/gpg-keys)

You can enable the signed push with:

```sh
git config --global push.gpgSign if-asked
```


...and enable signing your commits with:

```sh
git config --global commit.gpgsign true
```

Note: "." meaning current directory
For more help on using this tool, use this command: `repo help upload`

Make your changes and commit with a detailed message, starting with what you are working with (i.e. vision: Update Kernel)
Commit your patches in **one single commit**. Squash multiple commit using this command: git rebase -i HEAD~<# of commits>

To view the status of your and others' patches, visit [CarbonROM Code Review](http://review.carbonrom.org/)

If you have any issues/questions please contact us in channel:
 #carbonrom       //General-related questions
 #carbonrom-dev   //Development-related questions

 server: irc.freenode.net

## Attention Themers

You can find all CarbonROM Resources that need to be themed [here](https://github.com/CarbonROM/ThemeResources)
Let us know when there is anything else we can help with, we will gladly do.

## Translating CarbonROM

We use crowdin for our ROMs translation. If you want to help with that, you can do so here.
https://crowdin.com/project/carbonrom

The available projects to translate will be updated when new things come into Carbon, so be sure to keep on checking the page.

Many thanks to those who have helped translate the ROM!


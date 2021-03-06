# OKD Flask App
Learn how to deploy applications in the OKD, the open source community version of OpenShift. Below are instructions on how to configure Minishift in order to deploy many applications using the OKD containerization platform console. This Flask App is deployable.

Definitions to know:

**Minishift** – Command Line command responsible for launching a single-node OKD cluster inside a virtual machine to run ODK locally. Running this cluster allows you to then connect to the OKD interface located at the web console URL. MUST be running in order to access OKD. 

**OKD** – Optimized distribution of Kubernetes that allows you to create and manage containers; the community edition of RedHat’s OpenShift container platform. Provides a way to create a local, all-in-one cluster on your own machine using the oc command-line tool. Also adds developer and operation-centric tools for container management through rapid app development, easy deployment, and scaling. More information on OKD can be found here. 

**OpenShift Cluster** – A cluster is a group of connected machines or nodes working together to act as one. A Kubernetes cluster consists of one or more masters and a set of nodes.  


# Getting Started with OKD
Set up the OpenShift environment using OKD, create your own web app in a text editor, and deploy your web app via OKD using GitHub.
Objectives:
•	Set Up the OKD Environment
•	Create Your Own Web App
•	Deploy Python App on OKD

**Prerequisites**
1.	Homebrew

If you do not have Homebrew installed, please go to terminal and run:

`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"`

If this does not work, go to brew.sh and run the command in the box under Install Brew.
 

2.	GitHub Account

GitHub is a FREE repository space to store code. In this document we are going to upload our application to GitHub and allow OKD to pull it from there in order to deploy it.

3.	Text Editor

To create the web application, download a text editor. Atom or Sublime is recommended.


# Set Up the OKD Environment
OKD is the platform is where you will be creating and deploying applications. Install minishift and OpenShift CLI tools via Homebrew in the macOS terminal. Then, create an instance of Minishift to run the OKD cluster inside VirtualBox. Finally, you will set up your OKD credentials and log into the OKD web browser platform. 

**Install VirtualBox Virtualization Environment**
1.	Visit VirtualBox website at https://www.virtualbox.org/wiki/Downloads
 

2.	Under VirtualBox 6.1.4 platform packages, press OS X host to trigger download. Open and configure. 
*Note:  Your computer may be set to deny applications from the web, rendering VirtualBox unable to download. To allow VirtualBox to download on your computer, go to System Preferences > Security & Privacy > General. Press the golden lock at the very bottom of the page. Enter your password and you should physically see it unlock. Reopen the download and everything should go through.

## Minishift and CLI tools

Minishift launches a single-node OKD cluster inside a virtual machine. The OpenShift CLI (Command Line Interface) allows you to use oc commands too. (

## Install Minishift and OpenShift CLI

1.	Install Minishift via Homebrew and update the binary:  
```
brew cask install minishift
brew cask install --force minishift
```

3.	Install OpenShift CLI:
```
brew install openshift-cli
```

### Starting Minishift

Start the minishift VM inside VirtualBox and the OKD OpenShift cluster. If a minishift instance is already present in VirtualBox and you want to start a new one, you must run minishift delete, then run the minishift start again to replace it. 

Upon a successful minishift launch, the terminal will give you the URL to access the OKD console. Finish Setup before visiting OKD console URL.:
1.	Create an instance of Minishift inside VirtualBox:
```
minishift config set vm-driver virtualbox
```

2.	Start minishift VM inside VirtualBox and spin up the OKD OpenShift cluster
```
minishift start
```
(To stop the cluster when you are done, run: `minishift stop`. This is NOT the same as stopping the minishift cluster, this is deleting it.)

### Starting OKD

You must start the minishift server (`minishift start`) in order to run and access the OKD console in this section usiing `minishift console`.


1.	On the very first boot of OKD, you should make a username and password to create a workspace. This workspace is where you can access and manage your cluster. Run the `oc login` command and follow the prompts. 

If prompted for a server name, enter YOUR web console URL without the ‘/console’ at the end. If you forget these credentials, you can run `oc login` again and create another set of credentials for a new empty workspace. Acting as administrator grants access to all OKD projects. 

To become admin, run: 
```
oc login -u system:admin
```
2.	Access the OKD console to start deploying apps.
```
minishift console
```
A secure browsing message will show in the browser if using the link. Just click ‘Advanced’ and click the link directly below to continue

The OKD console should be in the browser! Now, log in with the credentials you just made and congrats! You can create a project or manage your cluster through the dashboard.




## Troubleshooting
**"Could not set oc CLI context for 'minishift' profile"
"Error starting the VM"**

Known Causes: Updating VirtualBox

Workaround:
```
$ minishift delete --force //Must use --force flag. Regular minishidt delete does NOT work
$ rm -rf ~/.minishift
$ minishift setup-cdk //If this command does not work, proceed to the next 
$ minishift config set vm-driver virtualbox
$ minishift start
```

**"Cannot set oc CLI context"**

Unknown Cause

Workaround:
```
$ oc login
```
If prompted for server, enter the web console url without the '/console' attached at the end. Continue through prompts.


**Minishfit error in VirtualBox**

Known Cause

Workaround:
Uninstall and reinstall VirtualBox

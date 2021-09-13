# R for Research

Activities for learning R for research. 

## Getting started


### Set up SSH keys

To check out the code locally, I recommend that you configure your SSH keys.
Open a terminal, and do this:

```
$ ls ~/.ssh
```

If you get an error because that directory does not exist, then run this command:

```
$ ssh-keygen
```

Press "Enter" repeatedly to accept the default answers (unless you really want to type a passphrase when using your key).
Then try again:

```
$ ls ~/.ssh
codecommit      config          id_rsa.pub
codecommit.pub  id_rsa          known_hosts
```

If all goes well, you should have an _id_rsa_ file, which is a **private** SSH key that should be kept private.
Do not share the contents of this file or copy it anywhere.
You can use the `cat` command to look at the contents of the **public** SSH key in _id_rsa.pub_:

```
$ cat ~/.ssh/id_rsa.pub
```

Copy all the text you see from "ssh-rsa" to the end.
Then go to your [GitHub settings](https://github.com/settings/profile), click on "SSH and GPG keys," then click the big green "New SSH key" button.
Give the new key a name like "laptop" (you may add keys from other machines like the HPC) and paste in the contents of the **public** key.
Click the "Add SSH key" button to save your new key.


### Fork this Repository

Next, go to the [repository](https://github.com/schackartk/R_for_research) and click the "Fork" button to make a copy of the code into your account. 

### Clone the Repository Locally

Now that you have a fork of the repository, find a place on your machine where you would like
to create a local clone of it. On Windows, you can go there in File Explorer, then click git bash here to open a bash terminal.

```
git clone git@github.com:YOUR_GITHUB_ID/R_for_research.git
```

If that goes well, you should have a _R_for_research_ directory.
Go into that directory:

```
cd R_for_research
```

You will need to configure my original GitHub repo as an _upstream_ source, so that you can get updates to the repo, with the following command:

```
git remote add upstream https://github.com/schackartk/R_for_research
```

I will make updates to the repo periodically to add new materials.
You will use this command to _pull_ my changes into your repo:

```
git pull upstream main
```


---
title: installing Go on Windows and linux(updated)
published: true
---

# [](#header-1)Windows

Download the latest installer from the website [here](https://go.dev/dl/).Run it and follow the prompts ,it will setup go automatically on you system open a terminal by running `win+r` and typing `cmd` in the prompt,then run `go version`

# [](#header-2)Linux

Download the latest Archive from the website [here](https://go.dev/dl/)

Remove any previous Go installation by deleting the /usr/local/go folder (if it exists), then extract the archive you just downloaded into /usr/local, creating a fresh Go tree in /usr/local/go:

      $ rm -rf /usr/local/go && tar -C /usr/local -xzf go1.20.3.linux-amd64.tar.gz
      

(You may need to run the command as root or through sudo).

Do not untar the archive into an existing /usr/local/go tree. This is known to produce broken Go installations.
Add /usr/local/go/bin to the PATH environment variable.

You can do this by adding the following line to your $HOME/.profile or /etc/profile (for a system-wide installation):

          export PATH=$PATH:/usr/local/go/bin
          

Note: Changes made to a profile file may not apply until the next time you log into your computer. To apply the changes immediately, just run the shell commands directly or execute them from the profile using a command such as `source $HOME/.profile`.
Verify that you've installed Go by opening a command prompt and typing the following command:

          $ go version
          

Confirm that the command prints the installed version of Go.


Create a new GitHub repository and add a file named README.md.
Your README.md file should include all of the following:

i. The IP address and SSH port so your server can be accessed by the reviewer.

ii. The complete URL to your hosted web application.

iii. A summary of software you installed and configuration changes made.

iv. A list of any third-party resources you made use of to complete this project.
Open your ~/.ssh/udacity_key.rsa file in a text editor and copy the contents of that file.
During the submission process, paste the contents of the udacity_key.rsa file into the "Notes to Reviewer" field.


IP ADDRESS
```
35.165.176.112
```

SSH Port `2200`

URL
```
???
```

## Launching and connecting to Virutal Machine
1. With the provided `udacity_key.rsa` file moved to the local directory `~/.ssh/`,
ssh into the instance with command:
```
ssh -i ~/.ssh/udacity_key.rsa root@35.165.176.112
```

## Creating user `grader` and giving user sudo permissions.
As root user, execute the following command:
```
sudo adduser grader
```
Password provided in the reviewer notes.
Then, use command `sudo visudo` to view file `/etc/sudoers.tmp` and add the `grader` line under root:

```
# User privilege specification
root    ALL=(ALL:ALL) ALL
grader  ALL=(ALL:ALL) ALL

```

To confirm user, install `finger` with:
```
sudo apt-get install finger
```
Then use command `finger` to display users.

## Switching users
In a separate terminal, use command the following command to ssh into the instance as `grader`:

```
ssh grader@35.165.176.122 -p 2222
```

## Update Installed Packages
As `grader`, execute the following commands:
```
sudo apt-get update
sudo apt-get upgrade
```

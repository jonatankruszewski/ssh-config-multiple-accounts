# set-multiple-git-accounts

- Navigate to your root folder
```
cd ~
```

- Run the SSH Agent
```
ssh-agent
```

```
ssh-keygen -t ed25519 -C "<your_email_1>"
```

To change the location pass the full path:

```
/home/my_user/.ssh/id_01
```

- Create a new SSH key pair. You can give it a passphrase. If so, remember it.
In your home directory inside the folder .ssh you will have the new id_rsa and id_rsa.pub files.
You can rename them to id_rsa_work and id_rsa_work.pub.

- Copy the content of id_rsa_work.pub. Go to your git account in the cloud, and under the settings, SSH Keys, add the new key. You can give it a name as identifier.
For example: 'Work_pc_ubuntu'

- Repeat process for your second account.

- Add the keys to the SSH Agent. To do that:
```
cd ./.ssh
eval $(ssh-agent -s)
ssh-add -D //deletes all previous keys
ssh-add id_rsa_work
ssh-add id_rsa_personal
```

- Check them that you added with
```
ssh-add -l
```

- Create a config file inside the .ssh folder:
```
touch config
```

- Paste the following into that file:
```
#The default config
Host github.com
   HostName github.com
   User git
   IdentityFile ~/.ssh/id_rsa_work

   
# The other one:
Host github.com-personal
   HostName github.com
   User git
   IdentityFile ~/.ssh/id_rsa_personal
```

If you are using windows, the paths to the identity files should look like the ones in this snippet:

```
Host github.com
  HostName github.com
  User workUser
  IdentityFile /c/Users/<windows_user>/.ssh/id_rsa_work

Host github.com-CDC
  HostName github.com
  User personalUser
  IdentityFile /c/Users/<windows_user>/.ssh/jid_rsa_personal

```
Before authenticating the users, paste the content of the public key in your Github Account
Do it for all the accounts


- Authenticate the users:
```
ssh -vT git@github.com
ssh -vT git@github.com-personal
```

- Go up one folder:
```
cd ..
```

- Modify .gitconfig:

```
[core]
	editor = \"C:\\Users\\ITC\\AppData\\Local\\Programs\\Microsoft VS Code\\Code.exe\" --wait
	longpaths = true
[user]
	email = work@email.com
	name = myName
[filter "lfs"]
	clean = git-lfs clean -- %f
	smudge = git-lfs smudge -- %f
	process = git-lfs filter-process
	required = true

[includeIf "gitdir/i:C:/<user>/dev/Repos/Personal/"]
    path = .gitconfig-personal

[alias]
    setpersonalmail = "config user.email 'personal@email.com'"
	  setworkmail = "config user.email 'work@email.tech'"
```

- Create in the same folder a file .gitconfig-personal. It should have the same configuration, except for the email and the includeIf:
```
[core]
	editor = \"C:\\Users\\ITC\\AppData\\Local\\Programs\\Microsoft VS Code\\Code.exe\" --wait
	longpaths = true
[user]
	email = personal@email.com
	name = me
[filter "lfs"]
	clean = git-lfs clean -- %f
	smudge = git-lfs smudge -- %f
	process = git-lfs filter-process
	required = true

[alias]
    setpersonalmail = "config user.email 'personal@email.com'"
	  setworkmail = "config user.email 'work@email.tech'"
```

That is it. Now to clone something from work:
git@github.com:workrepo
to clone something personal:
git@github.com-personal:personalrepo

Make sure that all the personal repos goes to the personal folder.


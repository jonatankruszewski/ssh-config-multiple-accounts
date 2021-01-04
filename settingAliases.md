# Setting Alias both in Windows, Ubuntu

```
cd
```

```
touch .bashrc
```

```
code .bashrc
```

paste the following aliases:

```
alias gs='git status'
alias gpa='find . -type d -name .git -exec sh -c "cd \"{}\"/../ && pwd && git pull" \;'
```

Save the file.

- [Link to Source](https://superuser.com/questions/602872/how-do-i-modify-my-git-bash-profile-in-windows)
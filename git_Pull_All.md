### Setting Aliases for the Terminal:

you need to run:

```
alias=<name_of_the_alias> "command to operate"
```

To set a pullall:

```
alias=pullall "find . -mindepth 1 -maxdepth 1 -type d -print -exec git -C {} pull \;"
```

To set a reset hard all:
```
alias=resetallH "find . -mindepth 1 -maxdepth 1 -type d -print -exec git -C {} reset --hard \;"
```

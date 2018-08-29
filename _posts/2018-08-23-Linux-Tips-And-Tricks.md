---
layout: post
title: Linux Tips And Tricks
published: true
---

It seems that publishing a post of Linux tips & tricks is a rite of passage that all engineers must go through. More importantly, it's a bookmark for my future self to find these eclectic mix of commands easily with minimal googling.

So without further ado, here's my list:

### find  
This command is very helpful while searching for needles in a haystack. It also has plenty of modifiers (too many to list), so I'll only mention the ones I use almost daily.

The general syntax of the command is:

```
$ find <starting directory> \
  -type <type of file/directory> \
  -name "<Regex of the file/dir name>" \
  -exec <arbitrary command to execute> {} \;
```

Basic example looking for java files:

```
$ find ~/projects -type f -name "*.java"
```

Example looking for directories called main

```
$ find ~/projects -type d -name "main"
```

We can also recursively execute a command on the matching files. This exposes the true power of the find command.

Example: Search all java files for the Main function. The output of this command will only be the matched strings.

```
$ find ~/projects -type f -name "*.java" -exec grep -i "Main" '{}' \;
```

Alternatively, if you wish to output the name of the matching file along with the matched string:

```
$ find ~/projects -type f -name "*.java" -exec grep -i "Main" '{}' +
```

Notice the difference in how the command ends. The braces `'{}'` are substituted by each matching file name at runtime. It's similar to how `xargs` works.

### less
For log files (typically large) and files that I wish to only read and
**NOT** edit, I use the `less` command extensively. One of the major
reasons I love this command is, I can tail files without it
cluttering my terminal. This command also has the benefit of only
loading the file partially into memory, thereby making it a sleek
alternative to `vi`

Example:
```
$ less /var/log/insanely-large-log-file.log
```

Once inside, you can use `G` to go to the end of the file or use `F` to tail the file.

Alternatively, you can open & tail the file directly using

```
$ less +F /var/log/insanely-large-log-file.log
```

To quit and return to the terminal, use the normal `vi` command

```
<ESC> :q
```

### entr

I recently came across this command and although it hasn't made it to my most frequently used commands, I think it's pretty useful. It would be a crime to compile such a list and not mention `entr`

This command allows users to execute an arbitrary script whenever a file changes. It's similar to `watchr`, `guard` & `nodemon`. Since `entr` is written in C, it's faster and more responsive on larger directories.

Usecases can range from running test cases whenever your source files change

```
$ ls *.c | entr 'make && make test'
```

or reloading the browser whenever an HTML file changes.

```
$ ls *.css *.html | entr reload-browser Firefox
```

You can also restart server processes using the `-r` modifier

```
$ ls *.rb | entr -r ruby main.rb
```

Check out more details [here](http://www.entrproject.org/).

### htop   
If you are looking at your machine's performance in any way apart from
`htop`, you're doing it wrong. It's what `top` should have been all along. Although it's not built-in, you can easily install it via:

```
$ apt install htop
```

or

```
$ brew install htop-osx.
```

The output is very self-explanatory and easier to understand & sort.

### jq
Your search for a JSON parser ends here. `jq` runs on a stream of JSON data. Each input is parsed as a sequence of whitespace-separated JSON values which are passed through each filter of `jq`. The filters themselves, can be combined in any way by piping the output of one filter to the input of another.

Example:

This example extracts the field 'foo' from the input JSON.

```
$ jq '.foo' {"foo": 42, "bar": "less interesting data"}
```

```
=> 42
```

This example extracts the 0th element of the JSON array.

```
$ jq '.[0]' [{"name":"JSON", "good":true}, {"name":"XML", "good":false}]
```

```
=> {"name":"JSON", "good":true}
```

### vim commands
By popular opinion, vim is the awesomest editor in town. But for newbies, it can be a little daunting and un-friendly. Once you get vim, you'll never go back to any other editor.

The following vim commands aren't for newbies. It's for more advanced users.

How often do you open a file in vim to edit it and realize you should have opened it as *root*? You can use the following command to save your changes without exiting vim.

```
<ESC> :w !sudo tee %
```

Slightly longer to type but completely worth it.

I think vim commands demand a dedicated post to do justice to the most beloved editor.

### Conclusion

I hope this was useful. I'll probably edit this post to reflect any new commands that cross my path/blow my mind.

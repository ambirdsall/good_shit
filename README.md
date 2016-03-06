# Good Tricks
Shit I have found useful, recorded for future reference. Focused on tools and workflows I like to use. Feel free to open a PR if you have a good trick, too!

#### Get rid of incorrect HTML-escaping on [Pro Git](https://git-scm.com/book/en/v2/)
Fire up the console and copy-paste. `&gt;` is but one of many, but it's the most common one I've run into.
```js
$('pre').each(function(idx, pre) {
  $(pre).text($(pre).text().replace(/&lt;/g, '<'))
  $(pre).text($(pre).text().replace(/&gt;/g, '>'))
})
```

#### Change a variable name project-wide
1. In project root dir: `$ vim $(ack 'bad_variable_name' -l)`
2. In vim: `:argdo %s/bad_variable_name/good_variable_name/gc | update`

Step 1: open every file containing `bad_variable_name` in vim.

Step 2: `argdo` applies the command to every file given as an argument; `c` flag can be left off, but then make sure to `git add -p`; piping to `update` saves each file after making all substitutions. If you don't do the `ack` bit at first, add an `e` flag to the `:%s` to suppress any errors from files without a match.

#### Convert Ruby hash syntax from 1.8-style to 1.9-
s/o https://robots.thoughtbot.com/convert-ruby-1-8-to-1-9-hash-syntax
##### In vim, one file:
```vim
:%s/:\([^ ]*\)\(\s*\)=>/\1:/g
```
##### In terminal, whole project:
```sh
perl -pi -e 's/:([\w\d_]+)(\s*)=>/\1:/g' **/*.rb
```

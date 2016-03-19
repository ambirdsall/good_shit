# Good Tricks
Shit I have found useful, recorded for future reference. Focused on tools and workflows I like to use. Feel free to open a PR if you have a good trick, too!

#### extending vim's command language
| Verb | Meaning |
|------|--------|
| `gc` (`cm`?) | [comment](https://github.com/tpope/vim-commentary)
| `cx` | [exchange](https://github.com/tommcdo/vim-exchange)
| `gr` | [go replace (from register)](https://github.com/vim-scripts/ReplaceWithRegister)
| `gs` | [go sort](https://github.com/christoomey/vim-sort-motion)
| `gt` | [titlecase](https://github.com/christoomey/vim-titlecase)
| `cp` | [system clipboard](https://github.com/christoomey/vim-system-copy)


| Text Object | Meaning |
|------|---|
| `ae` | [entire file](https://github.com/kana/vim-textobj-entire)
| `i` | [contiguous indent level](https://github.com/kana/vim-textobj-indent)
| `l` | [line, ignoring leading whitespace](https://github.com/kana/vim-textobj-line)

#### Get rid of incorrect HTML-escaping on [Pro Git](https://git-scm.com/book/en/v2/)
Fire up the console and copy-paste. `&gt;` is but one of many, but it's the most common one I've run into.
```js
$('pre').each(function(idx, pre) {
  $(pre).text($(pre).text().replace(/&lt;/g, '<'))
  $(pre).text($(pre).text().replace(/&gt;/g, '>'))
  $(pre).text($(pre).text().replace(/&amp;/g, '&'))
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

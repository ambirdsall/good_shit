# Good Tricks
Shit I have found useful, recorded for future reference. Focused on tools and workflows I like to use. Feel free to open a PR if you have a good trick, too!

#### Change a variable name project-wide
1. In project root dir: `$ vim $(ack 'bad_variable_name' -l)`
2. In vim: `:argdo %s/bad_variable_name/good_variable_name/gc | update`

1. opens every file containing `bad_variable_name` in vim.
2. `argdo` applies the command to every file given as an argument; `c` flag can be left off, but then make sure to `git add -p`; piping to `update` saves each file after making all substitutions. If you don't do the `ack` bit at first, add an `e` flag to the `:%s` to suppress any errors from files without a match.

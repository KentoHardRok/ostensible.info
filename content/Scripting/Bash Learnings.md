+++
title = "Bashing"
weight = 51
+++

#scripting/bash #scripting/sh 
# bash defaults
first we place the `set -eou pipefail` at the top of the script right after the shebang. 
The `set` command changes script execution options. For example, normally bash does not care if some command failed, returning a non-zero exit status code. it just happily jumps to the next one. Here is a link going down into the weeds as to what each option does and why we need it. [pipfail explained](https://vaneyckt.io/posts/safer_bash_scripts_with_set_euxo_pipefail/)

# Tidbits
`\` - this is an escape character, it does that, escapes characters so they aren't interpreted by the command line. AKA just treated as the character they are. ASCII equality. 

# Quotes and such

`"` - this nasty guy is used all over the place and its easy to not fully understand what he is doing. SO, what's significant to remember is that this is used to interpret variables. so that \$NUM will become 5 or whatever you have assigned. When it comes to strings it will also display strings as is and interpret things like line end /n. 
`'` - single quote literally interprets what is placed within it. so `@NUM` becomes `@NUM`, literally. thats all there is to that.
`'` - the back tick is used to run commands, so bash and such is interpreted with this. Text between backticks is executed and replaced by the output of the command. That is called command substitution because it is substituted with the output of the command. So if you want to print 5, you can't use backticks, you can use quotation marks, like echo "$b" or just drop any quotation and use echo $b.

#sed

# sed things
### search and replace strange things
#### replace the seperator
so if your string includes characters such as `/`, it will mess up your command, so you can change the default seperator. You enter a quote single or double, then the s for search then the next character will be the new seperator for this command. `"s|apple|orange|g"` this would replace apple with orange.


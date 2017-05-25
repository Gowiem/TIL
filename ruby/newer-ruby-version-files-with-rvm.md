# Creating the .ruby-version/.ruby-gemset files with RVM

Previously I had always used `rvm --rvmrc --create VERSION@GEMSET`. This now throws a warning as `.rvmrc` files are deprecated in favor of the more general `.ruby-version` and `.ruby-gemset` files which other tools use as well. These can be created in much the same way:

`rvm --ruby-version --create VERSION@GEMSET`

Simple! :sweat_smile:

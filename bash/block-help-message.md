# Top Comment block as --help message in Bash

You can use `sed` and top level block comments to provide an easy help message mechanism:

```bash
#!/bin/bash
###
### my-script — does one thing well
###
### Usage:
###   my-script <input> <output>
###
### Options:
###   -h        Show this message.

help() {
    sed -rn 's/^### ?//;T;p' "$0"
}

if [[ "$1" == "-h" ]]; then
    help
    exit 1
fi
```

More info: https://samizdat.dev/help-message-for-shell-scripts/
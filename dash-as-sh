#!/bin/bash

# Doesn't work on non GNU systems. There is no -i option for sed in non-GNU
# Get the scripts that have #!/bin/sh shebang and are not posix compliant. Change shebang to #!/bin/bash 
for i in $(find $(echo $PATH | sed 's/:/ /g') -type f -perm -o=r -print0 | xargs -0r gawk '/^#!.*( |[/])sh/{printf "%s\0", FILENAME} {nextfile}' | xargs -0r echo); do
    shellcheck --format=quiet --shell=dash $i
    if [ $? -ne 0 ];
    then
  	sed -i '1s/^#!\/bin\/sh/#!\/bin\/bash/' $i
	sed -i '1s/^#!\/usr\/bin\/env sh/#!\/usr\/bin\/env bash/' $i
    fi
done


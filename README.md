# mutex

## Problem

Automating often results in gluing together bits and peaces of new and old code. Some of this code may not be ready to run in parallel. To avoid race conditions, these peaces can be wrapped in a locking mechanism that ensures only one will run at a time.

## Solution

In this case it is solved by utilising the file system locking mechanism.

    mutex [-h] -n name -- command arg1 arg2 .. argN

      -n name       lock name, creates a file under /var/lock/${name}
      --            command to run with it's all arguments

    Mutex locks in bash implemented with file locking with flock.
    All processes started under the same lock name will run mutual exclusive.

## Test

See how it works

    for i in {1..25}; do ./mutex -n test -- "echo -n lock $i,; sleep .3; echo release $i" & done

###### vim: spell spelllang=en:

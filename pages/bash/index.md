---
title: Mort9 Posts
author: Mortie Torabi 
---

# Bash Scripting

#### Current Directory for a Script

```bash
DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" >/dev/null 2>&1 && pwd )"
```

#### Handle SIGINT (Ctrl-c) signal for a script

```bash
function handle_sigint() # Kill all subprocesses and childs
{
    for proc in `jobs -p`
    do
        kill $proc
    done
}

cmd1 &
cmd2 &
...

trap handle_sigint SIGINT  # calls handle_sigint on SIGINT (ctrl-c)
wait
```

### jq

```bash
jq '..|.updateDate?' # Skip non-json data
```

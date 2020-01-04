---
title: "Docker tips"
date: 2020-01-04T09:05:44Z
tags: [ "development", "container" ]
draft: false
---

Some useful tips for docker

1. Create shortcuts to free up space. On macOS use `alias` in `~/.bash_profile` (I use `~/.bashrc` for aliases, see my .dev/dotfiles repo). Alias is auto expanded by bash shell.    

    ```bash
    # remove just dangling docker images
    alias docker-dangling-images="docker rmi $(docker images --filter dangling=true)"
    
    # remove every stopped containers
    alias docker-stopped-containers="docker rm $(docker ps -a -q -f status=exited)"
    
    # remove every stopped containers, also
    # all networks not used by at least one container, 
    # all dangling images & dangling build cache
    dockerprune="docker system prune"
    ```

2. Useful to modify Docker Hyperkit VM's transparent_hugepages setting in case of redis complaining (macOS Mojave 10.14.x)    
 
   > `WARNING you have Transparent Huge Pages (THP) support enabled in your kernel.`

   see
   : https://github.com/docker-library/redis/issues/55#issuecomment-368346882
   : https://stackoverflow.com/questions/39739560/how-to-access-the-vm-created-by-dockers-hyperkit)  
    
    ```bash
    screen ~/Library/Containers/com.docker.docker/Data/vms/0/tty
    
    echo never > /sys/kernel/mm/transparent_hugepage/enabled
    echo never > /sys/kernel/mm/transparent_hugepage/defrag
    
    # exit: Ctrl-A-K then y
    ```

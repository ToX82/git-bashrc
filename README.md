git-bashrc
==========

This is a little hack to .bashrc to facilitate the use of GIT through colors to indicate the status of the repository.

![preview image](http://emanuele.itoscano.com/files/files/blog/git-bashrc.png)


If you want a shell like that, just add this lines at the end of your .bashrc file:


    Color_Off="\[\033[0m\]"       # Text Reset
    Yellow="\[\033[1;33m\]"       # Yellow
    Green="\[\033[0;32m\]"        # Green
    Red="\[\033[0;91m\]"          # Red
    
    export PS1='$(
      if [ -d .git ]; then 
        status="$(git status)" > /dev/null 2>&1; 
    
        if [[ $status == *"to be committed"* ]]; then 
          # Changes to be committed
          echo "'$Yellow'"$(__git_ps1 " {%s} ") '$Color_Off'\w\$ ""; 
    
        elif [[ $status == *"Changes not staged"* ]]; then 
          # Changes to stage
          echo "'$Red'"$(__git_ps1 " {%s} ") '$Color_Off'\w\$ ""; 
    
        elif [[ $status == *push* ]]; then 
          # Push needed
          echo "'$Green'"$(__git_ps1)* '$Color_Off'\w\$ ""; 
    
        else
          # Clean repository - nothing to commit
          echo "'$Green'"$(__git_ps1) '$Color_Off'\w\$ ""; 
    
        fi
      else 
        # Prompt when not in GIT repo
        echo "${debian_chroot:+($debian_chroot)}\u@\h:\w\$ ";
      fi
    )'
    
Enjoy!

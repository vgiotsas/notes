# Technical Notes

## 1. The environment variables in a user's `~/.bash_profile` file are not available to crontab jobs

Some crontab jobs may fail to work because a binary is in a non-standard path location.
The PATH environment variable is usually updated with these file paths in `~/.bash_profile` or `~/.bashrc`.

There are many different workarounds:

 * Set the environment variable at the top of the crontab file:
 
 ```shell
 ENVIRONMENT_VAR=production

 * * * * * /path/to/command/to/runn
 ```

 * Chain the loading of the `.bash_profile` with the cron job command:
 
 ```bash
 0 5 * * * . $HOME/.profile; /path/to/command/to/runn
 ```

 * Set the `SHELL` to `/bin/bash` at the top of the crontab file and then source the `.bash_profile` 
 
 ```bash
 SHELL=/bin/bash
 
 * * * * * source ~/.bash_profile && /path/to/command/to/run
 ```

More solutions are discussed in the StackOverlow question below:   
https://stackoverflow.com/questions/2229825/where-can-i-set-environment-variables-that-crontab-will-use

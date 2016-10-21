Github Multiple Accounts
================

Scenario
--------

> I have two github accounts, one is my personal Github account `personalAccount`, 
one is my job account `workAccount`.
When I push code at work as `workAccount` to my personal repo.

> it's show - **ERROR: Permission to personalAccount/repo denied to workAccount**

> How do I have the ability to push and pull to multiple accounts via ssh key?

Solution
--------

- Generate new SSH keys
    
    ```bash
    ssh-keygen -t rsa -b 4096 -f "$HOME/.ssh/id_rsa_personalAccount"
    ```
    
- Attach the New SSH Key 

    Add `id_rsa_personalAccount.pub` to `personalAccount` Github account 
  
- Add Key to the ssh-agent
 
    ```bash
    ssh-add "$HOME/.ssh/id_rsa_personalAccount"
    # can use ssh-add -l command to check if is successful added
    ```
    
- Create a Config File
   
   ```bash
    vim "$HOME/.ssh/config"
    ```
    
    content of config file
    ```
    # company
    Host github.com
        IdentityFile ~/.ssh/id_rsa
        HostName github.com
        User workAccount
    # personal
    Host github.com-personal
        IdentityFile ~/.ssh/id_rsa_personalAccount
        HostName github.com
        User personalAccount
    ```
    
- Change remote url
    
    ```bash
    git remote set-url origin git@github.com-personal:personalAccount/test.git  
    ```

Then I can push to my personal repo from company. Wa la la ~~ 

References
----------

* [@by KEVIN BURKE](https://kev.inburke.com/kevin/multiple-github-ssh-accounts/)
* [@by Jeffrey Way](https://code.tutsplus.com/tutorials/quick-tip-how-to-work-with-github-and-multiple-accounts--net-22574)

This file will cover how to use multiple accounts on the same computer. A possibly use case might be you have a personal laptop but 
you are doing work for a client and pushing to a separate repo with a different account (different email).

I found this helpful, but if it doesn't work for you -- there might be a few steps you missed.

[How to use Github with multiple accounts](https://code.tutsplus.com/tutorials/quick-tip-how-to-work-with-github-and-multiple-accounts--net-22574)



[Using Multiple Public SSH Keys](https://superuser.com/questions/272465/using-multiple-ssh-public-keys)


First, if you haven't already, sign up for Github account, well, TWO in fact. You can do that here: [Github Signup](https://github.com/join). I haven't tried it but you might also be able to do this on Bitbucket, for account at Bitbucket, go here: 
[Bitbucket Signup](https://bitbucket.org/account/signup/).

Second, check for your SSH keys. For all things SSH keys related, Github has a great page for [SSH key info](https://help.github.com/articles/connecting-to-github-with-ssh/).

```bash
git config --global user.email "email@example.com"
```

Verify Github Connection:
```bash
ssh -T git@github.com
```


#### [Check if you have ssh keys in your ssh-agent](https://help.github.com/articles/checking-for-existing-ssh-keys/)
```bash
ls -al ~/.ssh
# Lists the files in your .ssh directory, if they exist
```

#### [Generating a new ssh key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key)
```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

#### [Add your keys to the ssh-agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#adding-your-ssh-key-to-the-ssh-agent)
```bash
ssh-add -K ~/.ssh/id_rsa or instead of id_rsa the name of your ssh private key
```

#### Be sure to add your keys to your Github account too!


#### [Make sure to associate your email address for a _single_ repository - non - global](https://help.github.com/articles/setting-your-commit-email-address-in-git/#setting-your-email-address-for-a-single-repository)
```bash
git config user.email "email@example.com"
```



#### Pro Git Book - https://git-scm.com/book/en/v2


#### Troubleshooting Errors

- If you get the `ssh “permissions are too open” error` try `chmod 600 ~/.ssh/id_rsa` or instead of `id_rsa` the name of your ssh private key. 

Resources:
- [StackOverflow - Multiple github accounts on the same computer?](https://stackoverflow.com/questions/3860112/multiple-github-accounts-on-the-same-computer)
- [StackOverflow - ssh permissions are too open](https://stackoverflow.com/questions/9270734/ssh-permissions-are-too-open-error)
- [StackOverflow - ssh has no identities](https://stackoverflow.com/questions/26505980/github-permission-denied-ssh-add-agent-has-no-identities/28444641#28444641)
- [StackOverflow - Error: Permission denied (publickey)](https://help.github.com/articles/error-permission-denied-publickey/)
- [StackOverflow - git submodule with other users](https://stackoverflow.com/questions/6041516/git-submodule-update-with-other-user)
- [StackOverflow - Use a different user.email and user.name for Git config based upon remote clone URL](https://stackoverflow.com/questions/34597186/use-a-different-user-email-and-user-name-for-git-config-based-upon-remote-clone)

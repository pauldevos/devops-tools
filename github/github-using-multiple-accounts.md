This file will cover how to use multiple accounts on the same computer. A possibly use case might be you have a personal laptop but 
you are doing work for a client and pushing to a separate repo with a different account (different email).






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

#### Troubleshooting Errors

- If you get the `ssh “permissions are too open” error` try `chmod 600 ~/.ssh/id_rsa` or instead of `id_rsa` the name of your ssh private key.

Resources:

[StackOverflow - Multiple github accounts on the same computer?](https://stackoverflow.com/questions/3860112/multiple-github-accounts-on-the-same-computer)

## How do I clone a subdirectory only of a Git repository?

You can combine the sparse checkout and the shallow clone features. 
The shallow clone cuts off the history and the sparse checkout only pulls the files matching your patterns.

```
git init <repo>
cd <repo>
git remote add origin <url>
git config core.sparsecheckout true
echo "finisht/*" >> .git/info/sparse-checkout
git pull --depth=1 origin master
```
You'll need minimum git 1.9 for this to work. Tested it myself only with 2.2.0 and 2.2.2.

This way you'll be still able to push, which is not possible with `git archive`.

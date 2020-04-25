## How do I clone a subdirectory only of a Git repository?
例如：我只想有clone仓库下的*verification*目录

You can combine the **sparse checkout** and the **shallow clone** features. 
The shallow clone cuts off the history and the sparse checkout only pulls the files matching your patterns.

```
git init <repo>
cd <repo>
git remote add origin <url>
git config core.sparsecheckout true #设置sparse checkout为 true
echo "verification/*" >> .git/info/sparse-checkout #将要clone的目录相对于repo根目录的路径写入配置文件, *表示所有，!表示匹配相反的.
git pull --depth=1 origin master
```
You'll need minimum git 1.9 for this to work. Tested it myself only with 2.2.0 and 2.2.2.

This way you'll be still able to push, which is not possible with `git archive`.

# Developer notes

This README is intended for developre and maintainer of this blog.

## Edit theme

The theme is added through git submodule as

```bash
git submodule add <theme.github.repo.url>
```

And remove the submodule as:

1. Delete the relevant section from the `.gitmodules` file.

2. Stage the `.gitmodules` changes:

```bash
git add .gitmodules
```

3. Delete the relevant section from `.git/config`.

4. Remove the submodule files from the working tree and index:
`git rm --cached path_to_submodule` (no trailing slash)

5. Remove the submodule's `.git` directory:
`rm -rf .git/modules/path_to_submodule`

6. Commit the changes:
`git commit -m "Removed submodule <name>"`

7. Delete the now untracked submodule files:
`rm -rf path_to_submodule`

Source: https://stackoverflow.com/questions/1260748/how-do-i-remove-a-submodule



## How to publish new post

Place all the posts under the **content** directory. To create a new post with Hugo, use the command:

```bash
cd [root directory of this blog project]
hugo new content/my_new_post.md
```
Replace the `my_new_post` with your correponding article title.

Once you are done with writing up and editing the article, change the *draft* from `true` to `false` to have the article deployed.

## Run Hugo

```bash
hugo serve
```
or 
```bash
hugo server -D
```
to test in debug mode.

To view the page,  open a browser tab and insert the URL:

```
http://localhost:1313/megacephalo-tech-blog/
```

For local hosting.

# The deployed tech blog is at URL:

```
https://megacephalo.github.io/megacephalo-tech-blog/
```

# To add new article

```bash
hugo new ontent content/posts/your_article.md
```

Replace with the actual path to your new article.
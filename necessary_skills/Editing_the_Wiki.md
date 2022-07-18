[Home](../Home)
# How to Edit this Wiki

This page will help you learn how to edit this wiki to add your own contributions. The [Bitbucket documentation][1] also has more information about using a wiki.

Wiki pages are nothing more than plain text files with the `.md` extension. The `.md` extension means that the file is a Markdown file which contains [Markdown syntax](Markdown.md). Markdown syntax allows you to specify text formatting, link to other pages, and do other useful things and is tremendously easy to learn.

There are two ways to edit this wiki:

1. Edit using a web browser
    - Only good for quick and small edits
2. Edit locally on your computer using a text editor and Git
    - Good for edits of any kind, especially larger edits
    - This is the only option available for adding images and PDFs or changing the directory structure of the wiki itself 

---
## Edit Using A Web Browser - Quick and Small Edits


---
## Edit Using A Text Editor and Git - All Edits

>**IMPORTANT:** Understanding [how to use Git](Git.md) is a prerequisite for this method of editing the wiki!

The wiki itself is actually a Git repository that exists alongside the `lab-wiki` repository that currently hosts the wiki. This means you can clone it, edit it locally/offline, add images or any other file type, and push it back to Bitbucket. Pushed changed will be live on the web immediately.

The URL of the wiki is the same as the URL for the `lab-wiki` repository but has `/wiki` appended to it (to specify that we want the wiki itself and not the empty repository hosting the wiki). The wiki can be cloned using:

SSH
```
$ git clone git@bitbucket.org:utahtelerobotics/lab-wiki.git/wiki
```
HTTPS
```
$ git clone https://bitbucket.org/utahtelerobotics/lab-wiki.git/wiki
```

Since the Markdown files that makeup the wiki repository just contain plain text, they are easily created and modified with the text editor of your choice. **[Visual Studio Code](../useful_resources/Visual_Studio_Code.md) is highly recommended as a preferred text editor** because it has built-in support for Markdown syntax highlighting and IntelliSense out-of-the-box and has a Markdown preview window to see how edits affect the rendered page in real-time. There are extensions to enhance the preview window to see what the page will look like on [Bitbucket][2] or [GitHub][3] as well as enable it to [render emojis][4]. There is also a handy [spell checker extension][5]. All of these extensions can be installed and enabled in seconds from within VS Code with a single click.

[1]: https://confluence.atlassian.com/x/FA4zDQ
[2]: https://marketplace.visualstudio.com/items?itemName=hbrok.markdown-preview-bitbucket
[3]: https://marketplace.visualstudio.com/items?itemName=bierner.markdown-preview-github-styles
[4]: https://marketplace.visualstudio.com/items?itemName=bierner.markdown-emoji
[5]: https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker

### Adding Non-Markdown Files

When you edit the wiki locally as a Git repository, you can add non-Markdown files and reference them with links in Markdown files. Most file types do not belong in the wiki, but a few are perfect for it.

#### Images

Images can be embedded into rendered Markdown files. If the image you are embedding cannot be accessed using a URL over the internet, you must put the image into a directory of the wiki itself. Be conscious of good file/directory organization and group images together into a dedicated directory if that makes sense. The path to the image relative to the Markdown file referencing it can then be used.

#### PDFs

Similar to images, PDFs can be added to the wiki file structure and referenced from Markdown files using the standard Markdown link syntax. On Bitbucket, the link will pull up a new tab to display the PDF.


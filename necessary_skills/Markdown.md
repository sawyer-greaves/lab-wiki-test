[Home](../Home.md)
# Markdown Syntax

This wiki uses the [Markdown](http://daringfireball.net/projects/markdown/) syntax.
The [MarkDownDemo tutorial](https://bitbucket.org/tutorials/markdowndemo) shows how
various elements are rendered.

## Syntax highlighting

You can also highlight snippets of text (we use the excellent [Pygments][] library).

Here's an example of some Python code:

```python

def wiki_rocks(text):
    formatter = lambda t: "funky"+t
    return formatter(text)
```


You can check out the source of this page to see how that's done, and make sure to
bookmark [the vast library of Pygment lexers][lexers], we accept the 'short name' or
the 'mimetype' of anything in there.


[Pygments]: http://pygments.org/
[lexers]: http://pygments.org/docs/lexers/

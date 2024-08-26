---
author: John
tags: python archive
---
When reading the source code of [rez-localz](https://github.com/mottosso/rez-localz/blob/0f7a472b25f0a333ad080bbc42a6140249cb8838/python/localz/__main__.py#L124), I noticed that there’s a fancy way to do the clean up before exiting exceptionally.

```python
def excepthook(type, value, traceback):
    """Clean up temporary files"""

    cleanup()
    sys.__excepthook__(type, value, traceback)

...

sys.excepthook = excepthook
atexit.register(cleanup)
```

So the cleanup would get called whenever except encountered or exit exceptionally.

Moreover, there’s a concise implementation to get the total size of a folder:

```python
def dirsize(path):
    return sum(
        os.path.getsize(os.path.join(dirpath, filename))
        for dirpath, dirnames, filenames in os.walk(path)
        for filename in filenames
    )
```

That’s chill.
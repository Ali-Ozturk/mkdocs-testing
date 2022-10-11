# Initial Idea - Documentation Tool

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

The documentation for material UI can be found [Here](https://squidfunk.github.io/mkdocs-material/setup/extensions/python-markdown/#table-of-contents).

We are *only* limited in terms of a subscription based (15 USD) on another page

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.
* `python3 -m <mkdocs>` - For my terminal

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.

## Code Examples
Markdown makes it easy to add code examples 
```python
from urllib.request import Request, urlopen
from lxml import etree
import filecmp
from os.path import exists
import os

req = Request(
    url='https://www.holdsport.net/klub/baderiget-marselisborg', 
    headers={'User-Agent': 'Mozilla/5.0'}
)
html_bytes = urlopen(req).read()
html = html_bytes.decode("utf-8")
content = etree.HTML(html).xpath('//*[@id="wrap"]/div/div[3]/div[3]/div[2]/div/div/div')
content_formatted = (''.join(str(etree.tostring(e)) for e in content))

rel_path = os.getcwd()

if (exists('today.txt')):
	with open('tempFile.txt', 'w') as f:
		f.write(content_formatted)
	cmpResult = filecmp.cmp('today.txt', 'tempFile.txt')
	os.remove('tempFile.txt')

	if (cmpResult):
		print("There are no changes since last time")
	else:
		print("There was a change on the content of the page!!")
		with open('today.txt', 'w') as f:
			f.write(content_formatted)
else:
	with open('today.txt', 'w') as f:
		f.write(content_formatted)


```

### Other languages
It is also possible to use other coding languages than python
```java
public class SwapNumbers {

    public static void main(String[] args) {

        float first = 12.0f, second = 24.5f;

        System.out.println("--Before swap--");
        System.out.println("First number = " + first);
        System.out.println("Second number = " + second);

        first = first - second;
        second = first + second;
        first = second - first;

        System.out.println("--After swap--");
        System.out.println("First number = " + first);
        System.out.println("Second number = " + second);
    }
}
```

## Using inline math (LaTeX)
By providing the tool with links to javascript libraries for math we can write in-line latex code

$$f(x) = x^2 + 4$$
---
layout: post
title: "Color Python output text"
categories: coding
tag: 
  - coding
---

Output text of the Python can look too monotnous as it lacks the color. In order fill life into that, you can use `termcolor` module of Python that helps you color the output text.

In order to use `termcolor` module, you need to first install it using terminal. Use the command:

> pip install termcolor

Once it is installed, you can use the `colored()` function to print coloured output.

Syntax: `colored(output_text, color, highlights, attribute = [])`

`output_text` is the `string` that will be displayed. `color` is the color code of the text, `highlights` is the optional argument for background color and `attribute` is optional argument to highlight text.

Example:

```python
from termcolor import colored

text = colored('Hello, World!', 'red',attrs=[ 'blink'])
text_highlighted = colored('Hello, World!', 'red','on_cyan')
print(text)
print(text_highlighted)
```

Output:

![](\assets\images\colored_text.png)

## References

* [How to add colour to text Python? - GeeksforGeeks](https://www.geeksforgeeks.org/how-to-add-colour-to-text-python/#:~:text=Method%201%3A%20Using%20ANSI%20ESCAPE%20CODE&text=To%20add%20color%20and%20style,and%20color%20with%20code%20ANSI.&text=Functions%20Used%3A,and%2047%2C%20100%20and%20107)

* [termcolor · PyPI](https://pypi.org/project/termcolor/)

<!-- comments also like html comments -->
<!-- Headings -->
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6

<!-- Italics -->
*This text* is italic

_This text_ is italic

<!-- escape especial character -->
\*This text* is italic- no more italic and appearing `*` 


<!-- Strong -->
**This text** is italic

__This text__ is italic

<!-- Strikethrough -->
~~This text~~ is strikethrough

<!-- Horizontal Rule -->

---
___

<!-- Blockquote -->
> This is a quote

<!-- Links -->
[Traversy Media](http://www.traversymedia.com)

when hover on link http://www.traversymedia.com Traversy media is appearing. Below line contain syntax

[Traversy Media](http://www.traversymedia.com "Traversy Media")

<!-- UL -->
* Item 1
* Item 2
* Item 3
  * Nested Item 1
  * Nested Item 2
-----------------------------------------------

<!-- OL -->
**here only 1 is enter in .md file but output preview relevent order**
1. Item 1
1. Item 2
1. Item 3


<!-- Inline Code Block -->
`<p>This is a paragraph</p>`

<!-- Images -->
<!-- Very similar to link syntax just put ! except it -->
![Markdown Logo](https://markdown-here.com/img/icon256.png)

<!-- Github Markdown -->

<!-- Code Blocks -->
```bash
  npm install

  npm start
```

```javascript
  function add(num1, num2) {
    return num1 + num2;
  }
```

```python
  def add(num1, num2):
    return num1 + num2
```

<!-- Tables -->
| Name     | Email          |
| -------- | -------------- |
| John Doe | john@gmail.com |
| Jane Doe | jane@gmail.com |

<!-- Check List -->
Task List isn't appearing in VS code markdown preview. but in github it will show
* [x] Task 1
* [x] Task 2
* [ ] Task 3
<!-- comments also like html comments -->
<!-- Headings -->
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6

#
<!-- Italics -->
*This text* is italic

_This text_ is italic

<!-- escape especial character -->
\*This text* is italic- no more italic and appearing `*` 


<!-- Strong -->
**This text** is bold

__This text__ is bold

<!-- Strikethrough -->
~~This text~~ is strikethrough

<!-- Horizontal Rule -->

---
___

<!-- Blockquote -->
> This is a quote

<!-- Links -->
[Traversy Media](http://www.traversymedia.com)

when hover on link http://www.traversymedia.com Traversy media is appearing. Here is the syntax- [Traversy Media](http://www.traversymedia.com "Traversy Media")

<!-- UL -->
* Item 1
* Item 2
* Item 3
  * Nested Item 1
  * Nested Item 2
-----------------------------------------------

<!-- OL -->
**here only 1 is enter in .md file but output preview relevant order**
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

<!-- Simple formatted Tables -->
<!-- items on the center alignment on cell  -->
| Name     | Email          |
| :--------: | :--------------: |
| John Doe | john@gmail.com |
| Jane Doe | jane@gmail.com |

<!-- items on the right alignment on cell  -->
| Name     | Email          |
| --------: | --------------: |
| John Doe | john@gmail.com |
| Jane Doe | jane@gmail.com |


<!-- Check List -->
Task List isn't appearing in VS code markdown preview. but in github it will show
* [x] Task 1
* [x] Task 2
* [ ] Task 3
* like this

![git hub preview](./images/Screenshot%202023-11-12%20001541.png)![[Pasted image 20231123063118.png]]

- Admonitions are frequently used in documentation to call attention to warnings, notes, and tips. [Admonitions](https://www.markdownguide.org/hacks/#admonitions)
- [An option to highlight a "Note" and "Warning" using blockquote](https://github.com/orgs/community/discussions/16925)
![](assets/Pasted%20image%2020251230154107.png)
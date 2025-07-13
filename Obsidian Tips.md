## Check box hot key mapping

1. Go to the beginning of line and press ==ctrl+shift+c== to get bullet point
2. then again press ==ctrl+shift+c== to get uncheck check box (`ctl+shift+c` is manually maping for this option under settings->hotkeys->Cycle bullet/checkbox)
## Format linking notes & images
- [Embed files](https://help.obsidian.md/Linking+notes+and+files/Embed+files)- Link the image or file or pdf with the preview of link's position. that why we put `!` before the image path
- [Internal links](https://help.obsidian.md/Linking+notes+and+files/Internal+links)-
	- Obsidian supports 2 links formats
		- Wikilink: `[[Three laws of motion]]`
		- Markdown: `[Three laws of motion](Three%20laws%20of%20motion.md)`
	- Better to use Markdown because apart from obsidian, markdown editors also support those links. Here ==`%20`== use for ==represent a space.==.
	- [Real implementation Markdown Link in this vault. See point 2 in this link](./React/React-Vite-TS-Mosh/5%20Building%20Forms#Accessing%20Input%20Fields%20using%20the%20`useState`)
	- [[./React/React-Vite-TS-Mosh/5 Building Forms#Accessing Input Fields using the `useState|Wikilink example to link to the heading]]
- [How to make a link to the specific header in the Markdown file](https://blog.markdowntools.com/posts/how-to-link-to-a-header-in-markdown#:~:text=In%20Markdown%2C%20you%20can%20create,the%20text%20of%20the%20heading.&text=To%20link%20to%20a%20header%2C%20you%20need%20to%20use%20the,id%E2%80%9D%20attribute%20of%20the%20heading.)

## Insert project folder structure
- 1st method
	- Enter the `tree` command and copy the folder structure
- 2nd method- using alt code
	- for that need to use laptop keyboard
	- on number pad
	- while pressing the `alt` enter the suitable code using ***only numpad digit***
    - `├` 195 [Alt Codes](https://www.freecodecamp.org/news/alt-codes-special-characters-keyboard-symbols-windows-list/)
	- Then release the `alt` key
- Get tree view folders +files `tree /f`

## An option to highlight a "Note" and "Warning" using block-quote
> [!NOTE]  
> Highlights information that users should take into account, even when skimming.

> [!TIP]
> Optional information to help a user be more successful.

> [!IMPORTANT]  
> Crucial information necessary for users to succeed.

> [!WARNING]  
> Critical content demanding immediate user attention due to potential risks.

> [!CAUTION]
> Negative potential consequences of an action.

![](assets/Pasted%20image%2020250710155830.png)
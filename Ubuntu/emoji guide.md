# System-Wide Emoji Input on Ubuntu with IBus

A guide to configuring and using the IBus input method for a system-wide emoji shortcut on Ubuntu 24.04 LTS, similar to the `Win + .` shortcut on Windows.

---

## Configuration

Follow these steps to set up the IBus emoji shortcut.


1. **Open IBus Preferences**
   - Press `Ctrl` + `Alt` + `T` to open a terminal.
   - Run the following command:

  ```bash
  ibus-setup
  ```

2. **Set the Emoji Shortcut**
   - In the "IBus Preferences" window, navigate to the **Emoji** tab.
   - Find the "Emoji annotation" shortcut, which may default to `Ctrl` + `Shift` + `E`.
   - Click the `...` button next to the shortcut to change it.
   - Press your desired key combination. For a Windows 11 like experience, use `Super` + `.` (the `Super` key is the Windows key). The field will show `<Super>period`.
   - Click **OK** and close the preferences window.

   ![](assets/Screenshot%20from%202025-06-28%2021-31-30.png)
---

## Usage

Once configured, you can use the shortcut in any text field across the system.

1. **Activate Emoji Input**
   - Press your configured shortcut (e.g., `Super` + `.`).
   - An underlined `e` will appear, indicating that emoji input is active.

2. **Find and Insert Emojis**
   - **To Search**: Start typing a description (e.g., `joy`, `cat`, `rocket`). Suggestions will appear as you type. Press `Space` to insert the best match.
   - **To Browse**: Press `Space` immediately after activating the shortcut to open a categorized list of all available emojis. You can navigate this list with your keyboard or mouse.
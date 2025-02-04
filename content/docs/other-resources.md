---
title: Other Resources
weight: 160
---


## Notepad Replacement
Notepad is a default text editor shipped with Windows. You may want to use Notepad++ instead of Notepad. However, there's no obvious way to do it.
From the version 7.5.9 onward, you can run the following command to make Notepad++ replace Notepad (run in `cmd.exe` with Administrator privileges)[†](#registry-edit-warning):

```batch
reg add "HKLM\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\notepad.exe" /v "Debugger" /t REG_SZ /d "\"%ProgramFiles%\Notepad++\notepad++.exe\" -notepadStyleCmdline -z" /f
```

Note that you may need to use `%ProgramFiles(x86)%\Notepad++\` to substitute for `%ProgramFiles%\Notepad++\` if you have Notepad++ 32-bit installed, or use other path if your Notepad++ is installed in a non-default location.

Use the the following comment to undo the replacement:
```batch
reg delete "HKLM\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\notepad.exe" /v "Debugger" /f
```

This has historically worked from Windows 7 through Windows 10.  However, in Windows 11 it's Notepad UWP version installed, you have to remove Notepad UWP to make the above instructions work.

To remove UWP version of Notepad, you have to launch powershell with admin privileges, then run the following command:
```powershell
Get-AppxPackage *Microsoft.WindowsNotepad* | Remove-AppxPackage
```

For restoring Notepad, launch "Microsoft Store" via Start menu of Windows, search "Notepad", select "Windows Notepad", then click on "Install" button.

### Registry Edit Warning

_**† Warning**: editing your registry can be dangerous; edit your registry at your own risk; the developers of Notepad++ and contributors to this documentation cannot and will not be held responsible for mistakes made during registry changes or unintendended consequences of such edits_

## Explorer Right-Click menu

When you install Notepad++ normally, Notepad++ will add an **Edit with Notepad++** Explorer Right Click action for all file types. (This is separate from any file types that you use the [Settings > Preferences > File Association](../preferences/#file-association) or other Windows-standard means to "associate" that file type with Notepad++.)

### Missing "Edit with Notepad++" Action

If you are missing this feature, you can add it to your registry using your favorite method.  One such method is to save the following as a `.reg` file and run it[†](#registry-edit-warning):

**Single User**
```
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\SOFTWARE\Classes\*\shell\Notepad++]
@="Edit With Notepad++"

[HKEY_CURRENT_USER\SOFTWARE\Classes\*\shell\Notepad++\command]
@="\"C:\\Program Files\\Notepad++\\notepad++.exe\" \"%1\""
```
(If your installation is not in `c:\Program Files\Notepad++`, you will have to adjust that script.)

**All Users** (requires admin privileges)
```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\*\shell\Notepad++]
@="Edit With Notepad++"

[HKEY_CLASSES_ROOT\*\shell\Notepad++\command]
@="\"C:\\Program Files\\Notepad++\\notepad++.exe\" \"%1\""
```
(If your installation is not in `c:\Program Files\Notepad++`, you will have to adjust that script.)

### Windows 11 Right-Click Workarounds

Windows 11 hides the old right click menu, so even with a normal installation or if you've manually added those associations, the **Edit with Notepad++** might not be visible for you in Windows 11; though starting with v8.5.1, the installer should put the action in the main Windows 11 right-click menu again.  For older Notepad++, the Windows right click menu contains a **Show More Options** action which will bring up the old-style right click context menu with the old actions; this can also be accessed using the default <kbd>Shift+F10</kbd> shortcut on a file instead of right-clicking.

If that is not sufficient for you, https://www.tomshardware.com/how-to/windows-11-classic-context-menus describes a possible method of changing your registry[†](#registry-edit-warning) to get the old right click context menu by default again in Windows 11.

If you would rather have it in your modern Windows 11 right click, the following `.reg` files might bring **Edit with Notepad++** to your Windows 11 right click[†](#registry-edit-warning):

**Single User**
```
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\SOFTWARE\Classes\*\shell\pintohome]
"MUIVerb"="Edit with Notepad++"

[HKEY_CURRENT_USER\SOFTWARE\Classes\*\shell\pintohome\command]
@="\"C:\\Program Files\\Notepad++\\notepad++.exe\" \"%1\""
```
(If your installation is not in `c:\Program Files\Notepad++`, you will have to adjust that script.)

**All Users** (requires admin privileges)
```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\*\shell\pintohome]
"MUIVerb"="Edit with Notepad++"

[HKEY_CLASSES_ROOT\*\shell\pintohome\command]
@="\"C:\\Program Files\\Notepad++\\notepad++.exe\" \"%1\""
```
(If your installation is not in `c:\Program Files\Notepad++`, you will have to adjust that script.)

In v8.5, the Notepad++ installer would automatically add this `pintohome` workaround on Windows 11, as long as no other app is currently using the `pintohome` command; if there is already something else in that registry slot, Notepad++ will not overwrite it.  However, since this got rid of the Windows native "pin to home" feature for some Windows 11 users, v8.5.1 undid that change; instead, the installer was updated to add to the main Windows 11 right click, rather than being being relegated to the **Show More Options** sub-menu.

## Notepad++ Cheat sheet

### Tabs

- The tab bar settings can be found at [**Settings > Preferences > General > Tab Bar**](../preferences/#general), including the option to **Hide** the tab bar.

- To switch between first and last tab, use <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + ```MOUSEWHEEL``` on tabs. ```MOUSEWHEEL``` up will take to first tab while down will take to last tab.
  ![tabNavFirstLast](../images/tabNavFirstLast.gif)

- To switch and activate next/previous tab, there are multiple options:
  1. Use <kbd>Ctrl</kbd> + ```MOUSEWHEEL``` on tabs. ```MOUSEWHEEL``` up will take to previous tab while down will take next tab.
  2. Use <kbd>Ctrl</kbd> + <kbd>Page Up</kbd> for next tab and <kbd>Ctrl</kbd> + <kbd>Page Down</kbd> for previous tab.
  3. Use <kbd>Ctrl</kbd> + <kbd>Tab</kbd> for next tab and <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Tab</kbd> for previous tab. Using use <kbd>Ctrl</kbd> + <kbd>Tab</kbd> or <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Tab</kbd> while MRU is enabled provides great user experience. To enable MRU you can follow `Settings->Preferences->MISC.->Document Switcher`, then checkmark both `Enable` and `Enable MRU Behavior`.
  ![tabNavNextPrev](../images/tabNavNextPrev.gif)

- To move tab from one position to other position:
  1. Use <kbd>Shift</kbd> + ```MOUSEWHEEL``` on tabs. ```MOUSEWHEEL``` up will move currently selected tab to previous position while down will move to next position.
  2. Use <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Page Up</kbd> for previous position and <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Page Down</kbd> for next position.
  ![tabNavMoveRtLft](../images/tabNavMoveRtLft.gif)

- To move a tab from one View to the other, you can use the techniques described in the [Editing > Dual View](../editing/#dual-view) section, including:
  1. Use the menus: **View > Move/Clone Current Document > Move to Other View**
  2. Right Click on the tab's title and select **Move to Other View**
  3. Drag the tab's title into the editing pane for that same tab and select **Move to Other View**
  4. If the other View is already visible, drag the tab's title into the editing pane of the other View, and it will move
  ![move2view](../images/move2view.gif)

- To clone a tab from one View into the other, you can use the techniques described in the [Editing > Clone Document](../editing/#dual-view) section, including:
  1. Use the menus: **View > Move/Clone Current Document > Clone to Other View**
  2. Right Click on the tab's title and select **Clone to Other View**
  3. Drag the tab's title into the editing pane for that same tab and select **Clone to Other View**
  ![clonedDoc](../images/clonedDoc.gif)

- To create a new file tab using the tab bar:
  1. If there is empty area to the right of the last tab in the tab bar, double click there and a new tab will be created
  ![tabNavNewDoubleClick](../images/tabNavNewDoubleClick.gif)

- To close a tab using the tab bar:
  1. If **Settings > Preferences > General > Tab Bar > Show close button on each tab** is checked, you can click the red ☒ on that tab to close that tab
  2. If **Settings > Preferences > General > Tab Bar > Double click to close document** is checked, you can double-click the tab's title to close that tab
  ![tabNavCloseXDblClick](../images/tabNavCloseXDblClick.gif)

#### Tab Bar Right Click Menu

When you right click on the title for a tab, you get a context menu for manipulating that tab.

- `Close`: closes this file's tab
- `Close Mutiple Tabs >`:
  - `Close All But This`: Closes all files except this file
  - `Close All to the Left`: Closes all files that are to the right of this file on the tab bar
  - `Close All to the Right`: Closes all files that are to the left of this file on the tab bar
  - `Close All Unchanged`: Closes all files that do not have unsaved changes (leaves only files that have unsaved changes)
- `Save`: Saves the file (disabled/greyed out if there are no unsaved changes)
- `Save As`: Allows you to save the current file under a new name
- `Open Into >`:
  - `Open Containing Folder in Explorer`: Opens this file's folder in the Windows Explorer
  - `Open Containing Folder in cmd`: Opens this file's folder in the `cmd` command prompt
  - `Open Containing Folder as Workspace`: Opens this file's folder as a [Folder as Workspace](../session/#folder-as-workspace)
- `Rename`: Renames this file
- `Move to Recyle Bin`: Deletes the current file (placing it safely in Window's Recycle Bin)
- `Reload`: Reloads this file from disk
- `Print`: Prints this file
- `Read-Only`: Sets this file's Notepad++\-specific read-only flag (see more in the [**Edit** menu description](../editing/#edit-menu))
- `Clear Read-Only Flag`: Clears this file's read-only flag for the Windows OS (see more in the [**Edit** menu description](../editing/#edit-menu))
- `Copy to Clipboard >`
  - `Copy Full File Path`: Copies the full file path (drive, directory, and filename) to the Windows Clipboard
  - `Copy Filename`: Copies just the filename (no drive or directory) to the Windows Clipboard
  - `Copy Current Dir. Path`: Copies the file's directory (drive and directory, but not the  filename) to the Windows Clipboard
- `Move Document >`
  - `Move to Other View`: Moves the tab from one view to the other
  - `Clone to Other View`: Makes a tab for the same file in the other view
  - `Move to New Instance`: Moves the tab from this Notepad++ instance to a newly-created instance (only works on named files that have no unsaved changes)
  - `Open in New Instance`: Makes a tab in a new Notepad++ instance which contains the same file as this tab (only works on named files that have no unsaved changes)
- `Apply Color to Tab >` (new to v8.4.6)
  - `Apply Color #`: Applies the indicated color to the highlight portion of the tab bar.  (Applying a different color will _change_ the color, not combine the colors together.  Each tab can only have one color.)
  - `Remove Color`: Removes the color of the tab, returning to the default color scheme

### Menu Bar

The menu bar of Notepad++ has a variety of menus, including **File** (for generic file operations like open and close), [**Edit**](../editing#edit-menu), [**Search**](../searching/), and [**View**](../views/), **Encoding** (which affects how the bytes of the file are interpreted as text -- whether ANSI or UTF-8 or similar), **Language** (for [syntax highlighting](../programming-languages/)), [**Settings**](../preferences/), **Tools** (with a couple of built-in utilities), [**Macro**](../macros/), [**Run**](../config-files/#userdefinedcommands) (for running external commands), [**Plugins**](../plugins/), and the **Window** menu (for accessing open files already open in Notepad++).

It also contains the **?** menu, which is a **Help**-style menu, including actions that list the [command line arguments](../command-prompt/); actions that take you to the Notepad++ [home page](https://notepad-plus-plus.org/), the [project page](https://github.com/notepad-plus-plus/notepad-plus-plus), this [user manual](/), and the [Community Forum](https://community.notepad-plus-plus.org); actions for the updater and proxy; the **Debug Info** (which is critical information when asking for help at the Community Forum or when creating a feature request or bug report at the [project page](https://github.com/notepad-plus-plus/notepad-plus-plus/issues)) and **About**.

At the far right of the menu bar there are also icons `+` (to create a New file), `▼` (to choose from the open files), and `X` (which closes the active tab).  (Before v8.4.3, only the `X` existed in that area of the menu bar.  Starting in v8.4.5, these can be made hidden using [Settings > Preferences > General > Menu](../preferences/#general).)

### Toolbar

There is a toolbar which has icons for various common tasks.  The toolbar settings can be found at [**Settings > Preferences > General > Toolbar**](../preferences/#general), including the option to **Hide** the toolbar.  If you do not understand the icon, hovering over that icon will show the underlying action.


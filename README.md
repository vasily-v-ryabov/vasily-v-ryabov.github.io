# pywinauto
pywinauto is a GUI automation library written in pure Python. At its simplest
it allows you to send mouse and keyboard actions to dialogs and controls on both
Windows and Linux, while more complex text-based actions are supported on
Windows only so far (Linux AT-SPI support is under development).

## Technologies under the hood
* Win32 API ("win32" backend)
* MS UI Automation ("uia" backend)
* Windows low level hooks (win32_hooks) for callbacks on mouse and keyboard user actions.

## Documentation
* [Short Intro on ReadTheDocs](https://pywinauto.readthedocs.io/en/latest/)
* [**Getting Started Guide**](https://pywinauto.readthedocs.io/en/latest/getting_started.html) (core concept, Spy/Inspect tools etc.)
* [StackOverflow tag](https://stackoverflow.com/questions/tagged/pywinauto) for questions

## Setup
* Just run `pip install --upgrade pywinauto` (Py2.7+, Py3.3+)

## Dependencies
 * [six](https://github.com/benjaminp/six)
 * [pyWin32](https://github.com/mhammond/pywin32) (Windows only)
 * [comtypes](https://github.com/enthought/comtypes) (Windows only)
 * [python-xlib](https://github.com/python-xlib/python-xlib) (Linux only)

## Supported controls
* Standard Win32 controls (through Win32 API): MFC, WTL, VB6 and some other legacy apps, partial support for WinForms
* All standard widgets under MS UI Automation: WinForms, WPF, Qt, all browsers, explorer.exe and more (pywinauto 0.6.0+)

## Simple Example
It is simple and the resulting scripts are very readable. How simple?

```python
from pywinauto.application import Application
app = Application().start("notepad.exe")

app.UntitledNotepad.menu_select("Help->About Notepad")
app.AboutNotepad.OK.click()
app.UntitledNotepad.Edit.type_keys("pywinauto Works!", with_spaces = True)
```

## MS UI Automation Example
More detailed example for `explorer.exe`:

```python
from pywinauto import Desktop, Application

Application().start('explorer.exe "C:\\Program Files"')

# connect to another process spawned by explorer.exe
# Note: make sure the script is running as Administrator!
app = Application(backend="uia").connect(path="explorer.exe", title="Program Files")

app.ProgramFiles.set_focus()
common_files = app.ProgramFiles.ItemsView.get_item('Common Files')
common_files.right_click_input()
app.ContextMenu.Properties.invoke()

# this dialog is open in another process (Desktop object doesn't rely on any process id)
Properties = Desktop(backend='uia').Common_Files_Properties
Properties.print_control_identifiers()
Properties.Cancel.click()
Properties.wait_not('visible') # make sure the dialog is closed
```

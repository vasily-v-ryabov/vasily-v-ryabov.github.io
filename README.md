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

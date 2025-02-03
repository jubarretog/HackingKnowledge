---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Environment Variables

An **environment variable** is a user-definable value that can affect the way running processes will behave on a computer. In Linux, we can check them with the command `env` and identify them because they start with the `$` symbol.

Some of the most common preset environment variables are:

* **`$PATH`:** List of directories for searching executable files or other directories, by default contains directories of system applications and installed apps
* **`$USER`:** The user currently logged in
* **`$PWD`:** Current working directory
* **`$HOME`**: Home Directory path
* **`$$`:** Current shell PID
* **`$SHELL`:** The path to the current shell, determines which command-line interface you are using
* **`$TERM`:** Indicates the type of terminal to emulate when running the shell
* **`$LANG`:** Specifies the language and locale settings for the user environment
* **`$EDITOR`:** The default text editor set for the user
* **`$MAIL`:** The path to the user's mailbox
* **`$DISPLAY`:** Used in graphical environments to specify the display server to connect to
* **`$HISTSIZE`:** Defines the number of commands to remember in the command history for the current user session

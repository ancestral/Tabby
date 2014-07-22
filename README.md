# Tabby
Clean, tab-separated data format

## Introduction
Tabby is a file format for writing configuration and other text data in an easy and clean manner. It is similar to the tab-separated value (TSV) format, but more defined, with a logical flow that allows for arrayed and object data.

## Rules
Tabby files should end with the extension `.tabby` or `.tby`, but `.tsv` is also acceptable. Files may be encoded with any character set, as long as it contains tab and newline characters (carriage returns and/or line feeds).

There are three types of data in a Tabby file: objects, key-value pairs and values.

* **Object** may contain any number of other objects or key-value pairs. Any lines follow starting with an additional tab character. The object continues until a line begins with fewer beginning tab characters than the line of the object’s key.
* **Key-Value Pair** contains a key, followed by a tab character, then a value which can contain any non-newline characters. If the following line contains just a value at the same indentation, it is considered a list of values.
* **Value** may be objects or any number of integers or words, which can consist of any characters except newline characters, tabs and backslash. (Though not defined, `\t` and `\n` are typically representative of tabs and newlines, and `\\` for a single backslash.)

Additionally, a **Key** is any word which may contain any characters except quote, double quote, control characters, whitespace characters and backslashes, except if escaped with a backslash. However, Tabby files should not contain any of these exceptions if possible.

## Example
    menu
        id  file
        value File
        popup
            menuitem
                0
                    value New
                    onclick CreateNewDoc()
                1
                    value Open
                    onclick OpenDoc()
                2
                    value Close
                    onclick CloseDoc()

In JSON, this example would look like this:

    {"menu": {
      "id": "file",
      "value": "File",
      "popup": {
        "menuitem": [
          {"value": "New", "onclick": "CreateNewDoc()"},
          {"value": "Open", "onclick": "OpenDoc()"},
          {"value": "Close", "onclick": "CloseDoc()"}
        ]
      }
    }}

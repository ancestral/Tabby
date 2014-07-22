# Tabby
Clean, tab-separated data format

## Introduction
Tabby is a file format for writing configuration and other text data in an easy and clean manner. It is similar to the tab-separated value (TSV) format, but more defined, with a logical flow that allows for arrayed and object data.

## Rules
Tabby files should end with the extension `.tabby` or `.tby`, but `.tsv` is also acceptable. Files may be encoded with any character set, as long as it contains tab and newline characters (carriage returns and/or line feeds).

There are three types of data in a Tabby file: objects, key-value pairs and values.

* **Object** may contain any number of other objects or key-value pairs.
* **Key-Value Pair* contains a key and values.
* **Value** may be objects or any number of integers or words.

## Example
    menu
      id  file
      value File
      popup
        menuitem
          1
            value New
            onclick CreateNewDoc()
          2
            value Open
            onclick OpenDoc()
          3
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

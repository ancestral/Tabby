# Tabby
Clean, tab-separated data format

## Introduction
Tabby is a file format for writing configuration and other text data in an easy and clean manner. It is similar to the tab-separated value (TSV) format, but more defined, with a logical flow that allows for arrayed and object data. It requires typing fewer additional characters and works well when editing in spreadsheets or tables.

## Rules
Tabby files should end with the extension `.tabby` or `.tby`, but `.tsv` is also acceptable. Files may be encoded with any character set, as long as it contains tab and newline characters (carriage returns and/or line feeds).

### Types
There are three types of data in a Tabby file: objects, key-value pairs and values..

* **Object** may contain any number of other objects or key-value pairs. All objects must have a key. Any lines follow starting with an additional tab character. The object continues until a line begins with fewer beginning tab characters than the line of the object’s key.
* **Key-Value Pair** contains a key, followed by a tab character, then a value or set of values. If the line separates values with tabs, or the following lines contain just a value at the same indentation, it is then considered a list of values.
* **Value** may be objects or any number of integers or words, and any characters except newline characters, tabs, and a single backslash. (Though not defined, `\t` and `\n` are typically representative of tabs and newlines, and `\\` for a single backslash.) Other whitespace is counted.

Additionally, a **Key** is any word which may contain any characters except quote, double quote, control characters, whitespace characters and backslashes, except if escaped with a backslash. However, Tabby files should not contain any of these exceptions if possible.

The root type of the file is an anonymous object. Aside from that, anonymous objects are not allowed. If authors cannot find a suitable key name then they may use integers starting at 0.

### Tabs and spaces
Some coders like using soft tabs, and Tabby supports those too. The first time the file contains a line that starts with one or more spaces, it will define a tab being equal to that number of spaces, for the rest of the document.

* Technically tabs and soft tabs can co-exist in a file, but it should be discouraged in practice.
* If there are extra “remainder” spaces, if they surround a value, these are part of the value.)

## Validation
No tab separated files can be invalid. Even a malformed file will not throw an error, though it may not offer much worth to the developer or user.

## Example
As text (⇥ is a tab character):

    menu
    ⇥id⇥file
    ⇥value⇥File
    ⇥popup
    ⇥⇥menuitem
    ⇥⇥⇥0
    ⇥⇥⇥⇥value⇥New
    ⇥⇥⇥⇥onclick⇥CreateNewDoc()
    ⇥⇥⇥1
    ⇥⇥⇥⇥value⇥Open
    ⇥⇥⇥⇥onclick⇥OpenDoc()
    ⇥⇥⇥2
    ⇥⇥⇥⇥value⇥Close
    ⇥⇥⇥⇥onclick⇥CloseDoc()

In a table:

| menu |       |          |   |         |                |
|------|-------|----------|---|---------|----------------|
|      | id    | file     |   |         |                |
|      | value | File     |   |         |                |
|      | popup |          |   |         |                |
|      |       | menuitem |   |         |                |
|      |       |          | 0 |         |                |
|      |       |          |   | value   | New            |
|      |       |          |   | onclick | CreateNewDoc() |
|      |       |          | 1 |         |                |
|      |       |          |   | value   | Open           |
|      |       |          |   | onclick | OpenDoc()      |
|      |       |          | 2 |         |                |
|      |       |          |   | value   | Close          |
|      |       |          |   | onclick | CloseDoc()     |
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

## Differences compared to JSON
In some ways, Tabby is very similar to JSON. It isn’t too difficult to translate between the two formats, yet there are some significant differences between them.

* Tabby uses no punctuation aside from tab and newline characters when defining values.
* Spaces are not ignored when typed in a value.
* All values should be considered a part of an array, and if only one value exists, should be treated as if no array exists.

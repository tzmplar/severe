# File System

## dofile
### Definition
```lua
function dofile(path: string): (... any)
```
### Returns
```horizontal
### (... any)
```
### Description
Effectively `loadstring(readfile(path))()`. Loads and executes a Lua file, returning any values the file returns.

---

## loadfile
### Definition
```lua
function loadfile(path: string): (... any)
```
### Returns
```horizontal
### (... any)
```
### Description
Loads a Lua file and returns it as a function. Call the returned function to execute the file's code.

---

## writefile
### Definition
```lua
function writefile(path: string, content: string): ()
```
### Description
Overrides/creates a file at `path` with specified content.

---

## isfile
### Definition
```lua
function isfile(path: string): boolean
```
### Returns
```horizontal
### boolean
```
### Description
Validates the existence of a file at `path`, returns a boolean.

---

## isfolder
### Definition
```lua
function isfolder(path: string): boolean
```
### Returns
```horizontal
### boolean
```
### Description
Validates the existence of a folder at `path`, returns a boolean.

---

## readfile
### Definition
```lua
function readfile(path: string): string
```
### Returns
```horizontal
### string
```
### Description
Returns the contents of a file at `path` as a string.

---

## listfiles
### Definition
```lua
function listfiles(path: string): { string }
```
### Returns
```horizontal
### { string }
```
### Description
Returns an array of all files and folders at `path`.

---

## makefolder
### Definition
```lua
function makefolder(path: string): ()
```
### Description
Creates a new folder at `path`.

---

## delfolder
### Definition
```lua
function delfolder(path: string): ()
```
### Description
Removes the folder located at `path`.

---

> **Note:** All file operations are sandboxed to `C:\v2\workspace`. Attempting to read/write/load outside this directory is impossible.
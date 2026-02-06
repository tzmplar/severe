# File System

## dofile

### Definition

```luau
function dofile(path: string): (... any)
```

### Returns

<table data-header-hidden data-full-width="false"><thead><tr><th valign="middle">Type</th></tr></thead><tbody><tr><td valign="middle"><pre class="language-luau"><code class="lang-luau">(... any)
</code></pre></td></tr></tbody></table>

### Description

Effectively `loadstring(readfile(path))()`. Loads and executes a luau file, returning any values the file returns.

***

## loadfile

### Definition

```luau
function loadfile(path: string): (... any)
```

### Returns

<table data-header-hidden data-full-width="false"><thead><tr><th valign="middle">Type</th></tr></thead><tbody><tr><td valign="middle"><pre class="language-luau"><code class="lang-luau">(... any)
</code></pre></td></tr></tbody></table>

### Description

Loads a luau file and returns it as a function. Call the returned function to execute the file's code.

***

## writefile

### Definition

```luau
function writefile(path: string, content: string): ()
```

### Description

Overrides/creates a file at `path` with specified content.

***

## isfile

### Definition

```luau
function isfile(path: string): boolean
```

### Returns

<table data-header-hidden data-full-width="false"><thead><tr><th valign="middle">Type</th></tr></thead><tbody><tr><td valign="middle"><pre class="language-luau"><code class="lang-luau">boolean
</code></pre></td></tr></tbody></table>

### Description

Validates the existence of a file at `path`, returns a boolean.

***

## isfolder

### Definition

```luau
function isfolder(path: string): boolean
```

### Returns

<table data-header-hidden data-full-width="false"><thead><tr><th valign="middle">Type</th></tr></thead><tbody><tr><td valign="middle"><pre class="language-luau"><code class="lang-luau">boolean
</code></pre></td></tr></tbody></table>

### Description

Validates the existence of a folder at `path`, returns a boolean.

***

## readfile

### Definition

```luau
function readfile(path: string): string
```

### Returns

<table data-header-hidden data-full-width="false"><thead><tr><th valign="middle">Type</th></tr></thead><tbody><tr><td valign="middle"><pre class="language-luau"><code class="lang-luau">string
</code></pre></td></tr></tbody></table>

### Description

Returns the contents of a file at `path` as a string.

***

## listfiles

### Definition

```luau
function listfiles(path: string): { string }
```

### Returns

<table data-header-hidden data-full-width="false"><thead><tr><th valign="middle">Type</th></tr></thead><tbody><tr><td valign="middle"><pre class="language-luau"><code class="lang-luau">{ string }
</code></pre></td></tr></tbody></table>

### Description

Returns an array of all files and folders at `path`.

***

## makefolder

### Definition

```luau
function makefolder(path: string): ()
```

### Description

Creates a new folder at `path`.

***

## delfolder

### Definition

```luau
function delfolder(path: string): ()
```

### Description

Removes the folder located at `path`.

***

> **Note:** All file operations are sandboxed to `C:\v2\workspace`. Attempting to read/write/load outside this directory is impossible.

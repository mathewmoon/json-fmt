# json-lint-tools
Provides linting, diffing and formatting JSON. Diffing and linting is done by comparing an input (file or stdin) to what would be produced by
loading the string with `json.load(data)` then dumping it again with `json.dumps(data)` with options to order keys, order items in arrays, and
specify the expected indentation. The CLI tool can optionally update the original file with the pretty formatted JSON output.


## This package is primarily intended as a CLI tool for linting and formatting JSON. Thereis however documentation for the API [HERE](https://mathewmoon.github.io/json-lint-tools/)


## Installation
```shell
pip install json-lint-tools
```


## CLI Usage
```
usage: jsonfmt [-h] [--check] [-d] [-f] [-i INDENT] [--no-color] [-r] [-s] [--sort-arrays] [--sort-keys] [--stdin] [path ...]

positional arguments:
  path                  Path to a single file or directory of JSON files

options:
  -h, --help            show this help message and exit
  --check               Only check if the files would be changed. Show a list of any files that would be changed and exit with an error if any would be
  -d, --diff            Show a diff
  -f, --format          Format non-conforming files
  -i INDENT, --indent INDENT
                        How many spaces are expected per indentation
  --no-color            Don't print colors to stdout
  -r, --recursive       Search recursively for JSON files
  -s, --sort            Sort all objects by key and all arrays alphabetically. Shorthand for --sort-keys + --sort-arrays
  --sort-arrays         Sort arrays alphabetically
  --sort-keys           Sort keys in JSON objects alphabetically
  --stdin               Read data from stdin instead of a file
```

## Examples
Getting a pretty diff:
```shell
> jsonfmt -r -d tests/jsonfiles                                                                                                                                                                             File: tests/jsonfiles/test.json
---
+++
@@ -6,9 +6,9 @@
   ],
   "baz": {
     "myarry": [
-        "b",
-        "d",
-        "a"
+      "b",
+      "d",
+      "a"
     ]
   }
 }
File: tests/jsonfiles/root_array.json
---
+++
@@ -1 +1,8 @@
-["a", "d", "b", {"foo": "bar"}]
+[
+  "a",
+  "d",
+  "b",
+  {
+    "foo": "bar"
+  }
+]
File: tests/jsonfiles/one_line_obj.json
---
+++
@@ -1 +1,4 @@
-{"foo": "bar", "bar": "baz"}
+{
+  "foo": "bar",
+  "bar": "baz"
+}

```

Formatting stdin:

```shell
> echo '{"foo": "bar"}' | jsonfmt
{
  "foo": "bar"
}
```
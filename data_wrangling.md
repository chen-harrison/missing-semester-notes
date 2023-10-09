### Regular Expressions (Regex)

- `sed`: stream editor, best for search and replace and not much else
    - `COMMAND | sed "s/SEARCH_STRING/SUBSTITUTION_STRING/"` replaces regex-defined string subsitute in output
- Both `sed` and `grep` search strings can use regular expressions, aka regex, to capture text that follows certain patterns
    - Use `sed -E` option for normal regex syntax
- Characters
    - `\d` = digit (0-9)
    - `\D` = non-digit
    - `\w` = alphanumeric
    - `\W` = non-alphanumeric
    - `.` = any character
    - `\s` = any whitespace
    - `\S` = non-whitespace
    - `\` = escapes special char (`.`, `*`, `[`, etc.)
- Other
    - `^...$` = line start and end
    - `()` = capture group, content can be referred via `\1`, `\2`, `\3`, etc. in sequential order
- Character classes
    - `[abc]` = a, b, or c
    - `[123]` = 1, 2, or 3
    - `[^abc]` = NOT a, b, or c
    - `[a-z]`, `[0-9]` = as expected
- Quantifiers
    - `*` = 0 or more times
    - `+` = 1 or more times
    - `?` = 0 or 1 times
    - `{NUM}` = `NUM` times
    - `{LOW,HIGH}` = `LOW` to `HIGH` times
- More: https://www.rexegg.com/regex-quickstart.html
- Tutorial: https://regexone.com/

### More Tools

- `sort` = take file content/input stream and sort it
- `uniq` = remove redundant lines, but only if adjacent, so pipe in from `sort` = add `-c` to include counts
- `head`, `tail` = use with `-n NUM` to see the first/last `NUM` lines
- `awk` = print the `NUM`th column on each line with `awk {print $NUM}`
    - More functionality like `sed`, rather complex though
- `paste` = combines file content/input
- `bc` = command-line calculator, used like `echo "OPERATION" | bc -l`
- `xargs` = takes a list of inputs and turns them into arguments, i.e. `ARGS_SOURCE | xargs COMMAND`
- For specific use cases, remember to refer to documentation via `man`, `--help`, or `tldr`
- `jq` = JSON parser
- `pup` = HTML parser
- `pandas` = Python library
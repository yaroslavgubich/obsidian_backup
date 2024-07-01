#regex #cheatsheet

Certainly, here's a regex cheat sheet formatted as a code snippet for easier reference:

```regex
# Basic Matchers
.           # Matches any single character except newline
^           # Matches the start of a string
$           # Matches the end of a string
[abc]       # Matches any one character in the brackets
[^abc]      # Matches any one character not in the brackets

# Quantifiers
a*          # Matches 0 or more occurrences of 'a'
a+          # Matches 1 or more occurrences of 'a'
a?          # Matches 0 or 1 occurrence of 'a'
a{3}        # Matches exactly 3 consecutive occurrences of 'a'
a{3,}       # Matches 3 or more consecutive occurrences of 'a'
a{3,6}      # Matches between 3 and 6 occurrences of 'a'

# Character Classes
\d          # Matches any digit, equivalent to [0-9]
\D          # Matches any non-digit, equivalent to [^0-9]
\w          # Matches any word character (alphanumeric or _), equivalent to [a-zA-Z0-9_]
\W          # Matches any non-word character, equivalent to [^a-zA-Z0-9_]
\s          # Matches any whitespace character (spaces, tabs, line breaks)
\S          # Matches any non-whitespace character

# Anchors and Boundaries
\b          # Matches a word boundary (position between a word and a non-word character)
\B          # Matches a position that is not a word boundary

# Grouping and Capturing
(a|b)       # Matches either 'a' or 'b'
(a)         # Groups 'a' and captures the match

# Escaping Special Characters
\           # Used to escape special characters, turning them into literals, e.g., \. matches a period

# Lookahead and Lookbehind (Advanced)
(?=foo)     # Positive lookahead, matches a position preceding 'foo'
(?!foo)     # Negative lookahead, matches a position not preceding 'foo'
(?<=foo)    # Positive lookbehind, matches a position following 'foo'
(?<!foo)    # Negative lookbehind, matches a position not following 'foo'
```

This cheat sheet covers the basics and some advanced concepts in regular expressions. Remember, regex syntax and support might vary slightly between different programming languages and environments, so it's always a good idea to check the specific documentation for the language you're working with.

Adding more details to the regex cheat sheet to cover additional patterns and concepts:

```regex
# More Quantifiers
.*          # Matches any character (except newline) 0 or more times (greedy match)
.*?         # Matches any character (except newline) 0 or more times (lazy match)

# POSIX Character Classes (use within [])
[:digit:]   # Matches any digit, equivalent to \d
[:word:]    # Matches any word character, equivalent to \w
[:space:]   # Matches any whitespace character, equivalent to \s
[:alpha:]   # Matches any alphabetic character
[:alnum:]   # Matches any alphanumeric character
[:lower:]   # Matches any lowercase letter
[:upper:]   # Matches any uppercase letter

# Non-Capturing Groups and Modifiers
(?:a|b)     # Non-capturing group, matches either 'a' or 'b' but does not capture the match
(?i)        # Case-insensitive match (modifier can be applied to entire pattern or subpattern)
(?m)        # Multiline mode: '^' and '$' match start and end of a line, not just start and end of string

# Named Capture Groups (Syntax varies by language)
(?<name>a)  # Named capture group 'name' matches 'a' (syntax in Ruby, .NET, Java, etc.)
(?'name'a)  # Alternative syntax for named capture groups (syntax in .NET)

# Assertions (Advanced Lookaround)
(?=foo)     # Positive lookahead, asserts that what immediately follows the current position is 'foo'
(?!foo)     # Negative lookahead, asserts that what immediately follows the current position is not 'foo'
(?<=foo)    # Positive lookbehind, asserts that what immediately precedes the current position is 'foo'
(?<!foo)    # Negative lookbehind, asserts that what immediately precedes the current position is not 'foo'

# Atomic Groups (Advanced, prevents backtracking)
(?>a+)      # Atomic group, matches 1 or more 'a's without allowing backtracking

# Conditional Expressions (Syntax varies by language)
(?(condition)then|else) # Matches 'then' if 'condition' is true, otherwise matches 'else'

# Comments (Syntax varies by language)
(?#comment) # Inline comment (not supported in all regex flavors)

# Flags / Modifiers
i           # Case-insensitive match
m           # Multiline mode: '^' and '$' match start and end of each line (not only start and end of string)
s           # Single line mode: '.' matches newline characters as well
x           # Free-spacing mode: whitespace is ignored, and '#' starts a comment until the end of the line

# Greedy vs. Lazy (Reluctant) Quantifiers
a*          # Greedy quantifier, matches as many 'a's as possible
a*?         # Lazy (reluctant) quantifier, matches as few 'a's as possible to allow the overall match to succeed

# Backreferences (for capturing groups)
\1          # Matches the same text as previously matched by the first capturing group
\2          # Matches the same text as previously matched by the second capturing group

```

This expanded cheat sheet includes a broader range of regular expression features, including advanced constructs like lookarounds, atomic groups, and conditional expressions, along with explanations for POSIX character classes, non-capturing groups, named capture groups, and more about greedy vs. lazy quantifiers. 

Keep in mind that not all features are supported in every regex engine, so it's essential to consult the documentation for the specific language or tool you're using.
## Indentation

#### Line Length

Each level of indentation uses 4 spaces. All lines are less than 80 characters long. Lines longer than 79 characters that do not already contain parentheses can be wrapped within parentheses and broken into smaller lines.

#### Alignment

Continuous lines that are wrapped in parentheses align within those parentheses:

    def my_function(var1, var2, var3, var4, var5,
                    var6, var7, var8, var9, var10):
        print(something)

As the text `if (` is already 4 characters long, extended "if" conditions are indented a further 4 spaces to distinguish them from following lines:

    if (condition1 and condition2 and condition3
            and condition4 and condition 5):
        print(something)

#### Binary Operators

Binary operators on multiple lines appear at the start of the line:

    total = (var1 + var2 + var3 + var4
             + var5 + var6 + var 7
             + var8 + var 9 + var 10)

## Blank Lines

Top-level (non-indented) function/class definitions are surrounded by two blank lines on each side. Method definitions are surrounded by one blank line on each side:

    def my_function(var1):
        print(something)
    
    
    class MyClass:
        var1 = "Hello"

        def my_method(var2):
            print(something)

        def my_other_method(var3):
            print(something)

Blank lines may also be used sparingly to indicate logical sections and to group related functions.

## Quotes

Double quotes are used for strings. If the string contains double quotes, single quotes are used instead:

    string1 = "String 1"
    string2 = 'The string "String 1" is contained in string1'

## Whitespace

A space character is used after but not before commas, and should not precede a closing bracket:

    my_function(var1, var2)

#### Binary Operators

Binary operators are surrounded by a space in most cases.

All assignment, comparison and Boolean operators are surrounded by a space:

    var1 = 1
    if (var1 <= 5 and var1 != 3):

If a sequence of binary operators with different priorities appear on the same line, spaces surrounding higher-priority operators may be omitted to improve readability:

    var1 = var2*var3 + var4*var5

##Comments

Comments are complete sentences starting with a capital letter. Full-stops are used when a comment consists of multiple sentences. Each comment or line of a comment starts with a # followed by a single space.

#### Block Comments

Block comments describe/apply to most or all of the code that follows them, and are indented to the same level as that code. Paragraphs are separated by a # and a space:

    # This is
    # a block.
    # 
    # It consists of
    # two paragraphs.

#### Inline Comments

Inline comments are used sparingly, and only to explain something that is not immediately obvious. They should be separated from the preceding line of code with no less than 2 spaces:

    var1 += 5  # Add a buffer

## Naming Conventions

Names should be concise and descriptive. Shorter and less descriptive names are acceptable if their purpose can be understood from context (such as using "i" or "j" as incrementers).

Functions and variable names are in lowercase with underscores_separating_words, though they may be omitted to improve readability:

    total_velocity = v1 + v2

Class names are in UpperCamelCase.

Constants are in UPPERCASE with UNDERSCORES_SEPARATING_WORDS.


---
layout: default
title: Code layout and indenting
meta: Put extra info here, like if there any subjects required for this subject
todo: Variable naming, more examples of complete files, curly brace position
---
{% include licence.md %}

### Code indentation

Note that the commands in the block following the if statement (i.e. the lines after the curly brace, { ) are not written at the same level as the if statement itself. They should be **indented** slightly to the right. Indentation happens when you press the tab key, which is located to the left of q key. When the block ends with the closing curly brace, indentation ends as well. The closing curly brace } should be on the same level as the original `if` statement.

The use of indentation is crucial for the readability of program code. During this course and generally everywhere, you are expected to indent the code properly. IntelliJ helps with the correct indentation. You can easily indent your program by pressing ctrl, alt, and L simultaneously. It's also possible to select a whole section of code, and press tab to indent this whole section

{% include_relative exercises/001.md %}
{% include_relative exercises/002.md %}
{% include_relative exercises/003.md %}
{: .exercises }

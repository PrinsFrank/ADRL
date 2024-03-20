# ADRL
Syntax for "A Deductive Reasoning Language"

## Syntax v0.1

This specification uses the Augmented Backs-Naur Form (ABNF)

```text
statement           = identity
                    / modifier

identity            = premise
                    / conclusion

modifier            = argument
                    / soundness
                    / validity

premise             = "premise" section_separator identifier section_separator label

conclusion          = "conclusion" section_separator identifier section_separator label

argument            = "argument" 2*(section_seperator identifier)

soundness           = "sound" section_separator identifier
                    / "unsound" section_seperator identifier

validity            = "valid" section_separator identifier
                    / "invalid" section_separator identifier

identifier          = local_identifier
                    / relative_identifier
                    / absolute_identifier

local_identifier    = 2*char

relative_identifier = 2*(char / path_separator)

absolute_identifier = **TODO**

char                = ALPHA 
                    / DIGIT
                    / word_separator

path_separator      = "/"

word_separator      = "_"

section_separator   = " "
```

# ADRL
A Deductive Reasoning Language

## Syntax

```text
statement           = definition
                    / premise
                    / validity
                    / conclusion
                    / soundness

definition          = keyword_definition section_separator identifier

premise             = keyword_premise section_separator identifier

validity            = keyword_premise identifier (keyword_sound / keyword_unsound)

conclusion          = keyword_conclusion section_separator identifier

soundness           = keyword_conclusion identifier (keyword_valid / keyword_invalid)

identifier          = local_identifier
                    / relative_identifier
                    / absolute_identifier

local_identifier    = 2*char

relative_identifier = 2*(char / path_separator)

absolute_identifier =

char                = ALPHA 
                    / DIGIT
                    / word_separator

path_separator      = "/"

word_separator      = "_"

section_separator   = " "

keyword_definition  = "DEFINITION"

keyword_premise     = "PREMISE"

keyword_conclusion  = "CONCLUSION"

keyword_sound       = "SOUND"

keyword_unsound     = "UNSOUND"

keyword_valid       = "VALID"

keyword_invalid     = "INVALID"
```

This specification uses the Augmented Backs-Naur Form (ABNF)
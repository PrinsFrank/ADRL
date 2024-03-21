# ADRL
Syntax for "A Deductive Reasoning Language"

## Syntax

This specification uses the Augmented Backs-Naur Form (ABNF)

```text
statement           = identity
                    / modifier

identity            = premise
                    / conclusion

modifier            = argument
                    / soundness
                    / validity

premise             = "premise" SP identifier SP label

conclusion          = "conclusion" SP identifier SP label

argument            = "argument" 2*(SP identifier)

soundness           = "sound" SP identifier
                    / "unsound" SP identifier

validity            = "valid" SP identifier
                    / "invalid" SP identifier

identifier          = local-identifier
                    / relative-identifier
                    / absolute-identifier

local-identifier    = 2*char

relative-identifier = 2*(char / path-separator)

absolute-identifier = **TODO**

char                = ALPHA 
                    / DIGIT
                    / word-separator

path-separator      = "/"

word-separator      = "_"
```

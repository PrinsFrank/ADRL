# ADRL
Syntax for "A Deductive Reasoning Language"

## Syntax

This specification uses the Augmented Backus-Naur Form (ABNF)

```abnf
statement           = identity
                    / modifier

identity            = premise
                    / conclusion

modifier            = trueness
                    / validity

premise             = "premise" SP identifier [SP label]

conclusion          = "conclusion" 2*(SP identifier)  [SP label]

trueness            = "true" SP identifier [SP label]
                    / "false" SP identifier [SP label]

validity            = "valid" SP identifier [SP label]
                    / "invalid" SP identifier [SP label]

identifier          = local-identifier
                    / relative-identifier
                    / absolute-identifier

local-identifier    = 2*char

relative-identifier = 2*(char / path-separator)

absolute-identifier = **TODO**

label               = DQUOTE *(char / SP) DQUOTE

char                = ALPHA 
                    / DIGIT
                    / word-separator

path-separator      = "/"

word-separator      = "_"
```

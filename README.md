# ADRL

## 1.0 What is ADRL?

### 1.1 Introduction

ADRL stands for "A Deductive Reasoning Language". It tries to solve the problem of communicating large logic trees and deep arguments. As some conclusions may have large logic trees, included in this standard is a way to reference local identifiers, but also relative and absolute identifiers. This allows for collaborators to work on their own reasoning files, and to either build on existing logic trees or to (dis)prove conlusions and premises in a distributed fashion.

ADRL files are identified by their file extension: `.adrl` This standard is currently agnostic about the way these files are distributed. This might change in a future specification version. 

### 1.1 Objectives

When talking about complex problems, it sometimes becomes quite difficult to keep track of what arguments rely on what conclusions, and what underlying premises cause an argument to suddenly not be true anymore. For this reason, one of the objectives of this specification is that the files should be readable by - and structured for parsers, compared to natural languages which are hard to parse and may be parsed in the wrong way if the wording of an argument does allow for parsing.

Some reasoning sets may be fundamental for others. Therefor, it should be possible to build upon other reasoning sets. It should also be possible to invalidate other arguments or rely on a partially different set of premises. Some reasoning sets should be able to be reused across users, so besides local and relative identifiers the specification also allows for absolute identifiers.

## 2.0 Terminology

### 2.1 Identifier

### 2.1 Premise

### 2.1 Conclusion

## ABNF Syntax

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

absolute-identifier = "https://" host [":" port] "/" relative-identifier

label               = DQUOTE *(char / SP) DQUOTE

char                = ALPHA 
                    / DIGIT
                    / word-separator

host                = 1*alpha ["." host]

port                = 1*DIGIT

path-separator      = "/"

word-separator      = "_"
```

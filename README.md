# ADRL

## 1.0 What is ADRL?

### 1.1 Introduction

ADRL stands for "A Deductive Reasoning Language". It tries to solve the problem of communicating large logic trees and deep arguments. As some conclusions may have large logic trees, included in this standard is a way to reference local identifiers, but also relative and absolute identifiers. This allows collaborators to work on their own reasoning files, and to either build on existing logic trees or to (dis)prove conclusions and premises in a distributed fashion.

ADRL files are identified by their file extension: `.adrl` This standard is currently agnostic about the way these files are distributed. This might change in a future specification version. 

### 1.1 Objectives

When talking about complex problems, it sometimes becomes quite difficult to keep track of what arguments rely on what conclusions, and what underlying premises cause an argument to suddenly not be true anymore. For this reason, one of the objectives of this specification is that the files should be readable by - and structured for parsers, compared to natural languages which are hard to parse and may be parsed in the wrong way if the wording of an argument does allow for parsing.

Some reasoning sets may be fundamental for others. Therefore, it should be possible to build upon other reasoning sets. It should also be possible to invalidate other arguments or rely on a partially different set of premises. Some reasoning sets should be able to be reused across users, so besides local and relative identifiers the specification also allows for absolute identifiers.

## 2.0 Terminology

### 2.1 Identifier

An identifier is a unique alphanumeric string that can be used to reference a specific identity. Currently, an identity is either a premise or a conclusion, but more identity types may be added later on. 

Identifiers have to be unique in a file, and valid parsers should throw an error when encountering multiple definitions for the same identifier within a file. It is allowed to have multiple modifiers for one identifier.

When an identity is referenced through a relative or absolute identifier, the identifier will still be unique.

### 2.2 Premise

A premise is a declarative statement that can either be true or false. Consider the following argument:

> Because all humans are mortal, and Socrates is a Human, Socrates is mortal.

This argument contains two premises: "all humans are mortal", and "Socrates is a human".

### 2.3 Conclusion

A conclusion describes a statement that is logically true when all of its premises are true. In the above example, the argument contains the conclusion "Socrates is mortal" based on the two premises. 

### 2.4 Trueness of Premises

Premises can be either true or false. This is considered "trueness" in this specification.

### 2.5 Validity of Conclusions

If a conclusion is not valid, it can be marked as such. To allow for distributed arguments, it's also possible to mark a conclusion as valid.

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

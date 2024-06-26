# rust-specification
This repository is part of my thesis titled "Processes and Considerations for Non-Standardized Languages in Functional Safety" at the University of Amsterdam.

In this repository, I present a language specification for selected features of Rust, demonstrating best practices for a compiler qualification process. This specification draws inspiration from the [Ferrocene](https://github.com/ferrocene/specification) language specification and the [Rust Reference](https://github.com/rust-lang/reference), but it includes additional information that were considered important. It also incorporates some fixes that have been merged into the Ferrocene and Rust Reference repositories.

The following features are specified:

- /spec
  - /types
    - bool
    - union
  - /expressions
    - /operator expressions
      - bitwise expressions
      - comparison expressions
      - lazy boolean expressions
    - field access expressions
    - struct expressions
   

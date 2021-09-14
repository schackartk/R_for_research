# R Data Structure

This section will go over some R data structures and how to work with
them.

## Types

R utilizes several data types. While R is pretty relaxed with types,
this can cause some issues, so it is important to be aware of them.
However, I will only cover some of the basics here (and in a simplified
manner).

### Character

Characters are both singular characters or strings of characters, such
as

    a_letter <- "A"
    a_string <- "A string"

    typeof(a_letter)

    ## [1] "character"

    typeof(a_string)

    ## [1] "character"

Lists which have elements of a certain type inherit that type

    list_of_strings <- c("A", "list", "of", "strings")

    typeof(list_of_strings)

    ## [1] "character"

#### Factors

An interesting spin-off of the character or string is a `factor`.
Factors are used to represent the various levels of a categorical
variable. Because of this, factor *levels* are unique (not repeated).

    some_factors <- as.factor(c('bacteria', 'bacteria', 'virus', 'fungus', 'virus'))
                              
    some_factors

    ## [1] bacteria bacteria virus    fungus   virus   
    ## Levels: bacteria fungus virus

### Numbers

When storing a numerical value, its type defaults to a double. Numbers
without a decimal value can also be stored as an integer.

    a_number <- 1.5

    typeof(a_number)

    ## [1] "double"

    another_number <- 1

    typeof(another_number)

    ## [1] "double"

    an_integer <- integer(1)

    typeof(an_integer)

    ## [1] "integer"

### Logical

Boolean values are either TRUE or FALSE. These are integral to logic
statements, which is why they are the *logical* type in R.

    a_true <- TRUE

    typeof(a_true)

    ## [1] "logical"

    a_false <- FALSE

    typeof(a_false)

    ## [1] "logical"

They can also be represented using the shorthand T or F

    a_true <- T

    typeof(a_true)

    ## [1] "logical"

    a_false <- F

    typeof(a_false)

    ## [1] "logical"

## Structures

R would be useless if there weren’t powerful ways of organizing and
storing data.

### Lists

The most basic structure is the list. Lists can store elements of any
data type.

    string_list <- list("Legolas", "Gimli", "Sauron")
    str(string_list) # str can be used to get a more readable summary

    ## List of 3
    ##  $ : chr "Legolas"
    ##  $ : chr "Gimli"
    ##  $ : chr "Sauron"

    typeof(string_list)

    ## [1] "list"

    number_list <- list(1, 6, 12)
    str(number_list)

    ## List of 3
    ##  $ : num 1
    ##  $ : num 6
    ##  $ : num 12

    typeof(number_list)

    ## [1] "list"

    bool_list <- list(F, T, F)
    str(bool_list)

    ## List of 3
    ##  $ : logi FALSE
    ##  $ : logi TRUE
    ##  $ : logi FALSE

    typeof(bool_list)

    ## [1] "list"

You can even have a list of lists.

    list_list <- list(list(1, 2), list("a", "b"))

    str(list_list)

    ## List of 2
    ##  $ :List of 2
    ##   ..$ : num 1
    ##   ..$ : num 2
    ##  $ :List of 2
    ##   ..$ : chr "a"
    ##   ..$ : chr "b"

    typeof(list_list)

    ## [1] "list"

#### Vectors

A special type of list is a vector, which can be defined with the `c()`
shorthand.

Vectors inherit the type of their elements.

    number_vector <- c(2, 1, 4)
    typeof(number_vector)

    ## [1] "double"

    string_vector <- c("foo", "bar", "baz", "quux")
    typeof(string_vector)

    ## [1] "character"

    bool_vector <- c(T, F, F)
    typeof(bool_vector)

    ## [1] "logical"

Lists can have elements of different types. Vectors will coerce elements
to a consistent type.

    coerced_list <- c(1, F, "foo")

    str(coerced_list)

    ##  chr [1:3] "1" "FALSE" "foo"

    typeof(coerced_list)

    ## [1] "character"

    mixed_list <- list(1, F, "foo")

    str(mixed_list)

    ## List of 3
    ##  $ : num 1
    ##  $ : logi FALSE
    ##  $ : chr "foo"

    typeof(mixed_list)

    ## [1] "list"

### Dataframe

Lists are great, but for data analysis, we need something bigger and
better. This is the dataframe. A dataframe can be thought of kind of as
a table or a spreadsheet.

    a_df <- data.frame(plant = c("pingicula", "drosera",
                             "dionaea", "drosera", "dionaea"),
                       length = c(66, 82, 73, 49, 65),
                       cool = c(F, T, T, T, T)
                       )

    a_df

    ##       plant length  cool
    ## 1 pingicula     66 FALSE
    ## 2   drosera     82  TRUE
    ## 3   dionaea     73  TRUE
    ## 4   drosera     49  TRUE
    ## 5   dionaea     65  TRUE

## Accessing Data

### Lists

List and vector elements are accessed using square brackets `[]` In the
square bracket, you place the *index* to retrieve. Unlike in most
programming languages, indices start at 1 instead of 0, which would be
convenient if it didn’t feel so awkward coming from other languages!

    string_vector

    ## [1] "foo"  "bar"  "baz"  "quux"

    string_vector[1]

    ## [1] "foo"

List slices can also be accessed by using the notation `[start:end]`.
Again, unlike in many other languages, the range is inclusive (the value
at the end index is returned).

    string_vector[1:2] # First through second elements

    ## [1] "foo" "bar"

In order to exclude instead of retrieve certain elements of a list, you
can place a negative index value.

    string_vector[-3] # All elements but the third

    ## [1] "foo"  "bar"  "quux"

Additionally, a vector of boolean values can be used to retrieve certain
elements. In this case, it is best that the boolean vector has the same
length as the list.

Indices where there is True value are returned, indices with a False
value are not.

    string_vector[c(T, F, F, T)]

    ## [1] "foo"  "quux"

When using boolean vectors that are not the same length as the list, you
have to be careful because the list is “recycled” without any warning.

    string_vector[c(T, F)] # Returns every other list element

    ## [1] "foo" "baz"

The fact that you can access list elements with boolean vectors is
really useful. For instance, you can build a vector based on a
conditional, then use that to subset the list.

    # Create vector of booleans
    # The value will be True when the string_vector element is not "bar
    string_vector != "bar"

    ## [1]  TRUE FALSE  TRUE  TRUE

    # I read the following as string_vector where string_vector is not equal to "bar"
    string_vector[string_vector != "bar"]

    ## [1] "foo"  "baz"  "quux"

### Dataframes

Data frame parts can also be accessed using `[]` notation, but row and
column indices are specified as `[row, column]`. All list subsetting
rules described above apply to rows and columns, because each row and
column can be thought of as a list.

    a_df

    ##       plant length  cool
    ## 1 pingicula     66 FALSE
    ## 2   drosera     82  TRUE
    ## 3   dionaea     73  TRUE
    ## 4   drosera     49  TRUE
    ## 5   dionaea     65  TRUE

    # Access a single value
    a_df[4, 1] # Row 4, column 1

    ## [1] "drosera"

    # Access a whole row
    a_df[4, ]

    ##     plant length cool
    ## 4 drosera     49 TRUE

    # Access a whole column
    a_df[ , 3]

    ## [1] FALSE  TRUE  TRUE  TRUE  TRUE

Columns can also be accessed using strings as indices. A certain type of
list, *named list*, can also be accessed this way.

    a_df["length"]

    ##   length
    ## 1     66
    ## 2     82
    ## 3     73
    ## 4     49
    ## 5     65

A simplified notation for this is also available, but note that the
returned type is a vector.

    a_df$length

    ## [1] 66 82 73 49 65

    typeof(a_df["length"])

    ## [1] "list"

    typeof(a_df$length)

    ## [1] "double"

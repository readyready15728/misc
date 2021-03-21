# Pharo Notes
## Notes on the modern Smalltalk variant Pharo

* One-line code examples can be executed using shortcuts without selecting
  them. Multi-line examples must be selected first.
* `==` tests only for object equality (like in Java). More likely the user
  wants `=`.
* "Literal arrays are created at parse time and are read-only" (but copies are
  mutable—presumably the `isReadOnlyObject` primitive code handles this detail).
* Use dynamic arrays for instances like this one: `{ (2 + 3) . (6 \* 6) }`.
* Pharo works with the system clipboard. How's that for Smalltalk playing
  along nice with the host system? :)
* Use `&` for logical "and" and `|` for logical "or". Logical "not" is a unary
  message of the same name.
* Sending the binary message `@` to a number type along with another number
  type to create a `Point` object.
* PolyMath implements complex number arithmetic!
* `Date today + 3 weeks` and `Date yesterday < Date today` both work, very
  nice.
* `4 between: 0 and: 10` and `1 max: 3` are good examples of keyword messages.
* Keyword messages can be written across multiple lines. (And it looks like
  this applies to other messages as well.)
* `ProfStef perform: #next` is the same as `ProfStef next`.
* Remember "unary > binary > keyword", "left to right". There is no algebraic
  order of operations. All exceptions to the rules need to be implemented with
  parentheses.
* These are the same:

    ```pharo
    Transcript show: 'hello'.
    Transcript show: 'Pharo'.
    Transcript cr.
    ```
    
    and (uses the cascade operator):

    ```pharo
    Transcript 
	    show: 'hello';
	    show: 'Pharo' ;
	    cr.
    ```
* Examples of block invocation:

    ```pharo
    [:x | x + 2] value: 5.

    [GTPlayground open] value.

    [:x | x + 2] value: 10.

    [:x :y| x + y] value: 3 value: 5.
    ```
* Pharo blocks have lexical closure.
* Example of an "if" statement:

    ```pharo
    1 < 2
      ifTrue: [100]
      ifFalse: [42].
    ```

    It's just sending `ifTrue:ifFalse` to a Boolean type!
* Examples of loops:

    ```pharo
    1 to: 100 by: 3 do: [:i | Transcript show: i asString; cr].
    
    100 to: 0 by: -2 do: [:i | Transcript show: i asString; cr].
    
    1 to: 1 do: [:i | ProfStef next].
    ```
* More nice loops:

    ```pharo
    #(11 38 3 -2 10) do: [:each |
     Transcript show: each printString; cr].

    "Some other really nice iterators"
    
    #(11 38 3 -2 10) collect: [:each | each abs].
    
    #(11 38 3 -2 10) collect: [:each | each odd].
    
    #(11 38 3 -2 10) select: [:each | each odd].
    
    #(11 38 3 -2 10) select: [:each | each > 10].
    
    #(11 38 3 -2 10) reject: [:each | each > 10].
    
    #(11 38 3 -2 10) 
         do: [:each | Transcript show: each printString]
         separatedBy: [Transcript show: '.'].
    ```
* Double quotes denote comments in Pharo.
* The implementation of the unary `selectors` method does something like
  `methods` in Ruby.
* `respondsTo:` with a symbol is another useful bit of introspection.

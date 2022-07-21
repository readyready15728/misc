# Pharo Notes
## Notes on the modern Smalltalk variant Pharo

* One-line code examples can be executed using shortcuts without selecting
  them. Multi-line examples must be selected first.
* `==` tests only for object equality (like in Java). More likely the user
  wants `=`.
* "Literal arrays are created at parse time and are read-only" (but copies are
  mutable—presumably the `isReadOnlyObject` primitive code handles this detail).
* Use dynamic arrays for instances like this one: `{ (2 + 3) . (6 * 6) }`.
* Dynamic arrays are mutable from the get-go and do not need to be sent
  `copy`.
* Pharo works with the system clipboard. How's that for Smalltalk playing
  along nice with the host system? :)
* Use `&` for logical "and" and `|` for logical "or". Logical "not" is a unary
  message of the same name. (Actually, I was told `and:` and `or:` are more
  idiomatic because they're shortcut operators.)
* Indeed, _Kent Beck's Guide to Better Smalltalk_ says that an expression
like `anArray size >= 10 and: [(anArray at: 10) isNil]` is useful to guard
from errors.
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

    ```smalltalk
    Transcript show: 'hello'.
    Transcript show: 'Pharo'.
    Transcript cr.
    ```
    
    and (uses the cascade operator):

    ```smalltalk
    Transcript 
	    show: 'hello';
	    show: 'Pharo' ;
	    cr.
    ```
* Examples of block invocation:

    ```smalltalk
    [:x | x + 2] value: 5.

    [GTPlayground open] value.

    [:x | x + 2] value: 10.

    [:x :y| x + y] value: 3 value: 5.
    ```
* Pharo blocks have lexical closure.
* Example of an "if" statement:

    ```smalltalk
    1 < 2
      ifTrue: [100]
      ifFalse: [42].
    ```

    It's just sending `ifTrue:ifFalse` to a Boolean type!
* Examples of loops:

    ```smalltalk
    1 to: 100 by: 3 do: [:i | Transcript show: i asString; cr].
    
    100 to: 0 by: -2 do: [:i | Transcript show: i asString; cr].
    
    1 to: 1 do: [:i | ProfStef next].
    ```
* More nice loops:

    ```smalltalk
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
* Shift+Alt+Left Click brings up the halo on a Morph to get rid of a pesky morph.
* There is a Vim mode for Pharo!
* From the Discord:

  readyready15728: "I want to file a bug report for Pharo 9.0: whenever I delete text over multiple lines using the Backspace key in a Playground, the Transcript gets flooded with SubscriptOutOfBounds errors. I'm not sure I would be able to fix it on my own but I don't know exactly how to track down the error without a tool like grep. How can I find the offending call to Transcript show:?"

  Todd Blanchard: "SubscriptOutOfBounds is a class.  Specifically, it is a subclass of Error.  So I would probably get it up in the browser (type its name in a playground, select it, cmd-b for browse) and then hit the old 'class refs' button to see where it is used.  That should give you some clues."
* `WelcomeHelp open` opens the initial welcome help window on a fresh image.
* Nice examples of reflection:

```smalltalk
"You can inspect and change the system at runtime.

Take a look at method #ifFalse:ifTrue: source code of class True:"

(True>>#ifFalse:ifTrue:) sourceCode.

"Or just its comment:"

(True>>#ifFalse:ifTrue:) comment.

"Here's all the methods I implement:"

ProfStef selectors.

"Now let's create a new method to go to the next lesson:"

ProfStef class compile:'goToNextLesson
  self next'.

"Wow! I can't wait to use my new method!"

ProfStef goToNextLesson.
```
* **How to get rid of the Exercism logo**:

I want an untainted background image of a Mechanicus Forge World and both the
Pharo and Exercism logos have to go. The former can easily be removed using
the system menu but the latter requires a little work. I found out where the
logo is set by using Finder, setting the type of search to "Classes" and
searching for "Exercism", at `BaselineOfExercism>>setExercismLogo`:

```smalltalk
setExercismLogo
	| exercismLogo |
	exercismLogo := (AlphaImageMorph
		withForm:
		(ZnEasy
		getPng:
			'https://user-images.githubusercontent.com/38899847/48952150-634e9b80-eefe-11e8-890e-7a233d56df65.png'))
		layout: #scaledAspect;
		extent: 100 @ 100;
		position: 10 @ 135;
		lock.
	World addMorph: exercismLogo
```

I then figured out I could go into a Playground and inspect `World submorphs`
in search of my quarry. There are two `AlphaImageMorph` objects in there with
the Exercism logo and I sent them both the unary message `delete` for an
unblemished background.
* The Iceberg tutorial omitted the part where, after creating `src`, you
select the newly created directory as the location for uploaded source.
* From a [thread about Iceberg](http://forum.world.st/Iceberg-for-files-other-than-code-td5097973.html):

```
Indeed. Here's how to get the repository for class MyClass:

repo := IceRepository registeredRepositoryIncludingPackage: MyClass package.

And then the path ist just

repo location.
```
* Example of default parameter in Smalltalk:

```smalltalk
display
  self displayOn: Display
```

Which is implemented as:

```smalltalk
displayOn: aDisplayMedium
  self displayOn: aDisplayMedium at: 0@0
```  
* "Use an Array if you know the size of the collection when you create it and
if the indices into the elements (the first argument to `at:` and `at:put:`)
are consecutive integers between one and the size of the array."
* `OrderedCollection` is more flexible.
* Instances of `OrderedCollection` can be used as stacks and queues, not
unlike Python lists.
* The `Interval` class also exists, similar to Python ranges.

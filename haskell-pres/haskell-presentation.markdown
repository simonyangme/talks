build-lists: true
# Haskell

^ As some of you may know, I've been learning Haskell for the past 3 months. I'd like to share with the group what I've learned, sort of as a progress report.

---
## Why Haskell

### Who even uses it‽

^ Why haskell? Who even uses it?

^ Most think of it as just a research language, but it does actually see some use in industry

---

# Finance

Standard Chartered

- 2.5m lines of Haskell
- Used by engineers and traders alike to write code

^ Traditionally, some of the bigger users are in finance and ad tech. They generally are secretive, but Std Chartered has publically stated their use of Haskell

^ Has to be easy to use and safe

---

# Facebook

Sigma: Facebook's spam/malware/abuse detection system

- Fighting spam with Haskell[^1]
- The Road to Running Haskell at Facebook Scale - Jon Coens[^2]

[^1]: https://code.facebook.com/posts/745068642270222/fighting-spam-with-haskell/

[^2]: https://www.youtube.com/watch?v=sl2zo7tzrO8

^ Recently FB publicized their use of Haskell as well. There recently was a talk at CodeMesh on it

^ impressive numbers: 1M reqs/s, 30% increase in throughput

---

# Grasswire

^ Haskell is not just for large corporations that can throw money at problems

^ Grasswire is a collaborative news service powered by crowdsourced fact checks.

![inline](grasswire-adv-275.png)

![inline](grasswire-1-3-cost.png)

---
# What is Haskell?

> Haskell is a standardized, general-purpose purely functional programming language, with non-strict semantics and strong static typing.

-- Wikipedia

^ Unless you know programming languages well, that probably doesn't mean much. 

^ It didn't make sense to me either until I started to seriously look at Haskell, and then it started coming together.

<!--
---

- General purpose
- Pure
- Functional
- Non-strict (lazy) semantics
- Strong typing
- Static typing

Maybe cut this slide. Don't need to go into detail, probably
-->

---

# What does it mean??
# 🌈🌈

^ So...wdiam?

^ To me, what's special all comes down to the type system

---

# Swift

```swift
func sayHello(personName: String) -> String
```
---

# Swift

```swift
func sayHello(personName: String) -> String {
    let greeting = "Hello, " + personName
    return greeting
}
```
^ What if a bad actor wanted to add a gremlin to the mix discreetly?

---

# Swift

```swift
func sayHello(personName: String) -> String {
    if arc4random() != 0 {
        return greeting = "Hello, " + personName
    } else {
        return "Bye, " + personName
    }
    return greeting
}
```

^ In Swift, types tell you what a function takes as input, and what comes out the other end. But it does not specify what can or cannot happen when the function in run.

^ In fact, other than the types of input and output, it's implicitly implied that *anything* can happen when a function is run. It can increment a counter, update a database, etc.

---

# Swift

```swift
func sayHello(personName: String) -> String
```

### Anything can happen 🙃

---

# Haskell

```haskell
sayHello :: String -> String
```
---
# Haskell

```haskell
sayHello :: String -> String
sayHello = ("Hello, "++)
```
^ What if we wanted it to do what we did in Swift?

---

# Haskell

```haskell
sayHello :: String -> IO String
sayHello name = do
  randomInt <- randomIO
  if randomInt == 0
    then return $ ("Bye, " ++ name)
    else return $ ("Hello, " ++ name)
```

^ In Haskell, you are forced to encode any funny business in the type.

^ Want to fetch a web page? Update a database entry? Read from a file? All those have to be encoded in the type.

^ It sounds like a hassle, but it forces the developer to write better code

^ Not representative of real haskell code

---

# Haskell

```haskell
sayHello :: Integer -> String -> String
sayHello i name = 
  if i == 0
    then return $ ("Bye, " ++ name)
    else return $ ("Hello, " ++ name)

-- Some other code/function would deal with the IO
```

^ This is more representative of typical haskell code

^ Interactions with the unpredictable outside world moves closer to the outer layers of the code, while isolating the rest of the code base

^ It makes more of the code purely functional. That means more predictable code, more easily testable code, and more maintainable code.

---

# TDD?

---

# Type Driven Development

There's a saying in Haskell: "If it compiles, it works"

---

# Type Driven Development

There's a saying in Haskell: "If it compiles, it works"

Development process ends up being:

- Write the types
- Write code until compiler stops complaining
- ...
- Profit!

---

![inline](haskell-magic.png)

https://twitter.com/leothrix/status/672825545273565184

^ Now that you have working code, it's probably a mess and you want to refactor it...

---
# Refactoring

## "If it compiles, it works"

^ This is one of the places where Haskell really shines. Separation of concerns that was forced on you by the type system pays off here. 

^ If you already have working code, "If it compiles, it works" applies even more.

---
# Testing

- More testable code
- Less things to test (especially vs. JS/Ruby/etc.)
- State of the art testing tools (QuickCheck)

^ Pure functions (due to separation of concerns) are aplenty, and easier to test

^ Type system helps enforce certain properties, so less tests needed

^ State of the art testing tools often come from languages like Haskell. QuickCheck which offers property-based testing. You write a function that describes a relationship between the input and output that must hold (example: sayHello), and it'll run 100s or 1000s of random test cases.

---
<!-- 
# Tooling

--- 
-->
# Hoogle/Hayoo/etc.

![inline](hoogle-name.png)

^ not only search by function name, but if you know the shape of the function you're looking for

---
# Hoogle/Hayoo/etc.

![inline](hoogle-type.png)

^ you can also type the type signature in

<!-- 
---
# REPL

- Incremental development
- Type inspection
- Type holes (_)
 -->
---
# And more...

- Code reuse
- Learning curve
- Speed
- Parallelism (STM)
- REPL

---
# Lots of libraries available

- Web frameworks (Yesod, Snap, Spock, Scotty, ...)
- JSON (Aeson)
- Parsers (Parsec, Attoparsec, etc.)
- More on Hackage, Haskell's package repository

---
# How do I start?

- Haskell Programming from first principles (haskellbook.com)
- CIS194 from UPenn (Spring '13) or openhaskell.com
- #haskell/#haskell-beginners on freenode
- Santa Monica Haskell meetup

^ If this all sounds interesting to you...

^ and I think Haskell is a language worth learning even if you don't end up using it, because it can teach you some new higher level abstractions, which can apply anywhere, and make you a better programmer in general

---
# Thanks!

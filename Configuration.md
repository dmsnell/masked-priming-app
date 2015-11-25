The app should be configurable from a single human-readable text-file. This document is not final and is currently serving as the scratch pad for developing the configuration interface.

There's probably a good benefit to separating the static card content from the logic that controls how and when they are displayed. Although these views and rules could be interleaved in the same data structure, by separating them the cards and cardstacks themselves could be stored in some kind of repository and reused across experiements (maybe `include`-able).

## Declarative Properties

Certain pieces of the app are static and directly map to nothing more than data. Things such as the actual cards displayed on screen are some of these things because they remain the same regardless of what operational activity occurs.

### As native language-objects

The configuration for the cards could be done in a language-native way such as with JSON, an actual JavaScript object, EDN, or similar.

```js
{
  cardStacks: [
    {
      cards: [
        { fromLibrary: "focalPoint" },
        { content: "horse", duration: 200 },
        { content: "house" }
      ]
    },
    {
      name: "semanticViolin",
      cards: [
        { fromLibrary: "focalPoint" },
        { content: "cello", duration: 100 },
        { content: "viola", duration: 100 },
        { content: "violin" }
      ]
    }
  ],
  
  cardLibrary: {
    focalPoint: { content: "*", duration: 500 }  
  }
}
```

#### Pros

 - Easy to parse in the related language
 - Existing linting/parsing tools already exist
 - Duck-typing with list/map syntax built-in

#### Cons

 - Not as readable for non-programmers
 - More picky about things like semi-colons, brackets, etc...

### As yaml

Not too different from using native objects but with a slightly friendlier syntax

```yaml
cardStacks:
  - cards:
    - *focalPoint
    - content: "horse"
      duration: 200
    - content: "house"
  - cards: &semanticViolin
    - *focalPoint
    - content: "cello"
      duration: 100
    - content: "viola"
      duration: 100
    - content: "violin"

cardLibrary:
  - content: "*" &focalPoint
    duration: 500
```

#### Pros

 - Convenient and terse syntax, easily readable
 - Built-in anchors and references (naming)

#### Cons

 - Some parts of the syntax are confusing

### As XML

Haha, just kidding! 😉

### As actual language code

The cards could be built programmatically too. This method really opens up the possibilities for an ambitious researcher who could pass around things like callbacks to modify behavior at runtime, though this would break the separation between the static and runtime components.

#### In JavaScript
```js
makeSequence()
  .addStack()
    .addCard().fromLibrary( "focalPoint" )
    .addCard().showing( "horse" ).lasting( 200 )
    .addCard().showing( "house" )
  .addStack()
    .named( "semanticViolin" )
    .addCard().fromLibrary( "focalPoint" )
    .addCard().showing( "cello" ).lasting( 100 )
    .addCard().showing( "viola" ).lasting( 100 )
    .addCard().showing( "violin" );

makeLibrary()
  .addCard().named( "focalPoint" ).showing( "*" ).lasting( 500 );
```

#### In Clojure
```clojure
(makeSequence
  (addStack
    (addCard fromLibrary "focalPoint")
    (addCard showing "horse" for 500)
    (addCard showing "house"))
  (addStack named "semanticViolin"
    (addCard fromLibrary "focalPoint")
    (addCard showing "cello" for 100)
    (addCard showing "viola" for 100)
    (addCard showing "violin")))

(makeLibrary
  (addCard named "focalPoint" showing "*" for 500))
```

#### Pros

 - Maybe easier to extend and organically grow without breaking compatability
 - Simply runs in the language - linters and parsers already exist
 - Trivial to script by adding language code, _i.e._ looping, conditionals, etc...

#### Cons

 - Pretty verbose
 - Basically required programming knowledge to harness

## Operational Properties

The flow of the cards can be programmatically controlled, such as only displaying a certain card stack if another particular card stack had an inaccurate response.

These rules should also be able to be listed declaratively but could presumably include callbacks for runtime control.

### Possible control-flow actions

 - Show cardstack on condition
 - Show card on condition
 - Repeat cardstack (up to N times)

### Possible conditions

 - A certain card stack received an (in)correct response

#### As YAML
```yaml
rules:
  - for: "semanticViolin"
    skip:
      - ifCorrect: *semanticTuba
      - ifCorrect: *semanticFlute
  - for: "phoneticHouse"
    onlyShow:
      - ifIncorrect: *phoneticHorse
    repeat:
      - upTo: 5
```

#### As JavaScript
```js
skip( "semanticViolin" ).whenCorrect( "semanticTuba" );
onlyShow( "semanticViolin" ).whenIncorrect( "semanticTuba" );
```

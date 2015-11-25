The app should be configurable from a single human-readable text-file. This document is not final and is currently serving as the scratch pad for developing the configuration interface.

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

## Operational Properties

The flow of the cards can be programmatically controlled, such as only displaying a certain card stack if another particular card stack had an inaccurate response.

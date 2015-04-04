InteractionManager allows long-running work to be scheduled after any interactions/animations have completed. In particular, this allows JavaScript animations to run smoothly.

Applications can schedule tasks to run after interactions with the following:

```javascript
InteractionManager.runAfterInteractions(() => {
  // ...long-running synchronous task...
});
```

Compare this to other scheduling alternatives:

* requestAnimationFrame(): for code that animates a view over time.
* setImmediate/setTimeout(): run code later, note this may delay animations.
* runAfterInteractions(): run code later, without delaying active animations.

The touch handling system considers one or more active touches to be an 'interaction' and will delay `runAfterInteractions()` callbacks until all touches have ended or been cancelled.

InteractionManager also allows applications to register animations by creating an interaction 'handle' on animation start, and clearing it upon completion:

```javascript
var handle = InteractionManager.createInteractionHandle();
// run animation... (`runAfterInteractions` tasks are queued)
// later, on animation completion:
InteractionManager.clearInteractionHandle(handle);
// queued tasks run if all handles were cleared
```

## Methods 
static **runAfterInteractions**(callback: Function) 

Schedule a function to run after all interactions have completed.

static **createInteractionHandle**() 

Notify manager that an interaction has started.

static **clearInteractionHandle**(handle: number) 

Notify manager that an interaction has completed.
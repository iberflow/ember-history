ember-history
=============

Undo / Redo for Emberjs

Usage
-----
``` javascript
App = Ember.Application.create({});

obj = Ember.Object.create(Ember.History, {
    _trackProperties: 'width height list'.w(),
    width: '100px',
    height: '50px',
    list: ['asd','bbd','xxx']
});

obj.set('width','50px');
obj.set('height','100px');
obj.set('list', ['lol']);

History.undo() //list is now back to ['asd','bbd','xxx']
History.undo() // height is now 50px
History.redo() // height is 100px again
//etc.

```

You can also disable the history for a while
``` javascript
History.disable();
obj.set('height','300px'); //This won't push a new history state
History.enable();
obj.set('height','300px'); //This will now do
```
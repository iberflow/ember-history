ember-history
=============

Undo / Redo for Emberjs
Inspired by https://github.com/pangratz/ember-memento, however this implementation is for global History and not for individual objects. Though it doesn't matted how many objects you have it work's with one if you like.


Usage
-----
``` javascript
App = Ember.Application.create({});

obj = Ember.Object.create(Ember.History, {
    _trackProperties: 'width height list'.w(),
    width: '100px',
    height: '50px',
    list: ['item3','carrot','car']
});

obj2 = Ember.Object.create(Ember.History, {
    _trackProperties: 'name surname'.w(),
    name: 'Ignas',
    surname: 'Bernotas',
});

obj2.set('name','Matthew');
obj.set('height','100px');
obj.set('list', ['item1']);
obj2.set('surname', 'Parry');

History.undo(); // surname is now back to Bernotas
History.undo(); // list is now back to ['item3','carrot','car']
History.undo(); // height is now 50px
History.undo(); // name is now Ignas
History.redo(); // name is now Matthew
History.redo(); // height 100px
History.redo(); // list is ['item1'] again
History.redo(); // surname is Parry again
```

You can also disable the history for a while
``` javascript
History.disable();
obj.set('height','300px'); //This won't push a new history state
History.enable();
obj.set('height','300px'); //This will
```

And you can also clear the states
``` javascript
History.clear()
```
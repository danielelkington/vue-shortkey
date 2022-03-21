![vue-shortkey logo](https://github.com/danielelkington/vue-shortkey/blob/master/logo/shortkey.png?raw=true)

[![npm version](https://badge.fury.io/js/vue-three-shortkey.svg)](https://badge.fury.io/js/vue-three-shortkey)
[![npm](https://img.shields.io/npm/dt/vue-three-shortkey.svg)](https://www.npmjs.com/package/vue-three-shortkey)
[![MIT Licence](https://badges.frapsoft.com/os/mit/mit.svg?v=103)](https://opensource.org/licenses/mit-license.php)

Fork of [vue-shortkey](https://github.com/iFgR/vue-shortkey) with Vue 3 support.

Useful if you were previously using vue-shortkey in a Vue 2 project and you want to upgrade to Vue 3 without hassle - you should be able to switch to this npm package and update import statements, and apart from that this should be 100% compatible with your existing code.

Vue-Three-ShortKey - plugin for VueJS 3.x that accepts shortcuts globally and in a single listener.

## Install
```
npm install vue-three-shortkey --save
```

## Usage
```javascript
app.use(require('vue-three-shortkey'))
```
Add the shortkey directive to the elements that accept the shortcut.
The shortkey must have explicitly which keys will be used.

#### Running functions
<sub>The code below ensures that the key combination ctrl + alt + o will perform the 'theAction' method.</sub>

```html
<button v-shortkey="['ctrl', 'alt', 'o']" @shortkey="theAction()">Open</button>
```
The function in the modifier __@shortkey__ will be called repeatedly while the key is pressed. To call the function only once, use the __once__ modifier
```html
<button v-shortkey.once="['ctrl', 'alt', 'o']" @shortkey="theAction()">Open</button>
```

#### Multi keys
```html
<button v-shortkey="{up: ['arrowup'], down: ['arrowdown']}" @shortkey="theAction">Joystick</button>
```
... and your method will be called with the key in the  parameter
```javascript
methods: {
  theAction (event) {
    switch (event.srcKey) {
      case 'up':
        ...
        break
      case 'down':
        ...
        break
```

#### Setting the focus
You can point the focus with the shortcut easily.
<sub>The code below reserves the ALT + I key to set the focus to the input element.</sub>
```html
<input type="text" v-shortkey.focus="['alt', 'i']" v-model="name" />
```

#### Push button
Sometimes you may need a shortcut works as a push button. It calls the function one time when you click the button. When you release the shortcut, it calls the same function again like a toggle. In these cases, insert the "push" modifier.

The example below shows how to do this
```html
<tooltip v-shortkey.push="['f3']" @shortkey="toggleToolTip"></tooltip>
```

#### Using on a component
Use the modifier `native` to catch the event.
```html
 <my-component v-shortkey="['ctrl', 'alt', 'o']" @shortkey.native="theAction()"></my-component>
```

#### Multiple listeners
Use the modifier `propagate` to let the event propagate to other listeners
```html
 <my-component v-shortkey="['ctrl', 'alt', 'o']" @shortkey.propagate="anAction()"></my-component>
 <my-component v-shortkey="['ctrl', 'alt', 'o']" @shortkey.propagate="aDifferentAction()"></my-component>
```

#### Key list
| Key                        | Shortkey Name |
|----------------------------|---------------|
| Delete                     | del           |
| Backspace                  | backspace     |
| Insert                     | insert        |
| NumLock                    | numlock       |
| CapsLock                   | capslock      |
| Pause                      | pause         |
| ContextMenu                | contextmenu   |
| ScrollLock                 | scrolllock    |
| BrowserHome                | browserhome   |
| MediaSelect                | mediaselect   |
| Shift                      | shift         |
| Control                    | ctrl          |
| Alt                        | alt           |
| Alt Graph                  | altgraph      |
| Super (Windows or Mac Cmd) | meta          |
| Arrow Up                   | arrowup       |
| Arrow Down                 | arrowdown     |
| Arrow Left                 | arrowleft     |
| Arrow Right                | arrowright    |
| Enter                      | enter         |
| Escape                     | esc           |
| Tab                        | tab           |
| Space                      | space         |
| Page Up                    | pageup        |
| Page Down                  | pagedown      |
| Home                       | home          |
| End                        | end           |
| A - Z                      | a-z           |
| 0-9                        | 0-9           |
| F1-F12                     | f1-f12        |

You can make any combination of keys as well as reserve a single key.
```html
<input type="text" v-shortkey="['q']" @shortkey="foo()"/>
<button v-shortkey="['ctrl', 'p']" @shortkey="bar()"></button>
<button v-shortkey="['f1']" @shortkey="help()"></button>
<textarea v-shortkey="['ctrl', 'v']" @shortkey="dontPaste()"></textarea>
```

#### Avoided fields
You can avoid shortcuts within fields if you really need it. This can be done in two ways:
* Preventing a given element from executing the shortcut by adding the **v-shortkey.avoid** tag in the body of the element
```html
<textarea v-shortkey.avoid></textarea>
```
* Generalizing type of element that will not perform shortcut. To do this, insert a list of elements in the global method.

```javascript
app.use('vue-three-shortkey', { prevent: ['input', 'textarea'] })
```

* Or even by class
```javascript
app.use('vue-three-shortkey', { prevent: ['.my-class-name', 'textarea.class-of-textarea'] })
```

#### Other uses
With the dynamism offered by Vue, you can easily create shortcuts dynamically
```html
<li v-for="(ctx, item) in items">
  <a
    href="https://vuejs.org"
    target="_blank"
    v-shortkey="['f' + (item + 1)]"
    @shortkey="testa(item)"
    @click="testa()">
      F {{ item }}
  </a>
</li>
```

### Unit Test
```
npm test
```

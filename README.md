Redux DevTools Log Monitor Filterable
=====================================

Fork of [Redux DevTools Log Monitor](https://github.com/gaearon/redux-devtools-log-monitor) with the ability to specify actions to be hidden or shown in DevTools.

### Installation

```
npm install --save-dev redux-devtools-log-monitor-filterable
```

### Usage

You can use `LogMonitor` as the only monitor in your app:

##### `containers/DevTools.js`

```js
import React from 'react';
import { createDevTools } from 'redux-devtools';
import LogMonitor from 'redux-devtools-log-monitor';

export default createDevTools(
  <LogMonitor filter={{ blacklist: ['ACTION1', 'ACTION2'], whitelist: ['ACTION1', 'ACTION2'] }} />
);
```

Then you can render `<DevTools>` to any place inside app or even into a separate popup window.

Alternative, you can use it together with [`DockMonitor`](https://github.com/gaearon/redux-devtools-dock-monitor) to make it dockable.  
Consult the [`DockMonitor` README](https://github.com/gaearon/redux-devtools-dock-monitor) for details of this approach.

[Read how to start using Redux DevTools.](https://github.com/gaearon/redux-devtools)

### Features

Every action is displayed in the log. You can expand the tree view to inspect the `action` object and the `state` after it.

If a reducer throws while handling an action, you will see “Interrupted by an error up the chain” instead of the state and action tree view. Scroll up until you find the action which caused the error. You will see the error message in the action log entry. If you use a hot reloading tool, you can edit the reducer, and the error will automatically update or go away.

Clicking an action will disable it. It will appear crossed out, and the state will be recalculated as if the action never happened. Clicking it once again will enable it back. Use this together with a hot reloading solution to work sequentially on different states of your app without reproducing them by hand. You can toggle any action except for the initial one.

There are four buttons at the very top. “Reset” takes your app to the state you created the store with. The other three buttons work together. You might find it useful to think of them like you think of Git commits. “Commit” removes all actions in your log, and makes the current state your initial state. This is useful when you start working on a feature and want to remove the previous noise. After you’ve dispatched a few actions, you can press “Revert” to go back to the last committed state. Finally, if you dispatched some actions by mistake and you don’t want them around, you can toggle them by clicking on them, and press “Sweep” to completely remove all currently disabled actions from the log.

### Props

Name                  | Description
-------------         | -------------
`theme`               | Either a string referring to one of the themes provided by [redux-devtools-themes](https://github.com/gaearon/redux-devtools-themes) (feel free to contribute!) or a custom object of the same format. Optional. By default, set to [`'nicinabox'`](https://github.com/gaearon/redux-devtools-themes/blob/master/src/nicinabox.js).
`select`              | A function that selects the slice of the state for DevTools to show. For example, `state => state.thePart.iCare.about`. Optional. By default, set to `state => state`.
`preserveScrollTop`   | When `true`, records the current scroll top every second so it can be restored on refresh. This only has effect when used together with `persistState()` enhancer from Redux DevTools. By default, set to `true`.
`filter`              | An object with `blacklist` or `whitelist` arrays, which specify either actions to be hidden or shown in DevTools. If the latter is specified, other than those actions will be hidden.

### License

MIT

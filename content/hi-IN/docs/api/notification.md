# Notification

> Create OS desktop notifications

Process: [Main](../glossary.md#main-process)

## Using in the renderer process

If you want to show Notifications from a renderer process you should use the [HTML5 Notification API](../tutorial/notifications.md)

## Class: Notification

> Create OS desktop notifications

Process: [Main](../glossary.md#main-process)

`Notification` is an [EventEmitter](http://nodejs.org/api/events.html#events_class_events_eventemitter).

It creates a new `Notification` with native properties as set by the `options`.

### Static Methods

The `Notification` class has the following static methods:

#### `Notification.isSupported()`

Returns `Boolean` - Whether or not desktop notifications are supported on the current system

### `new Notification([options])` *Experimental*

* `options` ऑब्जेक्ट 
  * `title` String - A title for the notification, which will be shown at the top of the notification window when it is shown
  * `subtitle` String - (optional) A subtitle for the notification, which will be displayed below the title. *macOS*
  * `body` String - The body text of the notification, which will be displayed below the title or subtitle
  * `silent` Boolean - (optional) Whether or not to emit an OS notification noise when showing the notification
  * `icon` [NativeImage](native-image.md) - (optional) An icon to use in the notification
  * `hasReply` Boolean - (optional) Whether or not to add an inline reply option to the notification. *macOS*
  * `replyPlaceholder` String - (optional) The placeholder to write in the inline reply input field. *macOS*
  * `sound` String - (optional) The name of the sound file to play when the notification is shown. *macOS*
  * `actions` [NotificationAction[]](structures/notification-action.md) - (optional) Actions to add to the notification. Please read the available actions and limitations in the `NotificationAction` documentation *macOS*

### Instance Events

Objects created with `new Notification` emit the following events:

**Note:** Some events are only available on specific operating systems and are labeled as such.

#### Event: 'show'

Returns:

* `event` Event

Emitted when the notification is shown to the user, note this could be fired multiple times as a notification can be shown multiple times through the `show()` method.

#### Event: 'click'

Returns:

* `event` Event

Emitted when the notification is clicked by the user.

#### Event: 'close'

Returns:

* `event` Event

Emitted when the notification is closed by manual intervention from the user.

This event is not guarunteed to be emitted in all cases where the notification is closed.

#### Event: 'reply' *macOS*

Returns:

* `event` Event
* `reply` String - The string the user entered into the inline reply field

Emitted when the user clicks the "Reply" button on a notification with `hasReply: true`.

#### Event: 'action' *macOS*

Returns:

* `event` Event
* `index` Number - The index of the action that was activated

### Instance Methods

Objects created with `new Notification` have the following instance methods:

#### `notification.show()`

Immediately shows the notification to the user, please note this means unlike the HTML5 Notification implementation, simply instantiating a `new Notification` does not immediately show it to the user, you need to call this method before the OS will display it.

### Playing Sounds

On macOS, you can specify the name of the sound you'd like to play when the notification is shown. Any of the default sounds (under System Preferences > Sound) can be used, in addition to custom sound files. Be sure that the sound file is copied under the app bundle (e.g., `YourApp.app/Contents/Resources`), or one of the following locations:

* `~/Library/Sounds`
* `/Library/Sounds`
* `/Network/Library/Sounds`
* `/System/Library/Sounds`

See the [`NSSound`](https://developer.apple.com/documentation/appkit/nssound) docs for more information.
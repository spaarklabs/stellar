[![LENIS](https://assets.darkroom.engineering/lenis/header.png)](https://github.com/darkroomengineering/lenis)

Go to [darkroomengineering/lenis](https://github.com/darkroomengineering/lenis) for docs. This repository only documents patches made for better control over lenis.

## Install
```
npm i git+https://github.com/spaarkstudio/aided-lenis.git
```
This will replaces `lenis` dependency source, so you don't have to make any further changes to the codebase to use this fork.
```js
"dependencies": {
    "lenis": "github:spaarkstudio/aided-lenis", // Replaces official version.
}
```

## Patches
- Introduce `changed` boolean variable to `onComplete`.
    - If the scrollTo `target` equals the current scroll offset, `changed` would be `false`, otherwise `changed` would be `true`.
    - Reason: `changed` allows developers to handle asynchronous tasks differently when `scrollTo` does nothing and executes `onComplete`.
```js
lenis.scrollTo(target, {
    duration: 2,
    onComplete(lenis, changed) {
        if (changed) {
            console.log("It did scroll, so I'm executed after 2 seconds.");
        } else {
            console.log("The target is the same as the scroll offset, so I'm executed immediately.");
        }
    }
});
```

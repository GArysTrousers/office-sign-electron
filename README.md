# Office Sign
Electron edition

This is an electron version of my digital office sign.

It can dispay configurable messages and timers.

## Features
- Different statuses (Open, Closed, etc) 
- Adjustable timer ⏲️
- Timer triggered changes ⚡
- Launch on Startup 🌅

![Open and Closed](etc/screen1.png)

## Controls
- Number Keys 0-9: Switch between messages
- Spacebar: Add 10 mins or start 10 min timer
- Backspace: Reset timer
- Escape: Exit app
- F11: toggle Fullscreen

## Customising
The business logic is located at /src/routes/index.svelte

You'll find an array called 'messages' you can add to.

The message object looks like:
```
{
  title: '',          <- BIG TEXT
  body: '',           <- small text
  bg: '',             <- Classes to add to the back panel
  onStart: () => {},  <- Function to run when switched to
  onTimeout: () => {},<- Function to run when timer runs out
  onEnd: () => {},    <- Function to run when switched from
}
```

## Building
Open the root directory in a terminal and run:
```
npm i
npm run dev   <- to test program
npm run build <- to build installer
```
Installer will be located at ./dist/Office Sign Setup x.x.x.exe
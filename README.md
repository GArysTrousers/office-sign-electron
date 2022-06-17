# Office Sign
Electron edition

## Features
- Different statuses (Open, Closed, etc) 
- Adjustable timer ⏲️
- Timer triggered changes ⚡
- Launch on Startup

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
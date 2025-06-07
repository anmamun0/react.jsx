## Electron Desktop App

```bash
spi/
├── polytechnic_library_system/   ← 🟦 Django Backend
│   └── manage.py
├── spi-library/                  ← 🟨 Vite + React Frontend
│   └── vite.config.js
│   └── dist/                     ← ✅ Vite build output
├── electron-spi/                ← 🟥 Electron Desktop App
│   └── main.js                  ← Electron Entry (you edit this)
│   └── public/                  ← Copy of dist/
│       └── index.html

```


#### spi-library React File এ

```
npm run build
React File /dist ফাইল এর (assets,index.html) কপি করা electron-spi -এর public folder এর ভিতর past করো।
```




#### electron-spi File এ

#### 1. main.js
```js
import { HashRouter as Router, Route, Routes } from "react-router-dom";

const { app, BrowserWindow } = require('electron');
const path = require('path');

function createWindow() {
      // Django Backend Start
//   exec('start cmd.exe /k "cd ../polytechnic_library_system && venv\\Scripts\\activate && python manage.py runserver"', (error) => {
//     if (error) {
//       console.error('Backend Start Error:', error);
//     } else {
//       console.log('Backend server started.');
//     }
//   });

    
  const win = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      preload: path.join(__dirname, 'preload.js'), // যদি থাকে
      nodeIntegration: true,
      contextIsolation: false,
    }
  });

  // লোকাল ফাইল লোড করবে, তুমি যে build ফোল্ডার তৈরি করেছো সেটা ঠিক path দিতে হবে
  win.loadFile(path.join(__dirname, 'public', 'index.html'));

  // ডেভটুলস ওপেন করতে চাইলে:
  // win.webContents.openDevTools();
}

app.whenReady().then(() => {
  createWindow();

  app.on('activate', () => {
    if (BrowserWindow.getAllWindows().length === 0) createWindow();
  });
});

app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') app.quit();
});

```
#### terminal

```bash
cd/electron-spi
npm install electron --save-dev # as a development dependency.
npm init -y # electron/package.json ফাইল তৈরি হবে। তারপর সেটাতে devDependencies এবং scripts ম্যানুয়ালি যোগ করো।
```

#### package.json

```json
{
  "name": "electron-spi",
  "version": "1.0.0",
  "main": "main.js",
  "scripts": {
    "start": "electron ."
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "description": ""
}
```



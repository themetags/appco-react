## Theme Installation

To install the theme you have to install [React](https://create-react-app.dev/) than go to the `theme root directory` where `package.json` located.
Now install packages use this commend. Before running the command, make sure that you have `nodejs` installed to your machine.

```bash
npm install
```
it will install the packages.

After install process now you can run local server- 
local server port is 'http://localhost:3000' For development start use this commend `npm start` 

```bash
npm start
```

## Run static server (optional)
If you want to run the build project then we need to follow the following steps:

First install `serve`:
```bash
npm install -g serve
```

Then build the project:
```bash
npm run build
```

Finally run the project:
```bash
serve -s build
```

If you want know more about static deployment please visit [Create react app deployment](https://create-react-app.dev/docs/deployment/)
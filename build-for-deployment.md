###  For Build
To build your project for deployment, we just need to run the `build` command like:
```bash
npm run build
```

## Run static server (optional)
If you want to run the build project then we need to follow the following steps:

First install `serve`:
```bash
npm install -g serve
```

Then build the project (if you already the build the project then skill this):
```bash
npm run build
```

And run the project:
```bash
serve -s build
```

If you want know more about static deployment please visit [Create react app deployment](https://create-react-app.dev/docs/deployment/)
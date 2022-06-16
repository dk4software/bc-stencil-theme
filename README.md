# Local dev environment for Bigcommerce

## Steps to setup

- Checkout your theme into `src/` folder. You can take one of the below options:

  - Clone the **cornerstone theme**: `git clone git@github.com:bigcommerce/cornerstone.git src/` **OR**
  - Use the source code of a **custom theme**:
    - Go to Storefront > My Themes
    - Click on the thumbnail for the theme which you wish to customize. This will take you to the theme page.
    - Click on the appropriate button to download the theme:
      - Advanced > "Download Current Theme"
      - Advanced > "Download Original Theme"
      - "Theme Options" > "Download your latest customizations",
      - etc.
    - This will download a zip of the theme.
    - Extract that zip to the `src/` folder.
- Clone the checkout source from https://github.com/bigcommerce/checkout-js into `checkout-src/` folder by running `git clone git@github.com:bigcommerce/checkout-js.git checkout-src/`

- Find the channel that you want to work with. Open [docker-compose.yml](docker-compose.yml) and search for 'channel Id'. Change the parameter value against '-c' as the channel Id that you want to work with.

- Run `bin/init` for initial setup of the environment. It will bring up the containers and also prompt for initializing the stencil API tokens (which link your theme to the Bigcommerce store)

- Going forward, use `bin/start` to start the environment
- To stop the environment, use `bin/stop`.
- To find the status of the containers, use `bin/status`.
- To execute a stencil command e.g. push, bundle etc, use `bin/cli <command>`. e.g. to bundle the theme, run: `bin/cli bundle`.

Once the docker is running properly, you can access the website in the local using [http://localhost:3000](http://localhost:3000)

## Configure Checkout

- Once the docker containers are running properly, open bigcommerce [control panel](https://login.bigcommerce.com)
- Go to Advance Settings > Checkout in Left Navigation.
- In General Settings, change Checkout Type to 'Custom Checkout'.
- Scroll down and in the Custom Checkout Settings, update the Script URL as [http://127.0.0.1:8080/auto-loader-dev.js](http://127.0.0.1:8080/auto-loader-dev.js) and Save

## Issues and Resolution

### Stencil Docker exit with error message

```txt
stencil_1  | internal/modules/cjs/loader.js:818
stencil_1  |   throw err;
stencil_1  |   ^
stencil_1  |
stencil_1  | Error: Cannot find module 'webpack'
stencil_1  | Require stack:
stencil_1  | - /theme/stencil.conf.js
```

**Solution:** Connect to the docker by running the command: `docker-compose run --rm stencil bash`

Now run the command: `npm install` in the theme directory. Restart the docker and it should work.

### Checkout Docker exit error message

```txt
docker logs bc-stencil-theme_checkout-server_1

> @bigcommerce/checkout@1.182.1 dev:server /checkout-src
> http-server build

sh: 1: http-server: not found
npm ERR! code ELIFECYCLE
npm ERR! syscall spawn
npm ERR! file sh
npm ERR! errno ENOENT
npm ERR! @bigcommerce/checkout@1.182.1 dev:server: `http-server build`
npm ERR! spawn ENOENT
npm ERR!
npm ERR! Failed at the @bigcommerce/checkout@1.182.1 dev:server script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.
npm WARN Local package.json exists, but node_modules missing, did you mean to install?
```

**Solution:** Connect to the docker by running the command: `docker-compose run --rm checkout-dev bash`

Now run the command, in the source directory: `npm install`. Restart the docker and it should work.

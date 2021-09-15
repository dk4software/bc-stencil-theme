# Local dev environment for Bigcommerce: Stencil

## Steps to setup

- Checkout your theme into `src/` folder. You can take one of the below options:

  - Clone the **cornerstone theme**: `git clone git@github.com:bigcommerce/cornerstone.git src/` **OR**
  - Use the source code of a **custom theme**:
    - Go to Storefront > My Themes
    - Click on the thumbnail for the theme which you wish to customize. This will take you to the theme page.
    - Click the "Theme Options" drop down.
    - Select "Download your latest customizations". This will download a zip of the theme in it's current state.
    - Extract that zip to the `src/` folder.

- Run `bin/init` for initial setup of the environment. It will bring up the containers and also prompt for initializing the stencil API tokens (which link your theme to the Bigcommerce store)

- Going forward, use `bin/start` to start the environment
- To stop the environment, use `bin/stop`.
- To find the status of the containers, use `bin/status`.

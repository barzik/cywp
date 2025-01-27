# cypress-for-wordpress [![Test](https://github.com/OmriBarZik/cywp/actions/workflows/tests.yml/badge.svg)](https://github.com/OmriBarZik/cywp/actions/workflows/tests.yml)
Help you create testing environments for your WordPress plugins and themes.
## requirement
1. you must have cypress 6.7 or above
2. you must have docker up and running on your system.
## installation
```bash
npm install --dave-save cypress-for-WordPress
```

Add this at the `index.js` file in the plugin folder.
```js
module.exports = (on, config) => {
  return require('cypress-for-wordpress')(on, config)
}
```

this will analize the plugin configuration and will set the `baseUrl`. for more info [see](https://docs.cypress.io/guides/references/configuration#Global).

## Configuration
you can config your site by using the following configuration in your `cypress.json` file.
#### example
```jsonc
{
  "wordpressVersion": "latest", // WordPress version of the site.
  "wordpressPort": "8000", // On waht port the site will be expose.
  "wordpressTheme": "twentytwenty", // The theme of the site.
  "wordpressThemeVersion": "latest", // Version of the theme.
  "wordpressThemePath": "/path/to/theme", // uses localy installed theme.
  "wordpressPlugins": { // List of plugins you want to be installed on the site.
     "LocalPlugin": "./", // Relative path to localy installed plugin.
     "OtherLocalPlugin": "/path/to/plugin/LocalPlugin", // Absulute Path to localy installed plugin.
     "RemotePlugin": "1.0.0", // Version of the plugins the runner will install automatically.
     "OtherRemotePlugin": "latest" // Use the latest version available.
  }
}
```
### wordpressVersion
#### default `latest`
Sets the WordPress version on the site. 
### wordpressPort
#### default `8000`
Sets on which port the site will be expose.
### wordpressTheme
#### default `twentytwenty`
Sets the theme of the site.
### wordpressThemePath
#### default `latest`
Sets the theme's version.
### wordpressThemePath
#### default `none`
Path to localy installed theme.
this option enebale you to test your own theme on a vertual site.

If this config is set the plugin will create a bind between the given path and the docker container. the `wordpressThemePath` config weill be ignored.
This path must contain a theme with the same name as mentioned at `wordpressTheme`
### wordpressPlugins
#### default `none`
Object the that contains two types of plugins.
#### Local Plugins
You set the local plugins by passing its path. The plugin's name must be the same as the parameter

you can use relative and absolute paths.
```jsonc
{
  "wordpressPlugins": {
    "LocalPath": "./", // To expose current project to the docker contianer.
    "otherLocalPath": "/path/to/plugin/" // this path contians otherLocalPath.php
}
```

#### Remote Plugins
Remote plugins are plugins that will be download from the WordPress official site, install and activate on the site.

You add remote plugins by passing the wanted version.
```jsonc
{
  "wordpressPlugins": {
    "remotePlugin": "latest", // Install the latest version available. 
    "otherRemotePlugin": "1.3.5" // Install a spesific version.
  }
}
```

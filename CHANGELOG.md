* For versions prior to v6, see the [5.x stable branch of rails/webpacker](https://github.com/rails/webpacker/tree/5-x-stable). 
* Please see [UPGRADE GUIDE](./docs/v6_upgrade.md).

## Versions
### [Unreleased]
Changes since last non-beta release.

*Please add entries here for your pull requests that are not yet released.*
## [v6.0.0.rc.14] - January 20, 2022

### Improved
- Raise on multiple invocations of javascript_pack_tag and stylesheet_pack_tag helpers. [PR 19](https://github.com/shakacode/shakapacker/pull/19) by [tomdracz](https://github.com/tomdracz].
- Remove automatic addition of node_modules into rails asset load path. [PR 20](https://github.com/shakacode/shakapacker/pull/20) by [tomdracz](https://github.com/tomdracz].
- Remove pnp-webpack-plugin. [PR 21](https://github.com/shakacode/shakapacker/pull/21) by [tomdracz](https://github.com/tomdracz].

## [v6.0.0.rc.13 changes from v6.0.0.rc.6]

### Merged from rails/webpacker

- Make watched_files_digest thread safe. [rails/webpacker #3233](https://github.com/rails/webpacker/pull/3233) 
- Use single webpack config webpack.config.js. [rails/webpacker #3240](https://github.com/rails/webpacker/pull/3240)
- Switch to peer dependencies. [rails/webpacker #3234](https://github.com/rails/webpacker/pull/3234)

### Upgrading from rails/webpacker 6.0.0.rc.6
- Single default configuration file of `config/webpack/webpack.config.js`. Previously, the config file was set
  to `config/webpack/#{NODE_ENV}.js`.
- Changed all package.json dependencies to peerDependencies, so upgrading requires adding the dependencies, per the [UPGRADE GUIDE](./docs/v6_upgrade.md).

## [v6.0.0.rc.6 changes from v5.4] - Forked January 16, 2022


- `node_modules` will no longer be babel transfomed compiled by default. This primarily fixes [rails issue #35501](https://github.com/rails/rails/issues/35501) as well as [numerous other webpacker issues](https://github.com/rails/webpacker/issues/2131#issuecomment-581618497). The disabled loader can still be required explicitly via:

  ```js
  const nodeModules = require('@rails/webpacker/rules/node_modules.js')
  environment.loaders.append('nodeModules', nodeModules)
  ```

- If you have added `environment.loaders.delete('nodeModules')` to your `environment.js`, this must be removed or you will receive an error (`Item nodeModules not found`).
- `extract_css` option was removed. Webpacker will generate a separate `application.css` file for the default `application` pack, as supported by multiple files per entry introduced in 5.0.0. [#2608](https://github.com/rails/webpacker/pull/2608). However, CSS will be inlined when the webpack-dev-server is used with `hmr: true`. JS package exports `inliningCss`. This is useful to enable HMR for React.
- Webpacker's wrapper to the `splitChunks()` API will now default `runtimeChunk: 'single'` which will help prevent potential issues when using multiple entry points per page [#2708](https://github.com/rails/webpacker/pull/2708).
- Changes `@babel/preset-env` modules option to `'auto'` per recommendation in the Babel docs [#2709](https://github.com/rails/webpacker/pull/2709)
- Adds experimental Yarn 2 support. Note you must manually set `nodeLinker: node-modules` in your `.yarnrc.yml`.
- Fixes dev server issues [#2898](https://github.com/rails/webpacker/pull/2898)
- Update static files path to from `media/` to `static/`.
- Deprecated configuration option `watched_paths`. Use `additional_paths` instead in `webpacker.yml`.

### Breaking changes
- Renamed `/bin/webpack` to `/bin/webpacker` and `/bin/webpack-dev-server` to `bin/webpacker-dev-server` to avoid confusion with underlying webpack executables.
- Removed integration installers
- Splitchunks enabled by default
- CSS extraction enabled by default, except when devServer is configured and running


[Unreleased]: https://github.com/shakacode/shakapacker/compare/6.0.0-rc.14...master
[v6.0.0.rc.14]: https://github.com/shakacode/shakapacker/compare/v6.0.0-rc.13...v6.0.0-rc.14
[v6.0.0.rc.13 changes from v6.0.0.rc.6]: https://github.com/shakacode/shakapacker/compare/aba79635e6ff6562ec04d3c446d57ef19a5fef7d...v6.0.0-rc.13
[v6.0.0.rc.6 changes from v5.4]: https://github.com/rails/webpacker/compare/v5.4.3...aba79635e6ff6562ec04d3c446d57ef19a5fef7d

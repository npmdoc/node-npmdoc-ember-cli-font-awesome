# api documentation for  [ember-cli-font-awesome (v1.5.2)](https://github.com/martndemus/ember-cli-font-awesome#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-ember-cli-font-awesome.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-ember-cli-font-awesome) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-ember-cli-font-awesome.svg)](https://travis-ci.org/npmdoc/node-npmdoc-ember-cli-font-awesome)
#### An ember-cli addon for using Font Awesome icons in Ember applications.

[![NPM](https://nodei.co/npm/ember-cli-font-awesome.png?downloads=true)](https://www.npmjs.com/package/ember-cli-font-awesome)

[![apidoc](https://npmdoc.github.io/node-npmdoc-ember-cli-font-awesome/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-ember-cli-font-awesome_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-ember-cli-font-awesome/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-ember-cli-font-awesome/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-ember-cli-font-awesome/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Marten Schilstra",
        "email": "mail@martenschilstra.nl"
    },
    "bugs": {
        "url": "https://github.com/martndemus/ember-cli-font-awesome/issues"
    },
    "dependencies": {
        "ember-cli-babel": "^5.1.5",
        "ember-computed-decorators": "0.2.2"
    },
    "description": "An ember-cli addon for using Font Awesome icons in Ember applications.",
    "devDependencies": {
        "broccoli-asset-rev": "^2.3.0",
        "ember-cli": "2.4.1",
        "ember-cli-app-version": "^1.0.0",
        "ember-cli-dependency-checker": "^1.2.0",
        "ember-cli-htmlbars": "^1.0.1",
        "ember-cli-htmlbars-inline-precompile": "^0.3.1",
        "ember-cli-inject-live-reload": "^1.3.1",
        "ember-cli-qunit": "^1.2.1",
        "ember-cli-release": "0.2.8",
        "ember-cli-sri": "^2.1.0",
        "ember-cli-uglify": "^1.2.0",
        "ember-disable-prototype-extensions": "^1.1.0",
        "ember-disable-proxy-controllers": "^1.0.1",
        "ember-export-application-global": "^1.0.5",
        "ember-load-initializers": "^0.5.0",
        "ember-resolver": "^2.0.3",
        "ember-suave": "1.2.3",
        "ember-try": "^0.1.2",
        "loader.js": "^4.0.0"
    },
    "directories": {
        "doc": "doc",
        "test": "tests"
    },
    "dist": {
        "shasum": "d8a911c274c7ba0fe70171ae15983f782c52d507",
        "tarball": "https://registry.npmjs.org/ember-cli-font-awesome/-/ember-cli-font-awesome-1.5.2.tgz"
    },
    "ember-addon": {
        "configPath": "tests/dummy/config",
        "before": [
            "ember-cli-sass",
            "ember-cli-less"
        ]
    },
    "engines": {
        "node": ">= 0.12.0"
    },
    "gitHead": "c17c39a329489755dfbaacbbfcbe80ef6443b0b3",
    "homepage": "https://github.com/martndemus/ember-cli-font-awesome#readme",
    "keywords": [
        "ember-addon"
    ],
    "license": "Unlicense",
    "maintainers": [
        {
            "name": "lfridael",
            "email": "laurens.fridael@gmail.com"
        },
        {
            "name": "martndemus",
            "email": "mail@martenschilstra.nl"
        }
    ],
    "name": "ember-cli-font-awesome",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/martndemus/ember-cli-font-awesome.git"
    },
    "scripts": {
        "build": "ember build",
        "start": "ember server",
        "test": "ember try:testall"
    },
    "version": "1.5.2"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module ember-cli-font-awesome](#apidoc.module.ember-cli-font-awesome)
1.  [function <span class="apidocSignatureSpan">ember-cli-font-awesome.</span>included (app, parentAddon)](#apidoc.element.ember-cli-font-awesome.included)
1.  [function <span class="apidocSignatureSpan">ember-cli-font-awesome.</span>init (app)](#apidoc.element.ember-cli-font-awesome.init)
1.  string <span class="apidocSignatureSpan">ember-cli-font-awesome.</span>name



# <a name="apidoc.module.ember-cli-font-awesome"></a>[module ember-cli-font-awesome](#apidoc.module.ember-cli-font-awesome)

#### <a name="apidoc.element.ember-cli-font-awesome.included"></a>[function <span class="apidocSignatureSpan">ember-cli-font-awesome.</span>included (app, parentAddon)](#apidoc.element.ember-cli-font-awesome.included)
- description and source-code
```javascript
included = function (app, parentAddon) {

  // Quick fix for add-on nesting
  // https://github.com/ember-cli/ember-cli/issues/3718
  // https://github.com/aexmachina/ember-cli-sass/blob/v5.3.0/index.js#L73-L75
  if (typeof app.import !== 'function' && app.app) {
    this.app = app = app.app;
  }


  // https://github.com/ember-cli/ember-cli/issues/3718#issuecomment-88122543
  this._super.included.call(this, app);


  // Per the ember-cli documentation
  // http://ember-cli.com/extending/#broccoli-build-options-for-in-repo-addons
  var target = (parentAddon || app);
  target.options = target.options || {}; // Ensures options exists for Scss/Less below
  var options = target.options.emberCliFontAwesome || {};


  var faPath = path.join(target.bowerDirectory, 'font-awesome');
  var scssPath = path.join(faPath, 'scss');
  var lessPath = path.join(faPath, 'less');
  var cssPath = path.join(faPath, 'css');
  var fontsPath = path.join(faPath, 'fonts');


  // Ensure the font-awesome path is added to the ember-cli-sass addon options
  // (Taking a cue from the Babel options above)
  if (options.useScss) {
    target.options.sassOptions = target.options.sassOptions || {};
    target.options.sassOptions.includePaths = target.options.sassOptions.includePaths || [];
    if (target.options.sassOptions.includePaths.indexOf(scssPath) === -1) {
      target.options.sassOptions.includePaths.push(scssPath);
    }
  }


  // Ensure the font-awesome path is added to the ember-cli-less addon options
  // (Taking a cue from the Babel options above)
  if (options.useLess) {
    target.options.lessOptions = target.options.lessOptions || {};
    target.options.lessOptions.paths = target.options.lessOptions.paths || [];
    if (target.options.lessOptions.paths.indexOf(lessPath) === -1) {
      target.options.lessOptions.paths.push(lessPath);
    }
  }


  // Make sure font-awesome is available
  if (!fs.existsSync(faPath)) {
    throw new Error(
      this.name + ': font-awesome is not available from bower (' + faPath + '), ' +
      'install it into your project by running 'bower install font-awesome --save''
    );
  }


  // Early out if no assets should be imported
  if ('includeFontAwesomeAssets' in options && !options.includeFontAwesomeAssets) {
    return;
  }


  // Import the css when Sass and Less are NOT used
  if (!options.useScss && !options.useLess) {
    target.import({
      development: path.join(cssPath, 'font-awesome.css'),
      production: path.join(cssPath, 'font-awesome.min.css')
    });
  }


  // Import all files in the fonts folder when option not defined or enabled
  if (!('includeFontFiles' in options) || options.includeFontFiles) {
    fs.readdirSync(fontsPath).forEach(function(fontFilename){
      target.import(
        path.join(fontsPath, fontFilename),
        { destDir:'/fonts' }
      );
    });
  }

}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.ember-cli-font-awesome.init"></a>[function <span class="apidocSignatureSpan">ember-cli-font-awesome.</span>init (app)](#apidoc.element.ember-cli-font-awesome.init)
- description and source-code
```javascript
init = function (app) {

  // Enable ES7 decorators via Babel
  // https://www.npmjs.com/package/ember-computed-decorators#setup-with-addon
  this.options = this.options || {};
  this.options.babel = this.options.babel || {};
  this.options.babel.optional = this.options.babel.optional || [];
  if (this.options.babel.optional.indexOf('es7.decorators') === -1) {
    this.options.babel.optional.push('es7.decorators');
  }

}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)

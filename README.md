CIMB Clicks
===========

HTML templates and mobile app for My CIMB Clicks 

### Table of Contents:

- [CIMB Clicks](#markdown-header-cimb-clicks)
        - [Table of Contents:](#markdown-header-table-of-contents)
    - [USEFUL LINKS](#markdown-header-useful-links)
    - [GETTING STARTED WITH DEVELOPMENT](#markdown-header-getting-started-with-development)
    - [TECHNICAL SOLUTIONS](#markdown-header-technical-solutions)
        - [DEVELOPMENT DEPENDENCIES](#markdown-header-development-dependencies)
        - [VERSIONS](#markdown-header-versions)
    - [MOBILE FIRST APPROACH](#markdown-header-mobile-first-approach)
    - [FOLDER STRUCTURE](#markdown-header-folder-structure)
    - [CONVENTIONS & BEST PRACTICES](#markdown-header-conventions-&-best-practices)
        - [Recommended SublimeText plugins:](#markdown-header-recommended-sublimetext-plugins)
        - [Folder and file name:](#markdown-header-folder-and-file-name)
        - [JavaScript](#markdown-header-javascript)
        - [SCSS](#markdown-header-scss)
        - [Light Weight Login Page and Dashboard Prefetching](#markdown-header-light-weight-login-page-and-dashboard-prefetching)
        - [Angular 2](#markdown-header-angular-2)
    - [BUILD & CI SERVER INSTALLATION](#markdown-header-build-&-ci-server-installation)
    - [KNOWLEDGE BASE](#markdown-header-knowledge-base)

USEFUL LINKS
------------

- Wireframe & mockup URL: http://dev.aleph-labs.com/clients/CIMB/clicks/projects/?p=CIMB%20Clicks
- Issues Tracker: http://cimb-trac.aleph-labs.com/clicks
- Client's issues tracker: http://cimbclicks-trac.aleph-labs.com/
- Style guide: http://dev.aleph-labs.com/clients/CIMB/clicks/styleguide
- Releases: http://dev.aleph-labs.com/clients/CIMB/clicks/release/
- Static demo: http://dev.aleph-labs.com/clients/CIMB/clicks/
- App demo: visit release page for demo app download

GETTING STARTED WITH DEVELOPMENT
--------------------------------
There's is a submodule in this project, __messenger__. Please sync that submodule before start building. Command to use: `git submodule update --init`

1. Software installation:
    - Sublime Text 3
    - Necessary Sublime Text 3 plugins. See below
    - Currently stable Google Chrome
    - [NodeJS][] version 4.0+ (for testing, previewing, compiling and optimizing processes)
    - [GulpJS][] commandline tool: `npm install --global gulp`
    - Java SDK (for MFP CLI)
    - Mobile First Platform CLI
    - For Android dev:
        + Android SDK 21
        + ANT automation script
    - For iOS dev
        + Xcode 7
        + Xcode CLI
2. Setting up IDE/Editor
    - Install development dependencies: In terminal, cd to __this__ folder: `npm install`
    - Alternatively, if the deployment server does not have access to 
    - Open the `my-cimb-clicks.sublime-project`
4. Testing app in web browser (non-MFP):
    - Execute `gulp serve-static` to test desktop Angular HTML
    - Execute `gulp serve-app` to test Angular mobile app on browser
5. Code validation:
    - Execute `npm run eslint` to validate JavaScript code
    - Execute `npm run tslint` to validate TypeScript code
    - Execute `npm test` to execute both linters
6. Optimize source code and prepare bundle for deployment:
    - `gulp build`
7. Patch the app with Cordova / Worklight initialization scripts & copy source code to native projects:
    - `cd mfp`
    - `mfp push -n`
8. Build hybrid mobile apps:
    1. iOS:
        - Install iOS certificate and developer provisioning profile
        - Use Xcode to open mfpCimbclicksIphone.xcodeproj and archive to .ipa
    2. Android
        - Change terminal to this folder `mfp/apps/cimbclicks/android/native`
        - Execute: `ant debug`


TECHNICAL SOLUTIONS
-------------------

- [Angular][] 2.0 for the mobile app architecture
- [MobileFirst][] platform for the hybrid mobile app platform
- SASS (SCSS dialect) as CSS preprocessor
- Bootstrap as base CSS framework
- Mobile-first CSS implementation, which mean our layout styling start from mobile screens first, extra CSS to be added for tablet and desktop
- Progressive enhancement approach:
    + Rounded corner (border radius) on IE9+
    + CSS Transitions only support on IE9+
    + CSS Animations only support on IE10+
    + Icon fonts are used to have best support from old and new browsers
- Form field validation: [jQuery Validation][]
- Minimum browser's supports (as per overall TSD):
    + Safari Ver 8.x and 9.x
    + Google Chrome Ver 40.x to 46.x
    + Firefox 35.0.1 to 42.x
    + IE9.x, IE 10.x, IE 11.x, Edge
    + Opera 31 and above and __Opera Mini?__
    + iOS Ver: 7.x, 8.x, 9.x
    + Android OS: 4.1 and above, 5.x, 6.x

### DEVELOPMENT DEPENDENCIES

- [NodeJS][]
- [MobileFirst][]
- [GulpJS][]
- See _devDependencies_ in `package.json`

### VERSIONS

Below are list of main components

- Mobile First Platform: __7.1__
- Angular: __2.0 Beta 0__
- SystemJS: __0.19.9__
- jQuery: __2.1.4__
- Bootstrap: __3.3.6__

For other libraries and components, see details inside `vendor` folders

MOBILE FIRST APPROACH
---------------------

We are implement the SASS/SCSS with mobile first approach, meaning, the base direct styles are targeting mobile design. 

Styles and layout for larger screens will be added on top of that base and bundled into separated CSS files. 

With mobile first approach, the media query will have to use `min-width` to target larger screens, and the _non-@media_ styles will be targeting mobile.

Breakpoints            | Target layout
-----------            |  -------------
flat                   | core styles and mobile
min-width: 768px       | tablet layout & styles
min-width: 992px       | medium desktop layout & styles
min-width: 1200px      | large desktop layout & styles

CSS Utilities: use Bootstrap standard responsive prefixed class helpers to control visibility and column layout for different screen size:

Prefix   | Target Layout
------   | -------------
`none`   | default 1-column mobile layout
`-xs-`   | mobile screen
`-sm-`   | tablet screens --> use this to apply for tablet and above
`-md-`   | medium desktop screens --> use this to apply for desktop and above
`-lg-`   | large desktop screens

FOLDER STRUCTURE
----------------

_Folder structure is WIP_

    /                           : project / git root
    +-- private                 : folder for development assets like editable
    PSDs, build templates, icon font sources...
        +-- iconfont-templates  : templates for iconfont generator
        +-- icons               : all the SVG source files for iconfont
        generator
        +-- styleguide-template : templates for styleguide generator
    +-- html                    : Front End source for desktop website and all
    base components
        +-- styles              : SASS (SCSS) source, 
            +-- vendor          : 3rd party CSS / SCSS framework
        +-- scripts             : source for Angular app code (TypeScript and the like)
            +-- app             : the Angular app source
            +-- typings         : TypeScript definitions for libraries, it is to assist type and class checking in editor (not used to check during compilation for now)
            +-- vendor          : 3rd-party libraries, used specifically by Angular app, including Angular library itself
        +-- fonts               : icons and web fonts
        +-- img                 : UI image assets
        +-- js                  : vanilla JS source code
            +-- vendor          : non-Angular 3rd party JS code
        +-- mock                : mock resources and data for app dev and demo
    +-- app                     : Angular source and app configuration for mobile app
        +-- scripts             : mobile only app source code
    +-- ~dist                   : folder for build outputs (should not be checked in)
        +-- html                : desktop build and bundles
        +-- app                 : mobile app build and bundles
    +-- styleguide              : auto-generated styleguide output (should not
        be checked in)
    +-- mfp                     : Mobile First Platform's service adapters and platform specific projects
        +-- adapters            : service adapters
        +-- apps                : native app build targets
            +-- CIMBClicksMY    : native app for CIMB Clicks Malaysia
            +-- CIMBClicksSG    : native app for CIMB Clicks Singapore


CONVENTIONS & BEST PRACTICES
----------------------------

### Recommended SublimeText plugins:
- Babel
- EditorConfig
- Emmet
- GitGutter
- SCSS
- Select Quoted
- SublimeLinter
- SublimeLinter-contrib-eslint
- SublimeLinter-contrib-scss-lint
- SublimeLinter-contrib-tslint
- Terminal
- TypeScript

### Folder and file name:
- Use lower kebab-case for all folder names
- Use lower kebab-case for all file names except
    + PascalCase for Class and Singleton JavaScript files
    + PascalCase for single-class-exporting TypeScript/ES6 module files

### JavaScript
- Our convention is based on [Google JavaScript Style Guide][]
- Alignment by TABs (not SPACES, tab width is up to user's preference, but 4-space tab is recommended)
- Single quotes ('...') for String literal in js files
- Variable Naming:
    + Prefix property name with `_` (underscore) if it is intended as private and should not be used outside of the class
    + Prototypes, classes (base objects that are used to spawn instances) are named with __PascalCase__ (Pin, PinBoard)
    + Global objects, singleton and static objects are named with __PascalCase__ (DataModel, AppView, Templates)
    + Object instances are named with __camelCase__ (pin, pinBoard)
    + Prefix jQuery object variables with `$` sign so it is easier to differentiate jQuery objects with HTML element reference and other variable types. Example: `$view, $el, $scene`
    + Declare variables at top of functions, group variables which are not initializeed with values into a one-liner `var` statement
    ```JavaScript
        var a, b, c;
        var name = 'Default';
        var age = 20;
    ```
- Functions:
    + For local functions, prefer function declaration (`function doSomething() {}`) to function expression (`var doSomething = function() {}`)
    + Prefix function name with 'on' if it is an ordinary event handling function
    + Prefix function name with '_' if it is intended as private and should not be used outside of the class
- Unless required, local variable for `this` reference: name it `self`. Besides, consider using Function.prototype.bind(this) whenever applicable.
- Avoid using global jQuery `$(selector)` in View components, use local `$el.find(selector)` OR the shortcut `this.$(selector)` (where applicable) instead
- _eslint_ __MUST BE USED__ to validate JavaScript syntax to maintain sanity & clarity of the code.
    Refer to `.eslintrc` for detailed global rules
- Comment and documentation:
    + Comment every module/class
    + Comment every public function
    + Explicitly mark a function with `@override` if it is an override function
    + Make use of [JSDoc][] syntax for auto-documentation generation later

### SCSS
- __Linter__: We're using `scss-lint` as linter for .scss files, rules are defined in `.scss-lint.yml`
- __Comments__: 
    + Every CSS component/file (at high level)
    + Use [KSS][] annotations for styleguide components
- __OOCSS__:
    + NO IDs in CSS
    + Avoid attaching classes to elements (i.e. don’t do div.header or h1.title)
    + Except for utilitily classes, avoid using !important
    + Separate structure and skin: define repeating visual features (like background and border styles) as separate “skins” that you can mix-and-match
    + Separate container and content: rarely use location-dependent styles, an object should look the same no matter where you put it.
- __Autoprefixer__: Don't add browser prefixes by yourself, let the autoprefixr (part of `gulp styles` task) do it for you.
- Prefix underscore `_` to name SCSS files which are not supposed to be compiled separately.

### Light Weight Login Page and Dashboard Prefetching 

One of the critical requirements of the project is the login and register page must be lightweight. Hence we are considering __implement non-Angular login page__.

Since Dashboard page is the de facto landing page after login, we will use [link prefetch](https://developer.mozilla.org/en-US/docs/Web/HTTP/Link_prefetching_FAQ) technique to preload and cache as much resource from dashboard page.

### Angular 2

- Use single (') quotes for `templateUrl` properites in components since the template inlining script only recognize ES5 quotes.

BUILD & CI SERVER INSTALLATION
------------------------------
- [NodeJS][]: To be able to run all the build scripts and automation services. NodeJS comes with `npm` and `node` CLI.
    + Installation: Follow the guide at [NodeJS][] home page to take the most suitable installation approach for the server's OS and infrastructure
- [GulpJS][]: Main CLI command to execute the build scripts
    + Installation: `$ npm install --global gulp`
    + Corrupted Installation or missing dependecies or version error installations? 
        + `rm -rf node_modules/`
        + `npm cache clean`
        + `npm install`
    + Notes: 
        + `$ npm` installation requires Internet connection
        + `$ npm install --global` often requires Administrator permission
- Node packages dependecies: those dependencies are required for gulp build and code validation scripts.
    + Installation: `$ npm install` in the project folder (propably through Jenkin Shell build step)
    + If no internet access, a preinstalled `node_modules` folder must be provided.

KNOWLEDGE BASE
--------------

1. Angular 2.0 Cheatsheet: https://angular.io/docs/ts/latest/guide/cheatsheet.html
2. Understanding Angular's `@Component`: http://blog.thoughtram.io/angular/2015/05/03/the-difference-between-annotations-and-decorators.html
3. Angular mistakes to avoid for mantainability and scalability, for Angular 1, but some applicable for Angular 2: https://www.airpair.com/angularjs/posts/top-10-mistakes-angularjs-developers-make
4. Style guide generator: https://github.com/kss-node/kss/
5. Angular 2 unit test with TypeScript, Karma & Jasmine setup: https://dimakuzmich.wordpress.com/2015/08/21/test-angular2-now-or-how-to-set-up-angular2-unit-tests/
6. Using CLI to create, build, and manage MobileFirst project artifacts: https://developer.ibm.com/mobilefirstplatform/documentation/getting-started-7-0/advanced-client-side-development/using-cli-create-build-manage-project-artifacts/
    Known commands:
    `mfp create <project-name>` - Create new MFP project
    `mfp add hybrid cimbclicks` - Add hybrid app structure 
    `mfp add environment` - Select env. to add (follow prompts)
    `mfp push -n` - Generate all native app projects and copy the www resources to the native projects
7. Building Android app with CLI
    - Make sure environment and path to Android executables is set up
    - Make sure `ant` command is ready (either setting alias or PATH to ant's bin folder)
    - Change working dir to `mfp/apps/cimbclicks/android/native`
    - Generate the ANT script (build.xml) if not there by executing `android update project -p .`
    - Generate debug APK file to install on device: `ant debug`
8. Building iOS app with Xcode
    - Open "mfp/apps/cimbclicks/iphone/native/mfpCimbclicksIphone.xcodeproj" in Xcode
    - Go to "Build Settings" > Search for Bitcode > Set "Enable Bitcode" to "No"
    - If build fail because of Cordova, add the following line to your Build Settings -> Header Search Paths: "$(OBJROOT)/UninstalledProducts/$(PLATFORM_NAME)/include"
    - To update iOS's bundle ID, update from `application-descriptor.xml` and rerun `mfp push -n`
    - Select appropriate provisioning profile
    - Generate archive from build menu
9. (Trivial) Run Unix shell command in Jenkin Script Console:
    `println new ProcessBuilder('sh','-c','shell script here').redirectErrorStream(true).start().text`
10. Configure Jenkin Sonarqube runner: follow [the instructions](http://docs.sonarqube.org/display/SONAR/Analyzing+with+SonarQube+Scanner+for+Jenkins#AnalyzingwithSonarQubeScannerforJenkins-Installation)
    - For server: make sure the address is: http://localhost:9000
    - For runner: add a default runner with version 2.3+
    - At build job: Add a build step from dropdown "Invoke Standalone Sonar Analysis" and leave everything by default
11. All CI knowledge:
    - In order to push build number tag to origin from CI:
        + Add this shell script line to a shell build step as first step: `git config --global credential.helper 'cache --timeout 900'`
        + At the Git source code management, make sure the credentials used have the right to push to remote repository.
        + Add a git publisher to post-build actions with following parameters:
            * Push Only If Build Succeeds ✓
            * Tag to push: `test-build-$BUILD_NUMBER`
            * Create new tag ✓
            * Target remote name: `origin`
12. Status bar color configuration for iOS
    - Add these line in config.xml:
        `<preference name="DisallowOverscroll" value="true" />`
        `<preference name="StatusBarOverlaysWebView" value="false" />`
        `<preference name="StatusBarBackgroundColor" value="#333333" />`
        `<preference name="StatusBarStyle" value="lightcontent" />`
        Possible values for __StatusBarStyle__: lightcontent, blacktranslucent, blackopaque
    - Add these config in XCode project main .plist file:
        + __Status bar is initially hidden__: NO
        + __View controller-based status bar appearance__: NO
    - To avoid content overlapping status bar:
        + In __wlInitOptions__, set `showIOS7StatusBar: false` (in __mfp-init.js__)
13. Delete multiple remote branch in Git: http://stackoverflow.com/questions/10555136/delete-multiple-remote-branches-in-git
    Check the answer by Dmitriy        
14. Package required to build new Android app with Gradle: Start Android SDK Manager > look for these packages at Extras
    - Android Support Repository
    - Android Support Library
    - Google Play Service
    - Google Repository
15. Upgrade Angular Forms to new API: https://www.barbarianmeetscoding.com/blog/2016/07/15/updating-your-angular-2-app-to-use-the-new-forms-api-a-practical-guide/



[Angular]: https://angular.io
[GulpJS]: http://gulpjs.com/
[Google JavaScript Style Guide]: http://google.github.io/styleguide/javascriptguide.xml
[jQuery]: http://jQuery.com
[jQuery Validation]: http://jqueryvalidation.org
[JSDoc]: http://usejsdoc.org/
[MobileFirst]: https://developer.ibm.com/mobilefirstplatform/
[NodeJS]: http://nodejs.org/
[Normalize.css]: http://necolas.github.io/normalize.css/
[KSS]: https://github.com/kss-node/kss/blob/spec/SPEC.md

# Bootstrap-Gulp
Customizing your Bootstrap / MDBootstrap project (creating your custom Bootstrap / MDBootstrap package only with the components you really need)

# Installation
1. Install [NodeJs](https://nodejs.org/en/)
2. Install [Git Bash](https://git-scm.com/downloads)
3. Install Gulp globally

	```
	npm install gulp -g
	```
4. Downloading [MDB-Gulp-Package](https://mdbootstrap.com/download/mdb-jquery/mdb-gulp-free/4510akkBX7PNghRC6EIE/MDB-Gulp-Free_4.5.10.zip). Unzip the package

# Gulp Project
Create a gulp project using git bash or cmd

```
npm init
```

You will be asked to enter the project details, or just leave them blank and press 
enter. A new file ```package.json``` will be created.

Run another command storing gulp locally in project directory

```
npm install --save-dev gulp
```

Some more dependencies for our project are to be installed

```
npm install --save-dev gulp-sass gulp-autoprefixer gulp-cssmin browser-sync gulp-concat gulp-minify gulp-rename gulp-imagemin
```

We'll talk in details about each of these plugins in the steps below. Right now we 
just need to install them.

# Launching The Project And Live Server
Run the server using
```
gulp mdb-go
```

If that gives any error like

```
'gulp' is not recognized as an internal or external command,operable program or batch file.
```

then you might don't have the npm folder in path, to add it simply open 
**system environment variables** and select path and **add new** In there paste the path
for your npm folder which lies in 
```C:\Users\[MyWindowsUserName]\AppData\Roaming\npm```

If still that doesn't work try running this command from **cmd**

```
PATH=%PATH%;C:\Users\[MyWindowsUserName]\AppData\Roaming\npm
```

Now the error are solvedm, run gulp again and you should get some response

Go inside MDB-Gulp folder and run 

```
gulp mdb-go
```

A new browser window will open. In there click on ```index.html``` file and you should see
the webpage. 

## Removing Useless Dependencies
Open ```MDB-Gulp-Free_4.5.10\scss\mcd.scss``` file in your text editor. You should see many
imports. 

```
@charset "UTF-8";

// Bootstrap
@import "core/bootstrap/functions";
@import "core/bootstrap/variables";

// CORE
@import "core/mixins";
// Your custom variables
@import "custom-variables";
@import "core/colors";
@import "core/variables";
@import "core/global";
@import "core/helpers";
@import "core/typography";
@import "core/masks";
@import "core/waves";

// FREE
@import "free/animations-basic";
@import "free/animations-extended";
@import "free/buttons";
@import "free/cards";
@import "free/dropdowns";
```

Try removing ```@import "free/animations-extended";``` from

```
@import "free/animations-basic";
@import "free/animations-extended";
@import "free/animations-basic";
```

and save the file, look at the console and you should see new messages appearing like

```
[08:35:24] Starting 'css-compile'...
[08:35:24] Finished 'css-compile' after 5.92 ms
[08:35:27] Starting 'css-minify'...
[08:35:27] Finished 'css-minify' after 4.81 ms
[Browsersync] Reloading Browsers...
[Browsersync] Reloading Browsers...

```

What gulp does is compile the css files then minifies those files and reloads the browser, 
all of this by itself, this is the beauty of gulp.

# SASS dependencies

Some of the components require other components to work properly. That's why we have created a map of dependencies.

**Please note:**

1. All the components require core files. If you decide to remove any of the core files you 
risk a conflict.

2. If you remove any of the Free or Pro components - be sure it's not a dependency of any 
other component.

3. If you remove the dependency any of the Free or Pro components - be aware that's 
possible it may won't work 100% properly.

If you read the instructions given above the mdb.scss file you should get details of the 
dependencies.

```
Legend:

'-->' means 'required'

All free and pro files require files from 'core' catalog

'none' means 'this component doesn't require anything except core files'

A file wrapped by `< >` means that this file make the base component prettier but it isn't necessary for the proper working

All PRO components require 'pro/_variables.scss' file
```

# Compiling Javascript Files
Open ```\MDB Gulp Free\js\modules.js``` file in your code editor.

The same as with SASS files - just remove or comment the component you don't need and save 
the file.

```
[08:52:00] Starting 'js-build'...
[08:52:00] Finished 'js-build' after 13 ms
[08:52:01] Starting 'js-minify'...
[08:52:01] Finished 'js-minify' after 3.35 ms

```

After saving the file MDBootstrap gulp package compile new mdb.js and mdb.js.css files.

If you open these files within the ```\dist\js\``` you will notice they don't contain 
removed components. 

## Javascript Dependencies

```
Legend:

'-->' means 'required'

All files require jQuery and bootstrap.js

js/
├── dist/
│   ├── buttons.js
│   ├── cards.js
│   ├── character-counter.js
│   ├── chips.js
│   ├── collapsible.js --> vendor/velocity.js
│   ├── dropdown.js --> Popper.js, jquery.easing.js
│   ├── file-input.js
│   ├── forms-free.js
│   ├── material-select.js --> dropdown.js
│   ├── mdb-autocomplete.js
│   ├── preloading.js
│   ├── range-input.js --> vendor/velocity.js
│   ├── scrolling-navbar.js
│   ├── sidenav.js --> vendor/velocity.js, vendor/hammer.js, vendor/jquery.hammer.js
│   └── smooth-scroll.js
├── _intro-mdb-pro.js
├── modules.js
├── src/
│   ├── buttons.js
│   ├── cards.js
│   ├── character-counter.js
│   ├── chips.js
│   ├── collapsible.js --> vendor/velocity.js
│   ├── dropdown.js --> Popper.js, jquery.easing.js
│   ├── file-input.js
│   ├── forms-free.js
│   ├── material-select.js --> dropdown.js
│   ├── mdb-autocomplete.js
│   ├── preloading.js
│   ├── range-input.js --> vendor/velocity.js
│   ├── scrolling-navbar.js
│   ├── sidenav.js --> vendor/velocity.js, vendor/hammer.js, vendor/jquery.hammer.js
│   └── smooth-scroll.js
└── vendor/
    ├── addons/
    │   ├── datatables.js
    │   └── datatables.min.js
    ├── chart.js
    ├── enhanced-modals.js
    ├── hammer.js
    ├── jarallax.js
    ├── jarallax-video.js --> vendor/jarallax.js
    ├── jquery.easing.js
    ├── jquery.easypiechart.js
    ├── jquery.hammer.js --> vendor/hammer.js
    ├── jquery.sticky.js
    ├── lightbox.js
    ├── picker-date.js --> vendor/picker.js
    ├── picker.js
    ├── picker-time.js --> vendor/picker.js
    ├── scrollbar.js
    ├── scrolling-navbar.js
    ├── toastr.js
    ├── velocity.js
    ├── waves.js
    └── wow.js
```

**Before removing anything from javascript modules please refer to the map of dependencies 
for javascript.**

#  Project psd-to-html.

###  Simple one page website to practise HTML and CSS skills.

#### Demo [here](https://codeitsmyjob.github.io/psd-to-html/dist/)

####  Technologies used:
-  HTML;
-  CSS.

## Build Setup:

``` bash
# Download repository:
git clone https://github.com/codeitsmyjob/psd-to-html.git

# Go to the app:
cd psd-to-html

# Install dependencies:
npm install

# Server with hot reload at http://localhost:8081/
npm run dev

# Output will be at dist/ folder
npm run build
```

## Project Structure:

* `src/pug/layout` - put custom layout for pages
* `src/pug/includes` - all app includes
* `src/pug/utils` - pug mixins and other
* `src/pug/pages` - put custom app pages. Don't forget to import them in `index.js`
* `src/assets/scss` - put custom app SCSS styles here. Don't forget to import them in `index.js`
* `src/assets/css` - the same as above but CSS here. Don't forget to import them in `index.js`
* `src/assets/img` - put images here. Don't forget to use correct path: `assets/img/some.jpg`
* `src/js` - put custom app scripts here
* `src/index.js` - main app file where you include/import all required libs and init app
* `src/components` - folder with custom `.vue` components
* `static/` - folder with extra static assets that will be copied into output folder

<div align="center">
  <h2>Settings:</h2>
</div>

## Main const:
Easy way to move all files.
Default:
``` js
const PATHS = {
  // Path to main app dir
  src: path.join(__dirname, '../src'),
  // Path to Output dir
  dist: path.join(__dirname, '../dist'),
  // Path to Second Output dir (js/css/fonts etc folder)
  assets: 'assets/'
}
```
## Customize:
Change any folders:
``` js
const PATHS = {
  // src must be src
  src: path.join(__dirname, '../src'),
  // dist to public
  dist: path.join(__dirname, '../public'),
  // assets to static
  assets: 'static/'
}
```

## Import js files:
1. Create another js module in `./js/` folder
2. Import modules in `./js/index.js` file
``` js
// another js file for example
import './common.js'
```

## PUG Dir Folder:
#### Default:
* .pug dir: `./pug/pages`
* Configurations: in `./build/webpack.base.conf.js`
**Usage:**
All files must be created in the `./pug/pages` folder.
Example:
``` bash
./pug/pages/index.pug
./pug/pages/about.pug
```

#### Change PUG Default Dir Folder:
Example for `./pug/mynewfolder/pages`:
* Change `./build/webpack.base.conf.js` const PAGES_DIR:
``` js
// Your new path
const PAGES_DIR = `${PATHS.src}/pug/mynewfolder/pages/`
```
3. Rerun webpack dev server

## Create Another PUG Files:
#### Default: 
Automatic creation any pug pages:
1. Create another pug file in `./pug/pages/`
2. Open new page `http://localhost:8081/about.html` (Don't forget to RERUN dev server)

#### Second method:
Manual (not Automaticlly) creation any pug pages (Don't forget to RERUN dev server and COMMENT lines above)
1. Create another pug file in `./pug/pages/`
2. Go to `./build/webpack.base.conf.js`
3. Comment lines above (create automaticlly pug pages)
4. Create new page in pug:
``` js
    new HtmlWebpackPlugin({
      template: `${PAGES_DIR}/about/index.pug`,
      filename: './about/index.html',
      inject: true
    }),
    new HtmlWebpackPlugin({
      template: `${PAGES_DIR}/about/portfolio.pug`,
      filename: './about/portfolio.html',
      inject: true
    })
```
5. Open new page `http://localhost:8081/about.html` (Don't forget to RERUN dev server)

#### Third method: (BEST)
Сombine the first method and the second.
Example:
``` js
    ...PAGES.map(page => new HtmlWebpackPlugin({
      template: `${PAGES_DIR}/${page}`,
      filename: `./${page.replace(/\.pug/,'.html')}`
    }))
    new HtmlWebpackPlugin({
      template: `${PAGES_DIR}/about/index.pug`,
      filename: './about/index.html',
      inject: true
    })
```

## Add Fonts:
Add @font-face in `/assets/scss/utils/fonts.scss`:

``` scss
// Example with Helvetica
@font-face {
  font-family: "Helvetica-Base";
  src: url('/assets/fonts/Helvetica/Base/Helvetica-Base.eot'); /* IE9 Compat Modes */
  src: url('/assets/fonts/Helvetica/Base/Helvetica-Base.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
       url('/assets/fonts/Helvetica/Base/Helvetica-Base.woff') format('woff'), /* Pretty Modern Browsers */
       url('/assets/fonts/Helvetica/Base/Helvetica-Base.ttf')  format('truetype'), /* Safari, Android, iOS */
       url('/assets/fonts/Helvetica/Base/Helvetica-Base.svg') format('svg'); /* Legacy iOS */
}
```

Add vars for font in `/assets/scss/utils/vars.scss`:

``` scss
$mySecontFont : 'Helvetica-Base', Arial, sans-serif;
```

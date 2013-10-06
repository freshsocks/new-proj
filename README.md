Fresh Start
==============

A nodejs base app to start fresh from.

Includes
========

### Node Modules
* express
* jade
* stylus
* socket.io

### Bower Components
* d3
* gumby
* jquery
* modernizr
* underscore

Install
=======
```
git clone git://github.com/stevefloat/freshstart
```
```
cd freshstart
```
```
npm install
```
```
cd public
```
```
bower install
```
```
cd .. && node app
```

### Using Gumby

[Gumby](http://gumbyframework.com/) is a nice UI framework similar to Twitter's bootstrap. However, unlike bootstrap, its a pain in the gonads to [set up](http://gumbyframework.com/docs/). Gumby is very exsensible and flexible, as long as you have ruby ~1.9+ installed with sass, compass and modular-scale gems installed.

Gumby doesn't install nicely by just ``` bower install gumby ```, Gumby actually has it's own way of building and compiling using something called [Claymate](http://gumbyframework.com/docs/claymate/), which can be installed globally via npm. See, pain in the nads.

The reason for Claymate is that Gumby needs to compile the css using Compass, and needs to move files around to a bunch of different directories in order for Gumby to actually be used. So claymate jsut does that for you. In the case of **fresh start**, the directories are already set up, so Claymate is not an issue.

However, in the ``` /public/scss/ ``` directory, there are a few sass/compass files that are there for extending Gumby or changing some of the global Gumby variable, such as font sizes, colors, columns, etc. Gumby is already compiled into the ``` /public/css/gumby.css ``` file and it ready to use with out-of-the-box settings.

If you want to [customize some of the settings in Gumby](http://gumbyframework.com/docs/mixins/), you would do so by editing the files in ``` /public/scss/ ``` and then running the following in the ``` /public/ ``` directory:
```
compass compile
```
> **NOTE**
> <br><br>
> The css file that Gumby generates uses __Open Sans__ as the default font through an ``` @import ``` targeting Google Fonts. However, the URL is always incomplete upon compiling (missing an "http:" prefix), resulting in a missing font.
> <br><br>
> _I have taken the liberty of adding the "http:" prefix to the ``` @import ``` on the first line of ``` /public/css/gumby.css ``` so the fonts load properly._

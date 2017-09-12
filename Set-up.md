## I. Grunt Environment Variable 

#### Vào This PC --> properties --> Advanced system setting --> Advanced --> Environment Variables --> Path --> Edit --> this Pass in path : 


```
C:\Ruby23-x64\bin;

C:\Program Files\nodejs;

C:\Users\Dao.DC\AppData\Roaming\npm;

C:\Users\Dao.DC\AppData\Roaming\npm\node_modules\grunt-cli\bin;

C:\Users\Dao.DC\AppData\Roaming\npm\node_modules\grunt\bin;
```

## II. Set Up Project Environment 

## install
for this project ,plz install following soft

* git
* ruby
* scss
* compass
* node
* bower
* grunt

***

#### Git

https://git-scm.com/downloads

**success**

Open git base, start type the command code.

***

#### ruby

https://www.ruby-lang.org/en/downloads/

**success**

enable to use `ruby` command 

e.g.

`ruby -v`

ruby 2.2.0p0 (2014-12-25 revision 49005) [x86_64-darwin14]


***

#### scss

http://sass-lang.com/install

`$ gem install scss`

**success**

enable to use `scss` command

e.g.

`scss -v`

Sass 3.4.22 (Selective Steve)

***

#### compass

http://compass-style.org/install/

`$ gem install compass`

**success**

enable to use `compass` command

e.g.

`compass -v`

Compass 1.0.3 (Polaris)

***

#### node

https://nodejs.org/en/

**success**

enable to use `node` command

`node -v`

v0.12.5

`npm -v`

2.11.2

***

#### bower

http://bower.io/

`npm install bower -g`

**success**

enable to use `bower` command

`bower -v`

1.4.1

***

#### grunt

http://gruntjs.com/getting-started

`npm install -g grunt-cli`

**success**

enable to use `grunt` command

e.g.

`grunt -v `

grunt-cli@1.2.0



## set up

when just clone this project ,the directory structure is like ↓

```
moc/
├── asset
│   ├── build
│   │   ├── css
│   │   ├── js
│   │   └── moc
│   └── dev
│       ├── javascript
│       ├── moc
│       └── stylesheet
```

frontend's work space is moc/

and input ↓ commond
```
npm install
grunt dev
```
then the directory structure ↓is like

```
.
moc
├── asset
│   ├── build
│   │   ├── css
│   │   ├── js
│   │   └── html
│   └── dev
│       ├── javascript
│       ├── html
│       └── stylesheet
├── bower_components
├── node_modules

```
**success**

set up is successed if the directory 'asset/build/moc/' has new html .

after that plz ↓

```
grunt server
```
if success you can access　↓

http://localhost:9003
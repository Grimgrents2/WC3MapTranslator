<p align='center'>
  <b>WC3MapTranslator</b><br/>
  Translate <code>war3map</code> ⇄ <code>json</code> formats for WarCraft III .w3x maps
</p>
<p align='center'>
  <a href='https://www.npmjs.com/package/wc3maptranslator'>
    <img src='https://badge.fury.io/js/wc3maptranslator.svg?style=flat-square'/>
  </a>
  <a href='https://www.npmjs.com/package/wc3maptranslator'>
    <img src='https://img.shields.io/npm/dt/wc3maptranslator.svg'/>
  </a>
  <a href='https://opensource.org/licenses/MIT'>
    <img src='https://img.shields.io/badge/license-MIT-blue.svg'/>
  </a>

  <p align='center'>
    <b>Quality</b><br/>
    <a href='https://travis-ci.org/ChiefOfGxBxL/WC3MapTranslator'>
      <img src='https://travis-ci.org/ChiefOfGxBxL/WC3MapTranslator.svg?branch=master' />
    </a>
    <a href='http://packagequality.com/#?package=wc3maptranslator'>
      <img src='http://npm.packagequality.com/shield/wc3maptranslator.svg' />
    </a>
    <a href='https://codeclimate.com/github/ChiefOfGxBxL/WC3MapTranslator'>
      <img src='https://api.codeclimate.com/v1/badges/065fcb3a010c892f3813/maintainability' />
    </a>
    <br/>
    <a href='https://coveralls.io/github/ChiefOfGxBxL/WC3MapTranslator?branch=master'>
      <img src='https://coveralls.io/repos/github/ChiefOfGxBxL/WC3MapTranslator/badge.svg?branch=master' />
    </a>
    <a href="https://snyk.io/test/github/chiefofgxbxl/wc3maptranslator?targetFile=package.json">
      <img src="https://snyk.io/test/github/chiefofgxbxl/wc3maptranslator/badge.svg?targetFile=package.json" alt="Known Vulnerabilities" data-canonical-src="https://snyk.io/test/github/chiefofgxbxl/wc3maptranslator?targetFile=package.json" style="max-width:100%;">
    </a>
  </p>
</p>

<hr/>
<p align='center'>
  <a href="#overview"><strong>Overview</strong></a> &middot;
  <a href="#install"><strong>Install</strong></a> &middot;
  <a href="#usage"><strong>Usage</strong></a> &middot;
  <a href="#file-support"><strong>File Support</strong></a> &middot;
  <a href="#specification"><strong>Specification</strong></a> &middot;
  <a href="#contributing"><strong>Contributing</strong></a> &middot;
  <a href="#special-thanks"><strong>Special Thanks</strong></a>
</p>
<hr/>

## Overview
WC3MapTranslator is a TypeScript module to convert between JSON and WarCraft III (.w3x) `war3map` formats. This makes the map data readable and easily modifiable, a perfect format for storing WC3 maps in Git repositories and inspecting diffs!

![TranslationExample](https://user-images.githubusercontent.com/4079034/71315302-4947fb00-2427-11ea-8f50-edf05d6e5c6a.png)

## Structures of all war3map.xxx files (use this to update the Translators, maybe add wtg translator)



> 🔗 [Guide by Hodor in russian but very good, covers all wc3 versions](https://xgm.guru/p/wc3/w3-file-format)

> 🔗 [Software by Drake53](https://github.com/Drake53/War3Net/tree/master/src/War3Net.Build.Core)

> 🔗 [Guide by Zépir](https://wc3maps.com/InsideTheW3M.html)

> 🔗 [Guide by Chocobo 1](https://www.thehelper.net/threads/guide-explanation-of-w3m-and-w3x-files.35292/)

> 🔗 [Guide by Chocobo 2](https://world-editor-tutorials.thehelper.net/cat_usersubmit.php?view=42787)

> 🔗 [Guide by Luashine](https://www.hiveworkshop.com/threads/success-hybrid-12-24-player-map-backwards-compatible-1-24-1-28-5-1-31.339722/ )

> 🔗 [Guide by HiveWE](https://github.com/stijnherfst/HiveWE/wiki/)

 
## Install
```ts
npm install wc3maptranslator
```

**Requires Node ≥ 14**  

## Usage
```ts
import {
  CamerasTranslator,
  DoodadsTranslator,
  ImportsTranslator,
  InfoTranslator,
  ObjectsTranslator,
  RegionsTranslator,
  SoundsTranslator,
  StringsTranslator,
  TerrainTranslator,
  UnitsTranslator
} from 'wc3maptranslator';

// E.g. let's create a camera for the map
const cameras = [
  {
    "target": {
      "x": -319.01,
      "y": -90.18
    },
    "offsetZ": 0,
    "rotation": 90,
    "aoa": 304,
    "distance": 2657.34,
    "roll": 5,
    "fov": 70,
    "farClipping": 5000,
    "name": "MyCamera1"
  }
]

// Now translate the JSON into the WarCraft III format
// All translators have: `.jsonToWar` and `.warToJson` functions
const translatedResult = CamerasTranslator.jsonToWar(cameras);

// `translatedResult` contains a `buffer` which can be saved to disk
// This war3map.w3c file can now be placed inside a .w3x via an MPQ
// editor, and you should now see a camera in the Camera Palette!
fs.writeFileSync('war3map.w3c', translatedResult.buffer);
```

## File Support

### World files

| Type                    | Json → War  | War → Json  | File          |
|-------------------------|:-----------:|:-----------:|---------------|
| Terrain                 | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | ![times](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | war3map.w3e      |
| Units                   | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | war3mapUnits.doo |
| Doodads                 | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | war3map.doo      |
| Regions                 | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | war3map.w3r      |
| Cameras                 | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | war3map.w3c      |
| Sounds (definitions)    | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | war3map.w3s      |

### Object data files

| Type                    | Json → War  | War → Json  | File          |
|-------------------------|:-----------:|:-----------:|---------------|
| Units - Objects         | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | war3map.w3u     |
| Items - Objects         | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | war3map.w3t     |
| Abilities - Objects     | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | war3map.w3a     |
| Destructables - Objects | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | war3map.w3b     |
| Doodads - Objects       | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | war3map.w3d     |
| Upgrades - Objects      | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | war3map.w3q     |
| Buffs - Objects         | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | war3map.w3h     |

### Trigger files

| Type                    | Json → War  | War → Json  | File          |
|-------------------------|:-----------:|:-----------:|---------------|
| LUA                    | ![times](https://cloud.githubusercontent.com/assets/4079034/25298707/7a883642-26c5-11e7-841c-cd3eb1425461.png) | ![times](https://cloud.githubusercontent.com/assets/4079034/25298707/7a883642-26c5-11e7-841c-cd3eb1425461.png) | war3map.lua       |
| JASS                    | ![times](https://cloud.githubusercontent.com/assets/4079034/25298707/7a883642-26c5-11e7-841c-cd3eb1425461.png) | ![times](https://cloud.githubusercontent.com/assets/4079034/25298707/7a883642-26c5-11e7-841c-cd3eb1425461.png) | war3map.j       |
| Strings                 | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | war3map.wts     |



### Map files

| Type                    | Json → War  | War → Json  | File          |
|-------------------------|:-----------:|:-----------:|---------------|
| Info File               | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | war3map.w3i        |
| Imported Files          | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | ![check](https://cloud.githubusercontent.com/assets/4079034/25298706/7a881946-26c5-11e7-896b-402f60a0f059.png) | war3map.imp        |
| Pathing                 | ![times](https://cloud.githubusercontent.com/assets/4079034/25298707/7a883642-26c5-11e7-841c-cd3eb1425461.png) | ![times](https://cloud.githubusercontent.com/assets/4079034/25298707/7a883642-26c5-11e7-841c-cd3eb1425461.png) | war3map.wpm        |
| Shadow map              | ![times](https://cloud.githubusercontent.com/assets/4079034/25298707/7a883642-26c5-11e7-841c-cd3eb1425461.png) | ![times](https://cloud.githubusercontent.com/assets/4079034/25298707/7a883642-26c5-11e7-841c-cd3eb1425461.png) | war3map.shd        |


### Not relevant
 ![minus-solid](https://user-images.githubusercontent.com/4079034/108644014-16f6bb00-747b-11eb-8c2b-9e7a1d7b6f9b.png) Custom Text Trigger File (war3map.wct)  
 ![minus-solid](https://user-images.githubusercontent.com/4079034/108644014-16f6bb00-747b-11eb-8c2b-9e7a1d7b6f9b.png) Trigger Names File (war3map.wtg)  
 ![minus-solid](https://user-images.githubusercontent.com/4079034/108644014-16f6bb00-747b-11eb-8c2b-9e7a1d7b6f9b.png) Menu Minimap (war3map.mmp)  
 ![minus-solid](https://user-images.githubusercontent.com/4079034/108644014-16f6bb00-747b-11eb-8c2b-9e7a1d7b6f9b.png) Minimap Image (war3mapMap.blp)  
 ![minus-solid](https://user-images.githubusercontent.com/4079034/108644014-16f6bb00-747b-11eb-8c2b-9e7a1d7b6f9b.png) Minimap Image (war3mapMap.b00  
 ![minus-solid](https://user-images.githubusercontent.com/4079034/108644014-16f6bb00-747b-11eb-8c2b-9e7a1d7b6f9b.png) Minimap Image (war3mapMap.tga)  
 ![minus-solid](https://user-images.githubusercontent.com/4079034/108644014-16f6bb00-747b-11eb-8c2b-9e7a1d7b6f9b.png) Map Preview Image (war3mapPreview.tga)

## Specification
### WC3MapTranslator format
We have a detailed  explaining how to format a map in JSON. It explains everything from the high-level map object, all the way down to creating individual units, tiles, or custom objects.
 > 🔗 [WC3MapTranslator format](https://github.com/ChiefOfGxBxL/WC3MapTranslator/wiki)

### war3map format
The underlying WarCraft map files (e.g. war3map.doo) have been documented in a separate repository. If you are curious about how a .w3x file is composed, this is the place to learn!
 > 🔗 [WC3MapSpecification](https://github.com/ChiefOfGxBxL/WC3MapSpecification)

## Contributing
We encourage contributions! Generally, the process of making a change is:
1. Fork this repo
2. Develop your changes on a new branch
3. Submit a pull request to `dev`

**Your code should**:
 * **run** (your code needs to work, of course)
 * **include tests** (write unit tests to demonstrate your code works under different conditions)
 * **be linted** (run `npm run lint` and follow the project's coding standards)
 * **pass CI** (we enforce: ESLint, unit tests pass, code coverage)

A code review is required on your PR to be accepted into `dev`. A project member will get back to you within one week. If you haven't heard from someone regarding your PR, feel free to ping @chiefofgxbxl.

## Special Thanks
We owe a lot of thanks to *Chocobo* on [TheHelper](http://www.thehelper.net/) for the detailed documentation of the files found in a .w3x archive. Two tutorials are [here (1)](http://www.thehelper.net/threads/guide-explanation-of-w3m-and-w3x-files.35292/) and [here (2)](http://world-editor-tutorials.thehelper.net/cat_usersubmit.php?view=42787).

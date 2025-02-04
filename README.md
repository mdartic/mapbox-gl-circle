# Spherical-Cap "Native Circle" for Mapbox GL JS

[![Lint and Build](https://github.com/smithmicro/mapbox-gl-circle/actions/workflows/lint-and-build.yml/badge.svg)](https://github.com/smithmicro/mapbox-gl-circle/actions/workflows/lint-and-build.yml)
[![Publish Pre-Release](https://github.com/smithmicro/mapbox-gl-circle/actions/workflows/publish-prerelease.yml/badge.svg)](https://github.com/smithmicro/mapbox-gl-circle/actions/workflows/publish-prerelease.yml)
[![Publish Release](https://github.com/smithmicro/mapbox-gl-circle/actions/workflows/publish-release.yml/badge.svg)](https://github.com/smithmicro/mapbox-gl-circle/actions/workflows/publish-release.yml)
[![NPM Version](https://img.shields.io/npm/v/mapbox-gl-circle.svg)](https://www.npmjs.com/package/mapbox-gl-circle)

This project uses Turf.js to create a `google.maps.Circle` replacement, as a Mapbox GL JS compatible GeoJSON object.
Allowing the developer to define a circle using center coordinates and radius (in meters). And, optionally, enabling
interactive editing via draggable center/radius handles. Just like the Google original!

## Getting Started

Include [mapbox-gl-circle.min.js](https://npmcdn.com/mapbox-gl-circle/dist/mapbox-gl-circle.min.js) in
the `<head>` of your HTML file to add the _MapboxCircle_ object to global scope:

```html
<script src='https://npmcdn.com/mapbox-gl-circle/dist/mapbox-gl-circle.min.js'></script>
```

Or even better, fashionably importing it using a module bundler:

```npm
npm install --save mapbox-gl-circle
```

```javascript
const MapboxCircle = require('mapbox-gl-circle');
// or "import MapboxCircle from 'mapbox-gl-circle';"
```

## Usage

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### MapboxCircle

A `google.maps.Circle` replacement for Mapbox GL JS, rendering a "spherical cap" on top of the world.

**Parameters**

-   `center`  
-   `radius`  
-   `options`  

**Examples**

```javascript
var myCircle = new MapboxCircle({lat: 39.984, lng: -75.343}, 25000, {
        editable: true,
        minRadius: 1500,
        fillColor: '#29AB87'
    }).addTo(myMapboxGlMap);

myCircle.on('centerchanged', function (circleObj) {
        console.log('New center:', circleObj.getCenter());
    });
myCircle.once('radiuschanged', function (circleObj) {
        console.log('New radius (once!):', circleObj.getRadius());
    });
myCircle.on('click', function (mapMouseEvent) {
        console.log('Click:', mapMouseEvent.point);
    });
myCircle.on('contextmenu', function (mapMouseEvent) {
        console.log('Right-click:', mapMouseEvent.lngLat);
    });
```

#### constructor

**Parameters**

-   `center` **({lat: [number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number), lng: [number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)} | \[[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number), [number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)])** Circle center as an object or `[lng, lat]` coordinates
-   `radius` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** Meter radius
-   `options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)?** 
    -   `options.editable` **[boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)?** Enable handles for changing center and radius (optional, default `false`)
    -   `options.minRadius` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** Minimum radius on user interaction (optional, default `10`)
    -   `options.maxRadius` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** Maximum radius on user interaction (optional, default `1100000`)
    -   `options.strokeColor` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** Stroke color (optional, default `'#000000'`)
    -   `options.strokeWeight` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** Stroke weight (optional, default `0.5`)
    -   `options.strokeOpacity` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** Stroke opacity (optional, default `0.75`)
    -   `options.fillColor` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** Fill color (optional, default `'#FB6A4A'`)
    -   `options.fillOpacity` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** Fill opacity (optional, default `0.25`)
    -   `options.refineStroke` **[boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)?** Adjust circle polygon precision based on radius and zoom
            (i.e. prettier circles at the expense of performance) (optional, default `false`)
    -   `options.properties` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)?** Property metadata for Mapbox GL JS circle object (optional, default `{}`)

#### on

Subscribe to circle event.

**Parameters**

-   `event` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Event name; `click`, `contextmenu`, `centerchanged` or `radiuschanged`
-   `fn` **[Function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)** Event handler, invoked with the target circle as first argument on
        _'centerchanged'_ and _'radiuschanged'_, or a _MapMouseEvent_ on _'click'_ and _'contextmenu'_ events
-   `onlyOnce` **[boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)?** Remove handler after first call (optional, default `false`)

Returns **[MapboxCircle](#mapboxcircle)** 

#### once

Alias for registering event listener with _onlyOnce=true_, see [#on](#on).

**Parameters**

-   `event` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Event name
-   `fn` **[Function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)** Event handler

Returns **[MapboxCircle](#mapboxcircle)** 

#### off

Unsubscribe to circle event.

**Parameters**

-   `event` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Event name
-   `fn` **[Function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)** Handler to be removed

Returns **[MapboxCircle](#mapboxcircle)** 

#### addTo

**Parameters**

-   `map` **mapboxgl.Map** Target map for adding and initializing circle Mapbox GL layers/data/listeners.
-   `before` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** Layer ID to insert the circle layers before; explicitly pass `null` to
        get the circle assets appended at the end of map-layers array (optional, default `'waterway-label'`)

Returns **[MapboxCircle](#mapboxcircle)** 

#### remove

Remove source data, layers and listeners from map.

Returns **[MapboxCircle](#mapboxcircle)** 

#### getCenter

Returns **{lat: [number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number), lng: [number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)}** Circle center position

#### setCenter

**Parameters**

-   `position` **{lat: [number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number), lng: [number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)}** 

Returns **[MapboxCircle](#mapboxcircle)** 

#### getRadius

Returns **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** Current radius, in meters

#### setRadius

**Parameters**

-   `newRadius` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** Meter radius

Returns **[MapboxCircle](#mapboxcircle)** 

#### getBounds

Returns **{sw: {lat: [number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number), lng: [number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)}, ne: {lat: [number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number), lng: [number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)}}** Southwestern/northeastern bounds

## Development

### Install Dependencies

    npm install

### Run Locally

    npm start

### Build Development Bundle

    npm run browserify

### Build Distributable Package

    npm pack

### Update README API Documentation

    npm run docs

## Changelog

### v. 1.6.7

-   `optionalDependencies` removed from `package.json`, making this package easier to depend on ([#82](https://github.com/smithmicro/mapbox-gl-circle/issues/82))

### v. 1.6.6

-   New CI/CD integration, replacing Jenkins with GitHub Actions ([#93](https://github.com/smithmicro/mapbox-gl-circle/issues/93))

### v. 1.6.5

-   Bug fix for layer switching in `mapbox-gl>0.40.1` ([#73](https://github.com/smithmicro/mapbox-gl-circle/issues/73))
-   Half-fixed bug causing errors when adding circle to map style without the `waterway-label` layer

### v. 1.6.4

-   Performance improvements for Firefox and Edge on slow computers
    ([#64](https://github.com/smithmicro/mapbox-gl-circle/issues/64),
    [#59](https://github.com/smithmicro/mapbox-gl-circle/issues/59))
-   Deprecated Docker build step 

### v. 1.6.3

-   Transferring core project into SmithMicro organization, `mblomdahl/mapbox-gl-circle -> smithmicro/mapbox-gl-circle`

### v. 1.6.2

-   Handle center/radius drag interactions over Mapbox GL markers
-   Watch for removal of map container and handle removal 

### v. 1.6.1

-   Improved move animation ([#55](https://github.com/smithmicro/mapbox-gl-circle/issues/55)) 

### v. 1.6.0

-   Add optional `before` argument to _MapboxCircle.addTo_
    ([#50](https://github.com/smithmicro/mapbox-gl-circle/issues/50))
-   Updated center/radius handle interactions to make performance issues more subtle 

### v. 1.5.2

-   Fix bug where the circle would always show a horizontal resize cursor on radius handles,
    irrespective of position (top/bottom/right/left)

### v. 1.5.1

-   Bug fixes with respect to cursor style when hovering over editable-and-clickable circles
    [SPFAM-1293](https://projects.smithmicro.net/browse/SPFAM-1293)

### v. 1.5.0

-   Added support for passing `minRadius` and `maxRadius` options to _MapboxCircle_ constructor

### v. 1.4.3

-   Bug fix for handling _map.setStyle_ updates
-   Added package version property to circle class

### v. 1.4.2

-   README updated with [Getting Started](#getting-started) section
-   Improved usage examples
-   Bug fixes:
    -   Creating circle instances with bundler import failed
    -   Docker build serving the wrong `index.html`    

### v. 1.4.1

-   Performance and stability fixes

### v. 1.4.0

-   _MapboxCircle_ now supports subscribing to `click` and `contextmenu` (right-click) events

### v. 1.3.0

-   Added setters and getters for center/radius
-   _MapboxCircle_ now allows subscribing to events and fires `centerchanged`/`radiuschanged` on user modification
-   Improved API documentation + moved it into README / Usage

### v. 1.2.5

-   More bug fixes:
    -   The circle can now successfully remove itself from the map
    -   Multiple circles may be added to the map and edited without causing too much conflict
    -   Initial center/radius drag interaction no longer fails

### v. 1.2.4

-   Bug fixes; passing `editable: false` when creating a circle is now respected, along with any styling options

### v. 1.2.3

-   Publishing releases as `@latest` and pre-releases as `@next` to <https://www.npmjs.com/package/mapbox-gl-circle>

-   CI update for Docker image, now publishes releases and pre-releases to SMSI internal Docker registry,
    <http://docker.smithmicro.io/repository/mapbox-gl-circle>

### v. 1.2.2

-   CI updates, now integrates with GitHub and builds reliably (with unique version names) under 
    <http://jenkins.smithmicro.io:8080/job/mapbox-gl-circle-multibranch/>

### v. 1.2.1

-   Added first-draft Jenkinsfile and started including `package-lock.json`
-   Revised `package.json` scripts

### v. 1.2.0

-   Removed dead code and unused methods
-   Restructured library, moving `circle.js -> lib/main.js` and `index.js -> example/index.js`
-   Refactored helper functions from `example/index.js` into _MapboxCircle_ class, obsoleted _index.html_ with
    DOM updates in _example/index.js_
-   Refactor into _MapboxCircle_ into new-style ES6 class
-   Made _MapboxCircle.animate()_ and a bunch of properties private, added overridable defaults for
    fillColor/fillOpacity
-   Updated ESLint config to respect browser/commonjs built-ins and added docs to _MapboxCircle_ in order to
    align with ESLint JSDoc requirements
-   Updated project details in package.json and committed first-draft API documentation

### v. 1.1.0

Updated circle from Mapbox [bl.ocks.org sample](https://bl.ocks.org/ryanbaumann/d286190943d6b4eb70e65a9f76eab5a5/d3cd7cea5feed0dfddbf3705b7936ff560f668d1).

Now provides handles for modifying position/radius. Seems to also do better performance wise.

### v. 1.0.0

The initial 1.0.0 release is a modified version of
the [Draw-Circle.zip](https://www.dropbox.com/s/ya7am28y8eugd72/Draw-Circle.zip?dl=0) archive we got from Mapbox.

Live demo of the original can be found here: <https://www.mapbox.com/labs/draw-circle/>

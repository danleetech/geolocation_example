
# Geolocation Example in Vanilla Javascript

By Daniel Lee

### Technologies Used

*   [Browser Native navigator API](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API)
*   [Open Layers open source Map API](https://openlayers.org/en/latest/doc/quickstart.html)

Most browsers allow you to simply query the geo location after asking for user permissions

```js
function queryGeoLocation(successCallback, failureCallback) {
  if(!navigator.geolocation) {
    alert('Your browser does not support geo location')
  } else {
    // navigator is a global object present in the DOM / Browser
    navigator
      .geolocation
      .getCurrentPosition(successCallback, failureCallback);
  }
}
```

Using the Open Layers Map API is free and doesn't require an API key.  
All I did was import these assets in the top of my HTML file.

```html
<!-- assets needed for open layers -->
<link
  rel="stylesheet"
  href="https://cdn.jsdelivr.net/gh/openlayers/openlayers.github.io@master/en/v6.4.3/css/ol.css"
  type="text/css"
/>
<script src="https://cdn.jsdelivr.net/gh/openlayers/openlayers.github.io@master/en/v6.4.3/build/ol.js">
```


Here is how my code looks like:

```js
function renderMap(domId, positionObj) {
  const { latitude, longitude } = positionObj.coords;

  new ol.Map({
    target: domId,
    layers: [
      new ol.layer.Tile({
        source: new ol.source.OSM(),
      }),
    ],
    view: new ol.View({
      center: ol.proj.fromLonLat([longitude, latitude]),
      zoom: 10,
    }),
  });
}
```

**NOTE:** My `onSuccessCallback` in my previous `queryGeoLocation` function takes a success callback which renders the map object to the DOM.


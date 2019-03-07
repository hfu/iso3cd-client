# iso3cd-client
client code for iso3cd visualization
# Demo
https://hfu.github.io/iso3cd-geospatial/?https://hfu.github.io/iso3cd-client/cartotiles.js#3.36/-11.38/-75.95

# What the clients shall do to have geospatial visualization of their statistic data?
## 1. Prepare cartotiles.js that contains statistic data and style description
Please create a single JavaScript file that has the same structure as https://hfu.github.io/iso3cd-client/cartotiles.js, i.e. provide a global variable called cartotiles that contains two properties; (1) `data` array, and (2) `color` function. 

The structure of the `cartotiles.js` is as below: 
```javascript
cartotiles = {
  data: [
    ['AFG', 2] // , ...
  ],
  color: function (value) {
    //...
    return ['rgb', 0, 61, 153]
  }
}
```

### Specifications for the `data` array
The `data` property shall be an array of arrays. Each of the arrays shall represent the statistical record for an ISO-3166-1 Alpha-3 code. The first element shall be the ISO-3166-1 Alpha-3 code, and the second element shall be the value assigned for that code.

e.g. `['AFG', 2]` means that the number 2 is assigned to Afghanistan.

### Specifications for the `color` function
The `color` property shall be a function that takes the statistical value and returns the assigned color. The color shall be represented as in [Mapbox Style Specification](https://docs.mapbox.com/mapbox-gl-js/style-spec/), i.e. `"rgb(255, 255, 255)"`, `["rgb", 255, 255, 255]`. Use of alpha value (`rgba`) shall also be possible. 

#### example
The following example returns the same color for all statistical values.
```javascript
  color: function (value) {
    return ['rgb', 0, 61, 153]
  }
```

The following example is an implementation of the legend in the map on [Reporting compliance by State parties to the human rights treaty bodies](https://www.ohchr.org/Documents/Issues/HRIndicators/Reporting_Compliance.pdf).
```javascript
  color: function (value) {
    if (value === 0) {
      return ['rgb', 153, 0, 51]
    } else if (value <= 50) {
      return ['rgb', 255, 117, 25]
    } else if (value < 100) {
      return ['rgb', 48, 131, 255]
    } else {
      return ['rgb', 0, 61, 153]
    }
  }
```

## 2. Concatenate URLs of the geospatial service and the cartotiles.js
The URL of the geospatial service is https://hfu.github.io/iso3cd-geospatial/. Concatenate the URL for your cartotiles.js after adding '?'.

In the case the cartotiles.js is at https://hfu.github.io/iso3cd-client/cartotiles.js, the URL for the map is https://hfu.github.io/iso3cd-geospatial/?https://hfu.github.io/iso3cd-client/cartotiles.js.

1. Please not that the '/' after geospatial shall not be avoided.
2. You can add #${zoom}/${latitude}/${longitude} hash like in https://hfu.github.io/iso3cd-geospatial/?https://hfu.github.io/iso3cd-client/cartotiles.js#3.36/-11.38/-75.95.
3. This URL are intended to be used as the src of iframe.

## 3. There is no step 3.
It is done :-) 

# See also
[iso3cd-geospatial](https://github.com/hfu/iso3cd-geospatial): the contents that are proposed to be hosted by UN Geospatial Information Services. 

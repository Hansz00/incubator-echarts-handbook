# Visual Map of Data

Data visualization is the process (visual coding) of mapping data to visual elements (visual channel). 

Every chart types in ECharts have the built-in mapping process. For example, the line chart map the data to "Line" and the bar chart map it to "length". Complicate charts like relation chart, event flow chart, tree chart also has there unique built-in mappings. 

In addition, ECharts supported [visualMap component](${optionPath}visualMap) to provide a normalized visual mapping method. The visual elements in `visualMap` are: 

- symbol, symbolSize
- color, opacity, colorAlpha
- colorLightneses, colorSaturation, colorHue

Here is a brief introduction about how to use `visualMap` component. 

## Data and Dimension

Data in ECharts normally stored in the [`series.data`](${optionPath}series.data). Depend on the chart type, the form of data has little difference such as "line chart", "tree" and "graph", etc., but always have a commonality: set of "dataItem". Every data item has "Value" and other info (if needed). Each "Value" can be one-dimensional or multi-dimensional. 

For example, the common type of [series.data](${optionPath}series.data) is "line chart", which is a normal array: 

```js
series: {
    data: [
        {       // items here are dataItem
            value: 2323, // value of data
            itemStyle: {...}
        },
        1212,   // normally is value of dataItem
        2323,   // each value is one-dimensional
        4343,
        3434
    ]
}
```

```js
series: {
    data: [
        {                        // items here are dataItem
            value: [3434, 129,  'San Marino'], // value of data
            itemStyle: {...}
        },
        [1212, 5454, 'Vatican'],   // normally is value of dataItem
        [2323, 3223, 'Nauru'],     // each value is "3D". every column is a dimension
        [4343, 23,   'Tuvalu']    // for “bubble chart”, first dimension map the x-axis
                                 // second dimension map the y-axis
                                 // first dimension map the symbolSize
    ]
}
```

ECharts defaulted map the first two dimensions. The first one to x-axis and the second one to y-axis. Using `visualMap` can help to show more dimensions. Commonly, the [scatter chart](${optionPath}series-scatter) uses radius to reflect the third dimension. 

## visualMap Component

The `visualMap` component defined the mapping between *which dimension* and *which visual element*. 

ECharts provide two types of `visualMap` component, seperate by using [visualMap.type](${optionPath}visualMap.type).

The define structure is :

```js
option = {
    visualMap: [ // multiple visualMap component can be defined at the same time
        { // first visualMap component
            type: 'continuous', // continuous visualMap
            ...
        },
        { // second visualMap component
            type: 'piecewise', // piecewise visualMap
            ...
        }
    ],
    ...
};
```


## Continuous and Piecewise visualMap Component

The `visualMap` component of ECharts can be divided into [visualMapContinuous](${optionPath}visualMap-continuous) and [visualMapPiecewise](${optionPath}visualMap-piecewise). 

The continuous type means the data used in visual mapping is continuous while the piecewise type means the data is separated into several segments or is discrete. 

### Continuous Visual Mapping

Continuous visual mapping determines the range by specifying the maximum and minimum value. 

```js
option = {
    visualMap: [{
        type: 'piecewise'
        min: 0,
        max: 5000,
        dimension: 3,       // 4th dimension of series.data(value[3]) is mapped
        seriesIndex: 4,     // map for series 4
        inRange: {          // config for selected range
            color: ['blue', '#121122', 'red'], // color list of shape color mapping
                            // minimum value to 'blue'
                            // maximum value to 'red'
                            // calculate rest by linear algorithms
            symbolSize: [30, 100]   // Define the range of symbol size mapping
                                    // minimum value to 30
                                    // maximmum value to 100
                                    // calculate rest by linear algorithms
        },
        outOfRange: {       // for visual config out of range
            symbolSize: [30, 100]
        }
    },
       ...
    ]
};
```

The [visualMap.inRange](${optionPath}visualMap.inRange) define the stype of visual mapping in the range, [visualMap.outOfRange](${optionPath}visualMap.outOfRange) define the style out of the range.

[visualMap.dimension](~visualMap.dimension) defined the dimension of data to make the visual mapping. 


### Piecewise Visual Mapping

The piecewise visual mapping component have three modes: 

- Average segmentation for regular data: divide equally into several parts depends on the [visualMap-piecewise.splitNumber](${optionPath}visualMap-piecewise.splitNumber). 
- coustom segmentation for continuous data: define domain of each part by using [visualMap-piecewise.pieces](${optionPath}visualMap-piecewise.pieces). 
- Discrete data (categorical data): defined in  [visualMap-piecewise.categories](${optionPath}visualMap-piecewise.categories). 

While using segmentation visual mapping, you need to set `type` to `'piecewise'` and choose one of the three config items. After finishing the setting of that one, others can be similar to the continuous visual mapping. 

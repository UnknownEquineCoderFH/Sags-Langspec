## Types

### Literals
* Integer - Signed 32-bit natural number.
* Float - Signed 64-bit real number.
* Boolean - A binary true/false value.
* Text - A variable-size string of characters.
* Timestamp - An **ISO 8601** date-time value.
* Coordinate - An **ISO 6709** coordinate value.

### Containers
- List - A collection of objects with the same type.
- Map - A collection of key-value pair objects. (note: keys are always of type `Text`)
- Stream - A continuous stream of objects with the same type (can be seen as a generator).

### Structs
Define a new `struct` with the following syntax
```
struct Measurement:
	value Float
	taken_at Timestamp
```

## Pipeline
A `pipeline` is a function-like operation we perform on data.
It is the gross of what the Sagittarius Scripting language does.

Define a `pipeline` with the following syntax
```
1	@timeout(1000)
2	pipeline avg_measurement (Measurement... -> Float):
3		yieldfrom "measurements" |
4		filter "value" |
5		takeif valid |
6		collect 100 |
7		mean
```

To illustrate the meaning of this pipeline, we'll take it apart line by line

1) `@timeout(1000)`
This sets the maximum waiting time for a response before timing it out (1000ms in this case).
It serves to prevent slow or insufficient data transmission for real-time pipelines.
2) `pipeline avg_measurement (Measurement... -> Float)`
The pipeline keyword creates a new pipeline, which we name `avg_measurement`.
As part of the declaration, we annotate the input and output type of the pipeline 
`(Measurement... -> Float)`, which translates to: *take a stream of Measurement and return a Float*.
3) `yieldfrom "measurements"`
This expresses where the data comes from. Imagine a .ssd snippet like the one below as the source. 
In this case, the `measurements` label declares where the data comes from (i.e. the data source).
From this, we are declaring that the data source `measurements` should return json objects that conform to the struct `Measurement` (that means, there's a field `"value"` that can be parsed as a `Float` and a field `"taken_at"` that can be parsed as a `Timestamp`). Any other field present is optional and irrelevant.
The `yieldfrom` pipeline keeps polling the endpoint for new data, transforming a single-value endpoint into a `Stream`.
The `|` symbol is called the `pipe operator`, and allows to chain different built-in and user-defined pipelines together.
```
...
data:
	- measurements:
		uri is https://example.com/measurements
...
```
4) `filter "value"`
The `filter` pipelin transforms any `container` or `struct` object into some values taken from it.
In the case of `struct`, this is translated to taking only a single field from each value in the pipeline, effectively filtering the objects into one of their fields (in this case, a `Measurement` into a `Float`).
5) `takeif valid`
The `takeif` pipeline applies a value-wise filter and only allows values that respect a certain boolean condition. 
`takeif` requires a pipeline that takes whatever type you're filtering and returns a `Boolean`, in this case `valid` would be a built-in for filtering NAN and null values.
6) `collect 100`
The `collect` pipeline takes a `Stream` and transforms it into a `List` of the same type, with length *N*, where *N* is the number provided to it.
7) `mean`
Finally, we call the `mean` pipeline on the entire operation. It takes a `List` of numeric values and returns the arithmetic mean. In this case, it will be a `Float` since `"value"` is a `Float` and we annotated the type in line 2.








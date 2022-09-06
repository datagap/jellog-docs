# Grids

## Introduction

Jellog tag helpers for bootstrap based grid system.



## Demo

See the [grids demo page](https://bootstrap-taghelpers.jellog.io/Components/Grids) to see it in action.



### Sizing

**Equal Width:** Creates columns with equal width.

Sample:

````xml
<jellog-container>
    <jellog-row>
        <jellog-column jellog-border="Info">1 of 2</jellog-column>
        <jellog-column jellog-border="Danger">2 of 2</jellog-column>
    </jellog-row>
    <jellog-row>
        <jellog-column jellog-border="Primary">1 of 3</jellog-column>
        <jellog-column jellog-border="Secondary">2 of 3</jellog-column>
        <jellog-column jellog-border="Dark">3 of 3</jellog-column>
    </jellog-row>
</jellog-container>
````

**Column Breaker:** `jellog-column-breaker` is used for breaking the automatic width of placement of the current row and starting in a new row afterwards.

Sample:

````xml
<jellog-container>
    <jellog-row>
        <jellog-column>column</jellog-column>
        <jellog-column>column</jellog-column>
        <jellog-column-breaker/>
        <jellog-column>column</jellog-column>
        <jellog-column>column</jellog-column>
    </jellog-row>
</jellog-container>
````

**Setting one column width:** size attribute is used for setting the width for a specific column. 

Sample:

```xml
<jellog-container>
    <jellog-row>
        <jellog-column>1 of 3</jellog-column>
        <jellog-column size="_6">2 of 3 (wider)</jellog-column>
        <jellog-column>3 of 3</jellog-column>
    </jellog-row>
    <jellog-row>
        <jellog-column>1 of 3</jellog-column>
        <jellog-column size="_5">2 of 3 (wider)</jellog-column>
        <jellog-column>3 of 3</jellog-column>
    </jellog-row>
</jellog-container>
```

**Variable width content:** Auto resizing column based on content.

```xml
<jellog-container>
    <jellog-row h-align="Center">
        <jellog-column size-lg="_2" jellog-border="Info">1 of 3</jellog-column>
        <jellog-column size-md="Auto" jellog-border="Danger">Contrary to popular belief, Lorem Ipsum is not simply random text.</jellog-column>
        <jellog-column size-lg="_2" jellog-border="Warning">3 of 3</jellog-column>
    </jellog-row>
    <jellog-row>
        <jellog-column>1 of 3</jellog-column>
        <jellog-column size-md="Auto">Variable width content</jellog-column>
        <jellog-column size-lg="_2">3 of 3</jellog-column>
    </jellog-row>
</jellog-container>
```



### Responsive Classes

Responsive classes can be used strongly typed within jellog tags. 

```xml
<jellog-row>
    <jellog-column size-sm="_8">col-sm-8</jellog-column>
    <jellog-column size-sm="_4">col-sm-4</jellog-column>
</jellog-row>
<jellog-row>
    <jellog-column size-sm="_">col-sm</jellog-column>
    <jellog-column size-sm="_">col-sm</jellog-column>
    <jellog-column size-sm="_">col-sm</jellog-column>
    <jellog-column size-sm="_">col-sm</jellog-column>
</jellog-row>
<!-- Stack the columns on mobile by making one full-width and the other half-width -->
<jellog-row>
    <jellog-column size="_12" size-md="_8">.col-12 .col-md-8</jellog-column>
    <jellog-column size="_6" size-md="_4">.col-6 .col-md-4</jellog-column>
</jellog-row>

<!-- Columns start at 50% wide on mobile and bump up to 33.3% wide on desktop -->
<jellog-row>
    <jellog-column size="_6" size-md="_4">.col-6 .col-md-4</jellog-column>
    <jellog-column size="_6" size-md="_4">.col-6 .col-md-4</jellog-column>
    <jellog-column size="_6" size-md="_4">.col-6 .col-md-4</jellog-column>
</jellog-row>

<!-- Columns are always 50% wide, on mobile and desktop -->
<jellog-row>
    <jellog-column size="_6">.col-6</jellog-column>
    <jellog-column size="_6">.col-6</jellog-column>
</jellog-row>
```



### Alignment

Column alignments can be done strongly typed in jellog tags with both vertically and horizontally.

**Vertical-alignment**: `v-align` attribute value is used to align the columns vertically. 

Sample:

```xml
<jellog-container>
    <jellog-row v-align="Start">
        <jellog-column>column</jellog-column>
        <jellog-column>column</jellog-column>
        <jellog-column>column</jellog-column>
    </jellog-row>
    <jellog-row v-align="Center">
        <jellog-column>column</jellog-column>
        <jellog-column>column</jellog-column>
        <jellog-column>column</jellog-column>
    </jellog-row>
    <jellog-row v-align="End">
        <jellog-column>column</jellog-column>
        <jellog-column>column</jellog-column>
        <jellog-column>column</jellog-column>
    </jellog-row>
</jellog-container>
```

**Horizontal-alignment**: `h-align` attribute value is used to align the columns horizontally. 

Sample:

```xml
<jellog-container>
    <jellog-row h-align="Start">
        <jellog-column size="_4">One of two columns</jellog-column>
        <jellog-column size="_4">One of two columns</jellog-column>
    </jellog-row>
    <jellog-row h-align="Center">
        <jellog-column size="_4">One of two columns</jellog-column>
        <jellog-column size="_4">One of two columns</jellog-column>
    </jellog-row>
    <jellog-row h-align="End">
        <jellog-column size="_4">One of two columns</jellog-column>
        <jellog-column size="_4">One of two columns</jellog-column>
    </jellog-row>
    <jellog-row h-align="Around">
        <jellog-column size="_4">One of two columns</jellog-column>
        <jellog-column size="_4">One of two columns</jellog-column>
    </jellog-row>
    <jellog-row h-align="Between">
        <jellog-column size="_4">One of two columns</jellog-column>
        <jellog-column size="_4">One of two columns</jellog-column>
    </jellog-row>
</jellog-container>
```

**No gutters**: The gutters between columns in predefined grid classes can be removed with `gutters="false"`. This removes the negative `margin`s from `jellog-row` and the horizontal `padding` from all immediate children columns. 

Sample:

```xml
<jellog-row gutters="false">
    <jellog-column size="_8">One of two columns</jellog-column>
    <jellog-column size="_4">One of two columns</jellog-column>
</jellog-row>
```

**Column wrapping**: If more than 12 columns are placed within a single row, each group of extra columns will, as one unit, wrap onto a new line.

Sample:

```xml
<jellog-row>
    <jellog-column size="_9">.col-9</jellog-column>
    <jellog-column size="_4">.col-4<br>Since 9 + 4 = 13 &gt; 12, this 4-column-wide div gets wrapped onto a new line as one contiguous unit.</jellog-column>
    <jellog-column size="_6">.col-6<br>Subsequent columns continue along the new line.s</jellog-column>
</jellog-row>
```



### Reordering

**Order Classes**:  `order` attribute is used for controlling the visual order of the content. 

Sample:

```xml
<jellog-container>
    <jellog-row>
        <jellog-column order="_12">First, but Last</jellog-column>
        <jellog-column>Second, but unordered</jellog-column>
        <jellog-column order="_6">Third, but Second</jellog-column>
    </jellog-row>
</jellog-container>
```

**Offsetting columns**:  `offset` attribute is used for setting the offset of the grid columns. 

Sample:

```xml
<jellog-container>
    <jellog-row>
        <jellog-column size-md="_4">.col-md-4</jellog-column>
        <jellog-column size-md="_4" offset-md="_4">.col-md-4 .offset-md-4</jellog-column>
    </jellog-row>
    <jellog-row>
        <jellog-column size-md="_3" offset-md="_3">.col-md-3 .offset-md-3</jellog-column>
        <jellog-column size-md="_3" offset-md="_3">.col-md-3 .offset-md-3</jellog-column>
    </jellog-row>
    <jellog-row>
        <jellog-column size-md="_6" offset-md="_3">.col-md-6 .offset-md-3</jellog-column>
    </jellog-row>
    <jellog-row>
        <jellog-column size-sm="_5" size-md="_6">.col-sm-5 .col-md-6</jellog-column>
        <jellog-column size-sm="_5" offset-sm="_2" size-md="_6" offset-md="_">.col-sm-5 .offset-sm-2 .col-md-6 .offset-md-0</jellog-column>
    </jellog-row>
    <jellog-row>
        <jellog-column size-sm="_6" size-md="_5" size-lg="_6">col-sm-6 .col-md-5 .col-lg-6</jellog-column>
        <jellog-column size-sm="_6" size-md="_5" offset-md="_2" size-lg="_6" offset-lg="_">.col-sm-6 .col-md-5 .offset-md-2 .col-lg-6 .offset-lg-0</jellog-column>
    </jellog-row>
</jellog-container>
```



## jellog-row Attributes

- **v-align:** A value indicates the vertical positioning of the containing columns. Should be one of the following values:
  * `Default` (default value)
  * `Start`
  * `Center`
  * `End`

- **h-align**: A value indicates the horizontal positioning of the containing columns. Should be one of the following values: 
  * `Default` (default value)
  * `Start`
  * `Center`
  * `Around`
  * `Between`
  * `End`
- **gutter**: A value indicates if the negative `margin` and horizontal `padding` will be removed from all children columns. Will act as `true` value if this attribute is not set. Should be one of the following values: 
  * `true`
  * `false`

## jellog-column Attributes

- **size:** A value indicates the width of the column from `_`, `Undefined`, `_1`..`_12`, `Auto`. Or can be used with predefined values like:
  - `size-sm`
  - `size-md`
  - `size-lg`
  - `size-xl`
- **order**: A value indicates the order of column from `Undefined`, `_1`..`_12`, `First` and `Last`.
- **offset:** A value indicates offset of the column from `_`, `Undefined`, `_1`..`_12`, `Auto`. Or can be used with predefined values like:
  - `offset-sm`
  - `offset-md`
  - `offset-lg`
  - `offset-xl`


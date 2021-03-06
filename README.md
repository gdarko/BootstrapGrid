# TwitterBootstrapGrid

This is a lightweight PHP script that makes easy generating a ``Twitter Bootstrap 3`` grid using PHP.
It uses the default Twitter bootstrap classes like ``.row`` and ``.col-*`` to generate the grids.
It's pretty straightforward to use, it allows to specify how many columns per row to have for each Bootstrap viewport (xs, sm, md, lg)

# Installation
### Composer
You can install it with composer, you need to have composer installed and you are good to go!
```
composer require gdarko/twitter-bootstrap-grid
```
### I don't know what Composer is
I don't recommend this way but you can always download the latest release and require the class.
```php
require "twitter-bootstrap-grid/src/TwitterBootstrapGrid.class.php"
```

# How to Use
Few examples how to use the script:

### Example #1
You can use the addColumn method to add a column to the grid and later build. The constructor accepts array of columns as a second parameter
```php
use gdarko\Tools\TwitterBootstrapGrid;

$grid = new TwitterBootstrapGrid( $row_columns = 4 );
$columns = ["1", "2", "3", "4", "5", "6", "7"];
foreach($columns as $column){
    $grid->addColumn($column);
}
echo $grid->build();
```

### Example #2
You can use the setTotalRowColumns method to change the number of columns for a given viewport per row.
In this example we are using 2 columns for "lg" classes. So one of the column classes will be ``.col-sm-6``
```php
use gdarko\Tools\TwitterBootstrapGrid;

$columns = ["1", "2", "3", "4", "5", "6", "7"];
$grid = new TwitterBootstrapGrid( $row_columns = 4, $columns );
$grid->setTotalRowColumns(2, "lg");
echo $grid->build();
```

### Example #3
You have a large templates that need to be printed? No problem. You can combine it with output buffering.
```php
use gdarko\Tools\TwitterBootstrapGrid;

$grid = new TwitterBootstrapGrid( $row_columns = 3 );
foreach($objects as $object){
    ob_start();
    include('templates/display-orange.php');
    $content = ob_get_clean();
    $grid->addColumn($content);
}
$grid->setTotalRowColumns(3, "sm");
echo $grid->build();
```

### Example #4
Do you want to build a fluid grids? For example you have 3 columns per row on large screens and two columns per row on mobiles. It's not that easy with the default Bootstrap aproach. This snippet will make your life easier.
```php
use gdarko\Tools\TwitterBootstrapGrid;

$grid = new TwitterBootstrapGrid();
//Demo data, ignore it
for($i = 0; $i < 9; $i++){
    $grid->addColumn($i . "");
}

$grid->setCustomTotalRowColumns($grid->getColumnsCount());
$grid->setCustomColumnClass("col-lg-4", "lg");
$grid->setCustomColumnClass("col-xs-6", "xs");

echo $grid->build();
```
Pretty straightforward, huh?

# Changelog

### v1.2
-Fix: Missing closing </div> when the last row has less columns than specified number of columns per row.

### v1.1
- Fluid grids support ( see Example #4 )
- Updated constructor ( no need to require $row_column_lg in case we are creating fluid grids )

### v1.0
- Integration with Composer
- Integration with PSR-4

# Development
Want to contribute? Great!

If you found a bug or want to contribute to the script feel free to create pull requests to make it even better!




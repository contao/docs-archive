
# array_insert()

Insert a value / merge an array into an existing array at a particular index.


## Description

```php
function array_insert(&$arrCurrent, $intIndex, $arrNew)
```

> #### info:: Info
> * The passed `$arrCurrent` array will be modified.
> * Any preexisting numeric indices will be rebased.

**Location in Contao 3:** [*system/helper/functions.php*][contao3]<br>
**Location in Contao 4:** [*vendor/contao/core-bundle/src/Resources/contao/helper/functions.php*][contao4]

## Parameters

1. *array* `&$arrCurrent`

    The array to insert items into.

2. *integer* `$intIndex`

    The position in `$arrCurrent` where new items should be inserted.

3. *mixed* `$arrNew`

    The content to insert into the array.

    If this is an array, it will be [recursively merged][array_merge_recursive] into `$arrCurrent`.

    If it's not an array, it will be inserted into `$arrCurrent` at the given position with the appropriate numeric index.
    

## Examples

1. Insert an associative array into another associative array

    ```php
    <?php

    $fruit = [
        'apple' => 'green',
        'date' => 'brown'
    ];
    
    array_insert($fruit, 1, [
        'banana' => 'yellow',
        'cranberry' => 'red'
    ]);
    
    /*
    $fruit === [
        'apple' => 'green',
        'banana' => 'yellow',
        'cranberry' => 'red',
        'date' => 'brown'
    ]
    */
    ```

2. Insert a value into an array

    ```php
    <?php

    $placeholders = [ 'foo', 'foobar' ];
    
    array_insert($placeholders, 1, 'bar');
    
    // $placeholders === [ 'foo', 'bar', 'foobar' ]
    ```


[contao3]: https://github.com/contao/core/blob/3.5.0/system/helper/functions.php#L554-L579
[contao4]: https://github.com/contao/core-bundle/blob/4.0.0/src/Resources/contao/helper/functions.php#L386-L411
[array_merge_recursive]: http://php.net/manual/function.array-merge-recursive.php

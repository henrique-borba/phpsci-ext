# PHPSci CArray Extension

This is the extension used by [PHPSci](https://www.github.com/phpsci/phpsci). 
It offers the CArray object in place of PHP arrays to make scientific calculations faster.


Although it is not necessary, or you want to create your own library of arrays, we recommend that you use
[PHPSci](https://www.github.com/phpsci/phpsci) together with this extension.

> **ATENTTION:** Misuse of this extension can cause excessive memory consumption and consequently system crash. See the CArray internals section if you want to know more about the internal operation of the extension.

## Building

It's really easy to compile this extension using Linux environments.

#### Requirements

- php-devel (php-dev)
- PHP 7.x

#### Compiling

Clone the repository, `cd` to the source folder and:
```php
$ phpize
$ ./configure
$ make clean
$ make
$ make install
```
> Don't forget to check if the extension is enabled in your php.ini file.

> **Apache/NGINX Users:** Don't forget to restart your services.

## Using CArrays
Here are some examples of CArrays:

### Creating CArrays

Let's create two CArrays using the `Identity` initializer:

```php
$a = CArray::identity(2);
$b = CArray::identity(4);
print_r($a);
print_r($b);
```
```php
stdClass Object
(
    [uuid] => 0
)
stdClass Object
(
    [uuid] => 1
)
```
It sounds strange, but calm down! You will not be able to view your array using
`print_r` because CArrays are not PHP arrays. It's just pointers to memory, to view 
your array you'll need to convert it to PHP Array:

### Converting CArrays to PHP Arrays

Remember that this may require considerable time depending on the size of your CArray. Try performing all operations 
before converting to a PHP Array, and only, if needed of course.

```php
$php_array = CArray::toArray($a->uuid, 10, 10);
print_r($php_array);
```
> The `toArray()` static method receive 3 arguments: `public static toArray(int uuid, int rows, int cols);`. **For now, It's your
job to keep track of your array dimension and sizes. Misuse can cause segment faults.**

```php
Array
(
    [0] => Array
        (
            [0] => 1
            [1] => 0
        )

    [1] => Array
        (
            [0] => 0
            [1] => 1
        )

)
```
Now we can see our array and use it with other PHP general libraries.
WScore.Enum
===========

A simple enum implementation

### license

MIT License

### inspired by

inspired (or copied idea) from:
[https://github.com/myclabs/php-enum](https://github.com/myclabs/php-enum)
and
[https://github.com/fre5h/DoctrineEnumBundle](https://github.com/fre5h/DoctrineEnumBundle).



Sample Code
-----------

### creating a enum class.

Declaring a class for enums.

```php
/**
 * Class Gender
 * @package tests\EnumTest
 *
 * @method bool isMale
 * @method bool isFemale
 */
class Gender extends Enum
{
    const MALE   = 'M';
    const FEMALE = 'F';

    protected static $choices = [
        self::MALE   => 'Male',
        self::FEMALE => 'Female',
    ];
}
```

Minimum requirement is to define the static variable, $choices.
To use some shortcut method, define constant.


### how to use it.

Constructing an enum value object.

```php
$someOneGender = new Gender( Gender::FEMALE );
```

To get the value,

```php
// getting the value set
echo (string) $someOneGender;   // 'F'
echo $someOneGender->get();     // 'F'
echo $someOneGender->show();    // 'Female'
```

To check the value, use ```is``` method.
The ```isMale``` and ```isFemale``` methods are
 magic methods implemented by ```__call```. 

```php
// checking the value
echo $someOneGender->is( Gender::MALE );   // false;
echo $someOneGender->is( Gender::FEMALE ); // true;
echo $someOneGender->isMale();             // false;
echo $someOneGender->isFemale();           // true;
```

Static methods to get information about the enum class.

```php
// does this exist?
echo $someOneGender::exists( 'X' );        // false;

// getting the list of possible values
$list = Gender::getValues(); // [ 'M', 'F' ]
$list = Gender::getChoices();   // [ 'M' => 'Male', 'F' => 'Female' ]
```

that's it.

### identification of object

This is not implemented.

```php
$someOneGender = new Gender( Gender::FEMALE );
$someOneElseGender = new Gender( Gender::FEMALE );
$someOneGender ==  $someOneElseGender; // true.
$someOneGender === $someOneElseGender; // false.
```



EnumList Wishing Code
---------------------

This is an idea for array of enum values.
i.e. not implemented yet.


```php
class Choices extends EnumList
{
    const ADD = 'A';
    const MOD = 'M';
    const DEL = 'D';
    protected static $choices = [
        self::ADD => 'Adding',
        self::MOD => 'Modifying',
        self::DEL => 'Deleting'
    ];
    protected static $separator = ',';
}
```

```php
$choice = new Choices( "A,M" );

// getting the values
echo (string) $choice;  // "A,M"
echo $choice->get();    // "A,M"
echo $choice->show();   // [ 'Adding', 'Modifying' ]
echo $choice->list();   // [ 'A', 'M' ]

// checking the value
echo $choice->is( Choices::DEL ); // false;
echo $choice->is( Choices::ADD ); // true;
echo $choice->isDel();            // false;
echo $choice->isMod();            // true;

// getting the list of possible values
$list = Choices::getConstList(); // [ 'A', 'M', 'D' ]
$list = Choices::getChoices();   // [ 'A' => 'Adding', 'M' => 'Modifying', 'D' => 'Deleting' ]
```
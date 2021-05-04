# Calculating number of overlapping dates

```php
<?php

namespace App\Helpers;

use Carbon\Carbon;

class Date
{
    public static function calculateOverlappingDays(string $date, $string date2)
    {
        $from = Carbon::parse($date);
        
        $to = Carbon::parse($to);
        
        return $from->diffInDays($to);
    }
}

// Example

$intervals = App\Helpers\Date::calculateOverLappingDays('2021-01-01', '2021-05-01');

$intervals === 120;
```

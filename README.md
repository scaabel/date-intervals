# Calculating number of overlapping dates

```php
<?php

namespace App\Helpers;

use Carbon\Carbon;
use Carbon\CarbonPeriod;
use Illuminate\Support\Arr;

class Date
{
    public static $daysInPeriods = [];

    public static function calculateOverlappedDays(array $intervals): int
    {
        collect($intervals)
            ->each(function ($interval) {
                list($from, $to) = static::generateDate($interval);

                $period = CarbonPeriod::create($from, $to);

                foreach ($period as $date) {
                    $day = $date->format('Y-m-d');

                    static::$daysInPeriods[] = $day;
                }
            });

        $uniqueDays = collect(static::$daysInPeriods)->unique();
        $overlappedDays = collect(static::$daysInPeriods)->diffAssoc($uniqueDays);

        return $overlappedDays->count();
    }

    private static function generateDate(array $interval): array
    {
        $from = Carbon::parse(Arr::first($interval))->toDateTimeString();

        $to = Carbon::parse(Arr::last($interval))->toDateTimeString();

        return [$from, $to];
    }
}

// Example

$intervals = [
           ['2021-01-01', '2021-02-02'],
           ['2021-01-03', '2021-03-03'],
           ['2021-03-01', '2021-04-04']
        ];

$overlappedDaysCount = App\Helpers\Date::calculateOverlappedDays($intervals);

$overlappedDaysCount === 34;
```

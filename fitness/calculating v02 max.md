[this page says](https://www.omnicalculator.com/sports/vo2-max-runners):

```
VO2max% ​= 0.8 + 0.1894393*e^(−0.012778*t) + 0.2989558*e^(−0.1932605*t)​

VO2 = −4.60 + 0.182258 * v + 0.000104 * v^2

VO2max=VO2/VO2max %

where t is the race time in _minutes_, and v is race velocity in _meters / minute_.
```

OpenWorkoutTracker has this C++ function I found via github search:

```c++
double VO2MaxCalculator::EstimateVO2MaxFromRaceDistanceInMeters(double raceDistanceMeters, double raceTimeMinutes)
{
	double speed = raceDistanceMeters / raceTimeMinutes;
	return -4.60 + 0.182258 * speed + 0.000104 * speed * speed;
}
```

so if you run a 40 minute 10k, that would give:

```js
> speed = 10000 / 40
< 250
> -4.6 + 0.182258 * speed + 0.000104 * speed * speed;
< 47.4645
```

but that's significantly lower than what daniels uses; if we try the calculation given first, we get:

```js
> 0.8 + 0.1894393 * Math.pow(Math.E, -0.012778 * 40) 
>     + 0.2989558 * Math.pow(Math.E, -0.1932605 * 40)
< 0.9137614442697204
```

and so:

```js
> 47.4645 / 0.9137614442697204
< 51.9440826680247
```

which matches [Daniels](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwibzcyx78z-AhWFGlkFHVOkDRAQFnoECAoQAQ&url=https%3A%2F%2Fwww.amazon.com%2FDaniels-Running-Formula-Jack-Tupper%2Fdp%2F1450431836&usg=AOvVaw1hK91oBpsmscEoCUfwdFVt) very closely
# Tessel-Calibrate

Tessel-Calibrate is a lightweight package that allows you to get a buffer of values, plus the high and low, from a number of Tessel modules.

Any module with a method formatted `module.method(callback(err, data){ ... })` can be called with `calibrate.get(module, 'method')`. The resulting values can be accessed via a promise:
```
calibrate.get(module, 'method').then() 
```
or as an event: 
```
calibrate.get(module, 'method'); 
calibrate.on(‘calibrated’, callback);
```

[See examples.](https://github.com/sarahgp/tessel-calibrate/blob/master/examples/calibrate-examples.js)

Modules supported include:
* [Ambient](https://github.com/tessel/ambient-attx4)
* [Climate](https://github.com/tessel/climate-si7005)
* [Color Sensor](https://www.npmjs.com/package/rgb-tcs34725)
* [Proximity](https://www.npmjs.com/package/proximity-hcsr04)
* [Grove Ultrasonic](https://www.npmjs.com/package/tessel-sen10737p)
* [Pulse Sensor](https://www.npmjs.com/package/pulsesensor)

## Installation
```
npm install tessel-calibrate --save
```

## Calling `calibrate.get`

The function takes two required arguments, the module you are using and the method name, the latter as a string. Eg: `calibrate.get(ambient, ‘getSoundbuffer’);`

It also takes an optional options hash, shown below with default values
``` 
{ returnsSingle: false,
  calls: 10,
  thresholds: {high: 1, low: 0} } 
```

Set `returnsSingle: true` if the method you are calling returns a single value instead of a buffer array, and `calibrate` will create and return an array for you.

If it is a single return method, you can also choose how many calls to use to create the buffer with `calls: num`. This will not work with `returnSingle: false`.

Finally I assume the values returned will be between 0 and 1. If not, set the hight and low thresholds by passing a hash with `high` and `low` values to `thresholds`.

## Returned Values
Calibrate always returns a hash with three values:
``` 
{ buffer: [], // array of values
  high: .012345,
  low: .000012 } 
```

## License
MIT

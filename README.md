# :mag: :clock230: Pico Frequency Finder
Finds the closest possible clocks to a given frequency for the [Raspberry Pi Pico](https://www.raspberrypi.com/products/raspberry-pi-pico/).
The output is a `CSV` formated list.
This tool uses `vcocalc.py` from the pico-sdk and just makes it conveniet to compare various frequency multipliers quickly.

## Getting started

1. Install [python 3.x](https://www.python.org/downloads/)
2. Clone
```sh
git@github.com:StateOff/pico_frequency_finder.git
cd pico_frequency_finder
```
3. Set `PICO_SDK_PATH` to a local clone of the [pico-sdk](https://github.com/raspberrypi/pico-sdk)
```sh
# Linux
export PICO_SDK_PATH="/home/stateoff/pico-sdk"

# Windows (cmd)
set PICO_SDK_PATH="C:\pico-sdk"
```
4. Run with a requested frequency as argument.
```sh
python frequency_finder.py --all --min_freq 50 --max_freq 180 3.579545454545454545
```
5. Sample output
```
             Error, Mult,        Requested Freq,         Achieved Freq,    Over-/Undercl,  FBDIV,   VCO,  PD1,  PD2
0.0000000000000000,   22,   78.7500000000000000,   78.7500000000000000,       -46.250000,    105,  1260,    4,    4
0.0048701298701275,   17,   60.8522727272727266,   60.8571428571428541,       -64.142857,     71,   852,    7,    2
0.0097402597402549,   34,  121.7045454545454533,  121.7142857142857082,        -3.285714,     71,   852,    7,    1
0.0113636363636402,   19,   68.0113636363636402,   68.0000000000000000,       -57.000000,    119,  1428,    7,    3
0.0211038961038952,   15,   53.6931818181818201,   53.7142857142857153,       -71.285714,     94,  1128,    7,    3
0.0259090909090958,   13,   46.5340909090909065,   46.5600000000000023,       -78.440000,     97,  1164,    5,    5
...
```

## Help

```
usage: frequency_finder.py [-h] [--all] [--max_freq MAX_FREQ] [--min_freq MIN_FREQ] [--input_freq INPUT_FREQ] [--version] requested_freq

Finds the closest possible clocks to a given frequency for the Raspberry Pi Pico.
This tool is based on the `vcocalc.py` tool from the pico-sdk.

Make sure to set the PICO_SDK_PATH environment variable.

Columns Description:
    Error -> Absolute difference between requested (multiplied) and achieved frequency
    Mult -> Integer multiplier of the requested frequency
    Requested Freq -> Multiplied Requested Frequency (requested_freq * Mult)
    Achieved Freq -> Possible frequency
    Over-/Undercl -> Difference to given input frequency
    FBDIV -> Feedback Divider
    VCO -> Voltage Controller Oscillator frequency (fbdiv * crystal_freq_khz)
    PD1 -> First Post Divider
    PD2 -> Second Post Divider
    
positional arguments:
  requested_freq        Desired frequency

options:
  -h, --help            show this help message and exit
  --all                 Print all result, by default the closest match(es) will be shown
  --max_freq MAX_FREQ   The maximum frequency the CPU can be overclocked to
  --min_freq MIN_FREQ   The minimum frequency the CPU can run with
  --input_freq INPUT_FREQ
                        The default CPU frequency used to calculate over-/underclock
  --version             Show version and exit
```

## License & Credits

This tool depends on the `vcocalc.py` tool in the pico-sdk by the raspberry pi foundation.

Written by Blazej Floch.

MIT compare `LICENSE`

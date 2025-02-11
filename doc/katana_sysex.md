# Startup Sequence

f0 7e 7f 06 01 f7 -> f0 7e 00 06 02 41 13 04 00 00 00 00 00 00 f7

f0 41 00 00 00 00 00 13 12 7f 00 00 01 00 00 f7

f0 41 00 00 00 00 00 13 12 7f 00 00 01 01 7f f7


# Message Anatomy

## Prefix

| Syx start | VendorId | DeviceID | ???            |
| --------- | -------- | -------- | -------------- |
| f0        | 41       | 00       | 00 00 00 00 13 |

f0 41 00 00 00 00 00 13

### Full Message Example

| Syx start | VendorId | DeviceID | ???            | Operation | Address     | Value | Checksum | SyxEnd |
| --------- | -------- | -------- | -------------- | --------- | ----------- | ----- | -------- | ------ |
| f0        | 41       | 00       | 00 00 00 00 13 | 12        | 60 00 00 34 | 00    | 6c       | f7     |

# Operations 

| Value | Function |
| ----- | -------- |
| 11    | Read     |
| 12    | Write    |

# Parameters

| addr        | type                                            | name       |
| ----------- | ----------------------------------------------- | ---------- |
| 60 00 00 3b | [On/Off Button](#On-Off)                        | Tweeter    |
| 60 00 00 3a | [3 State Colour Button](#3-State-Colour-Button) | High Mid   |
| 60 00 00 39 | [3 State Colour Button](#3-State-Colour-Button) | Low Mid    |
| 60 00 00 38 | [3 State Colour Button](#3-State-Colour-Button) | Blend      |
| 60 00 00 35 | [4 State Colour Button](#4-State-Colour-Button) | Shape      |
| 60 00 00 34 | [On/Off Button](#On-Off)                        | Pad        |
| 60 00 00 3f | [3 State Colour Button](#3-State-Colour-Button) | FX2        |
| 60 00 00 3d | [3 State Colour Button](#3-State-Colour-Button) | FX1        |
| 60 00 00 33 | [3 State Colour Button](#3-State-Colour-Button) | Drive      |
| 60 00 00 31 | [3 State Colour Button](#3-State-Colour-Button) | Comp       |
| 60 00 00 29 | [Slider](#Slider)                               | Treble     |
| 60 00 00 28 | [Slider](#Slider)                               | Mid High   |
| 60 00 00 27 | [Slider](#Slider)                               | Low Mid    |
| 60 00 00 26 | [Slider](#Slider)                               | Bass       |
| 60 00 00 25 | [Slider](#Slider)                               | Blend      |
| 60 00 00 24 | [Slider](#Slider)                               | Amp Volume |
| 60 00 00 23 | [Slider](#Slider)                               | Amp Gain   |
| 60 00 00 22 | [Amp Type](#amp-type)                           | Amp Type   |
| 60 00 00 2b | [Off-Slider](#Off-Slider)                       | FX2 Main   |
| 60 00 01 39 |                                                 | FX 2 Type  |

# FX2

## Chorus

A change of the FX2 Main will trigger a change in *Low Rate* and *High Rate* that is send from the AMP.


| addr        | type                      | name             |
| ----------- | ------------------------- | ---------------- |
| 60 00 00 2b | [Off-Slider](#Off-Slider) | FX2 Main         |
| 60 00 04 01 | [Slider](#Slider)         | Chorus Low Rate  |
| 60 00 04 05 | [Slider](#Slider)         | Chorus High Rate |
| 60 00 04 02 | [Slider](#Slider)         | Low Depth        |
| 60 00 04 06 | [Slider](#Slider)         | High Depth       |
| 60 00 04 03 | [Pre Delay](#pre-delay)   | Low Pre Delay    |
| 60 00 04 07 | [Pre Delay](#pre-delay)   | High Pre Delay   |
| 60 00 04 04 | [Slider](#Slider)         | Low Level        |
| 60 00 04 08 | [Slider](#Slider)         | High Level       |
| 60 00 04 09 | [Slider](#Slider)         | Direct Mix       |
| 60 00 04 00 | [Xover Freq](#xover-freq) | Xover Freq       |

# Value Types

## Off-Slider

### Range

| min | max |
| --- | --- |
| 0   | 101 |

### Values
| Value |     |
| ----- | --- |
| 0     | Off |

## Slider

### Range

| min | max |
| --- | --- |
| 0   | 100 |

## Pre Delay

### Range

| min | max |
| --- | --- |
| 0   | 80  |

### Values

0 - 40ms in 0.5ms steps

## Xover Freq

### Range

| min | max |
| --- | --- |
| 0   | 16  |

### Values

| Value | Freq    |
| ----- | ------- |
| 0     | 100Hz   |
| 1     | 125Hz   |
| 2     | 160Hz   |
| 3     | 200Hz   |
| 4     | 250Hz   |
| 5     | 315Hz   |
| 6     | 400Hz   |
| 7     | 500Hz   |
| 8     | 630Hz   |
| 9     | 800Hz   |
| 10    | 1.0kHz  |
| 11    | 1.25kHz |
| 12    | 1.6kHz  |
| 13    | 2.0kHz  |
| 14    | 2.5kHz  |
| 15    | 3.15kHz |
| 16    | 4.0kHz  |

## 3 State Colour Button

### Range

| min | max |
| --- | --- |
| 0   | 2   |

### Values

| Value | Colour |
| ----- | ------ |
| 0     | Green  |
| 1     | Red    |
| 2     | Yellow |

## 4 State Colour Button

### Range

| min | max |
| --- | --- |
| 0   | 3   |

### Values

| Value | Colour |
| ----- | ------ |
| 0     | Off    |
| 1     | Green  |
| 2     | Red    |
| 3     | Yellow |

## On Off

### Range

| min | max |
| --- | --- |
| 0   | 1   |

### Values

| Value | Colour |
| ----- | ------ |
| 0     | Off    |
| 1     | On     |

## Amp Type

Will also send the current value of the *tweeter* if changed on the panel

```f0 41 00 00 00 00 00 13 12 60 00 00 3b 00 65 f7```

```f0 41 00 00 00 00 00 13 12 60 00 00 3b 01 64 f7```


### Range

| min | max |
| --- | --- |
| 0   | 2   |

### Values

| Value | Type    |
| ----- | ------- |
| 0     | Vintage |
| 1     | Flat    |
| 2     | Modern  |





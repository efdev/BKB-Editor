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

| addr        | type                                                    | name                      |
| ----------- | ------------------------------------------------------- | ------------------------- |
| 60 00 00 3b | [On/Off Button](#On-Off)                                | Tweeter                   |
| 60 00 06 34 | [On/Off Button](#On-Off)                                | Send/Return               |
| 60 00 00 3a | [3 State Colour Button](#3-State-Colour-Button)         | High Mid                  |
| 60 00 00 39 | [3 State Colour Button](#3-State-Colour-Button)         | Low Mid                   |
| 60 00 00 38 | [3 State Colour Button](#3-State-Colour-Button)         | Blend                     |
| 60 00 00 35 | [4 State Colour Button](#4-State-Colour-Button)         | Shape                     |
| 60 00 00 34 | [On/Off Button](#On-Off)                                | Pad                       |
| 60 00 00 3f | [3 State Colour Button](#3-State-Colour-Button)         | FX2                       |
| 60 00 00 3d | [3 State Colour Button](#3-State-Colour-Button)         | FX1                       |
| 60 00 00 33 | [3 State Colour Button](#3-State-Colour-Button)         | Drive                     |
| 60 00 00 31 | [3 State Colour Button](#3-State-Colour-Button)         | Comp                      |
| 60 00 00 29 | [Slider](#Slider)                                       | Treble                    |
| 60 00 00 28 | [Slider](#Slider)                                       | Mid High                  |
| 60 00 00 27 | [Slider](#Slider)                                       | Low Mid                   |
| 60 00 00 26 | [Slider](#Slider)                                       | Bass                      |
| 60 00 00 25 | [Slider](#Slider)                                       | Blend                     |
| 60 00 00 24 | [Slider](#Slider)                                       | Amp Volume                |
| 60 00 00 23 | [Slider](#Slider)                                       | Amp Gain                  |
| 60 00 00 22 | [Amp Type](#amp-type)                                   | Amp Type                  |
| 60 00 00 2b | [Off-Slider](#Off-Slider)                               | FX2 Main                  |
| 60 00 01 38 | [FX2 Main Type](#fx2-main-type)                         | FX2 Main Type             |
| 60 00 01 39 | [FX2 FX Secondary Type](#fx2-fx-secondary-type)         | FX2 FX Secondary Type     |
| 60 00 01 3a | [FX2 Delay Secondary Type](#fx2-delay-secondary-type)   | FX2 Delay Secondary Type  |
| 60 00 01 3b | [FX2 Reverb Secondary Type](#fx2-reverb-secondary-type) | FX2 Reverb Secondary Type |

# FX2 FX

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

## Flanger

A change of the FX2 Main will trigger a change in *Rate* that is send from the AMP.


| addr        | type                                | name         |
| ----------- | ----------------------------------- | ------------ |
| 60 00 04 0a | [Slider](#Slider)                   | Rate         |
| 60 00 04 0b | [Slider](#Slider)                   | Depth        |
| 60 00 04 0d | [Slider](#Slider)                   | Resonance    |
| 60 00 04 0c | [Slider](#Slider)                   | Manual       |
| 60 00 04 0f | [Flanger Low Cut](#flanger-low-cut) | Low Cut      |
| 60 00 04 10 | [Slider](#Slider)                   | Effect Level |
| 60 00 04 11 | [Slider](#Slider)                   | Direct Mix   |

# Value Types

## FX2 Main Type

### Range

| min | max |
| --- | --- |
| 0   | 2   |

### Values

| Value |        |
| ----- | ------ |
| 0     | FX     |
| 1     | Reverb |
| 2     | Delay  |

## FX2 FX Secondary Type

### Range

| min | max |
| --- | --- |
| 0   | 23  |

### Values

| Value |                |
| ----- | -------------- |
| 0     | Chorus         |
| 1     | FLanger        |
| 2     | Phaser         |
| 3     | Uni-V          |
| 4     | Tremolo        |
| 5     | Vibrato        |
| 6     | Rotary         |
| 7     | Ring Mod       |
| 8     | Slow Gear      |
| 9     | T. WAH         |
| 10    | Graphic Eq     |
| 11    | Parametric Eq  |
| 12    | Octave         |
| 13    | Pitch Shifter  |
| 14    | Harmonist      |
| 15    | Humanizer      |
| 16    | Enhancer       |
| 17    | Bass Simulator |
| 18    | Defretter      |
| 19    | Bass Synth     |
| 20    | Auto Wah       |
| 21    | Heavy Octave   |
| 22    | Slicer         |

## FX2 Delay Secondary Type

### Range

| min | max |
| --- | --- |
| 0   | 5   |

### Values

| Value |           |
| ----- | --------- |
| 0     | Digital   |
| 1     | Analog    |
| 2     | Tape Echo |
| 3     | Reverse   |
| 4     | Modulate  |
| 5     | SDE-3000  |

## FX2 Reverb Secondary Type

### Range

| min | max |
| --- | --- |
| 0   | 4   |

### Values

| Value |          |
| ----- | -------- |
| 0     | Plate    |
| 1     | Room     |
| 2     | Hall     |
| 3     | Spring   |
| 4     | Modulate |


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


## Flanger Low Cut

### Range

| min | max |
| --- | --- |
| 0   | 10  |

### Values

| Value | Freq  |
| ----- | ----- |
| 0     | Flat  |
| 1     | 55Hz  |
| 2     | 110Hz |
| 3     | 165Hz |
| 4     | 200Hz |
| 5     | 280Hz |
| 6     | 340Hz |
| 7     | 400Hz |
| 8     | 500Hz |
| 9     | 630Hz |
| 10    | 800Hz |


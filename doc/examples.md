# Thumb Cluster

```yaml
TIMING:
  TAP_MILLISEC: 200
  DOUBLE_TAP_MILLISEC: 150

MAPPINGS:
  # left cluster
  - KEY: KEY_BACKSPACE
    TAP: KEY_BACKSPACE
    HOLD: KEY_LEFTSHIFT

  - KEY: KEY_ESC
    TAP: KEY_ESC
    HOLD: KEY_LEFTCTRL

  - KEY: KEY_TAB
    TAP: KEY_TAB
    HOLD: KEY_LEFTALT

  # right cluster
  - KEY: KEY_SPACE
    TAP: KEY_SPACE
    HOLD: KEY_RIGHTSHIFT

  - KEY: KEY_ENTER
    TAP: KEY_ENTER
    HOLD: KEY_RIGHTCTRL

  - KEY: KEY_DELETE
    TAP: KEY_DELETE
    HOLD: KEY_RIGHTALT
```

# Home Row Modifiers

```yaml
TIMING:
  TAP_MILLISEC: 200
  DOUBLE_TAP_MILLISEC: 150

# hold home row keys for modifiers
MAPPINGS:
  - KEY: KEY_A
    TAP: KEY_A
    HOLD: KEY_LEFTSHIFT

  - KEY: KEY_S
    TAP: KEY_S
    HOLD: KEY_LEFTCTRL

  - KEY: KEY_D
    TAP: KEY_D
    HOLD: KEY_LEFTALT

  - KEY: KEY_F
    TAP: KEY_F
    HOLD: KEY_LEFTMETA


  - KEY: KEY_J
    TAP: KEY_J
    HOLD: KEY_RIGHTMETA

  - KEY: KEY_K
    TAP: KEY_K
    HOLD: KEY_RIGHTALT

  - KEY: KEY_L
    TAP: KEY_L
    HOLD: KEY_RIGHTCTRL

  - KEY: KEY_SEMICOLON
    TAP: KEY_SEMICOLON
    HOLD: KEY_RIGHTSHIFT
```

# Key Combinations, No Double Tap

```yaml
TIMING:
  TAP_MILLISEC: 200
  DOUBLE_TAP_MILLISEC: 0
  SYNTHETIC_KEYS_PAUSE_MILLISEC: 10

MAPPINGS:
  # shifts tap ( ) like space cadet
  - KEY: KEY_LEFTSHIFT
    TAP: [ KEY_LEFTSHIFT, KEY_9, ]
    HOLD: KEY_LEFTSHIFT
  - KEY: KEY_RIGHTSHIFT
    TAP: [ KEY_LEFTSHIFT, KEY_0, ]
    HOLD: KEY_RIGHTSHIFT

  # alts tap < >
  - KEY: KEY_LEFTALT
    TAP: [ KEY_LEFTSHIFT, KEY_COMMA, ]
    HOLD: KEY_LEFTALT
  - KEY: KEY_RIGHTALT
    TAP: [ KEY_LEFTSHIFT, KEY_DOT, ]
    HOLD: KEY_RIGHTALT

  # tab to hyper modifier
  - KEY: TAB
    TAP: TAB
    HOLD: [ KEY_LEFTCTRL, KEY_LEFTMETA, KEY_LEFTALT, ] 
```

# Autoshift
```yaml
  - KEY: KEY_A
    TAP: KEY_A
    HOLD: [KEY_LEFTSHIFT, KEY_A]
    HOLD_START: AFTER_RELEASE

  - KEY: KEY_B
    TAP: KEY_B
    HOLD: [KEY_LEFTSHIFT, KEY_B]
    HOLD_START: AFTER_RELEASE

  - KEY: KEY_C
    TAP: KEY_C
    HOLD: [KEY_LEFTSHIFT, KEY_C]
    HOLD_START: AFTER_RELEASE
```
example by @calvinreu

# Complete Example (Thanks @heymajor !)

## Use case

- Caps Lock to Esc on tap / Ctrl on hold
- Enter to Enter on tap / Ctrl on hold
- Left Ctrl to `{` on tap / Ctrl on hold
- Right Ctrl to `}` on tap / Ctrl on hold
- Left Shift to `(` on tap / Shift on hold
- Right shift to `)` on tap / Shift on hold

## Setup

Laptop sometimes used with a wireless keyboard. Config for wired keyboard came out of troubleshooting overall setup.

## /etc/interception/udevmon.yaml
```yaml
- JOB: "intercept -g $DEVNODE | dual-function-keys -c /etc/interception/dual-function-keys/logitech.yaml | uinput -d $DEVNODE"
  DEVICE:
    NAME: "Logitech Wireless Keyboard PID:4023"
    EVENTS:
      EV_KEY: [KEY_CAPSLOCK, KEY_ENTER, KEY_LEFTSHIFT, KEY_RIGHTSHIFT, KEY_LEFTCTRL, KEY_RIGHTCTRL]

- JOB: "intercept -g $DEVNODE | dual-function-keys -c /etc/interception/dual-function-keys/lenovo.yaml | uinput -d $DEVNODE"
  DEVICE:
    NAME: "AT Translated Set 2 keyboard"
    EVENTS:
      EV_KEY: [KEY_CAPSLOCK, KEY_ENTER, KEY_LEFTSHIFT, KEY_RIGHTSHIFT, KEY_LEFTCTRL, KEY_RIGHTCTRL]

- JOB: "intercept -g $DEVNODE | dual-function-keys -c /etc/interception/dual-function-keys/dock.yaml | uinput -d $DEVNODE"
  DEVICE:
    NAME: "CHICONY USB Keyboard"
    EVENTS:
      EV_KEY: [KEY_CAPSLOCK, KEY_ENTER, KEY_LEFTSHIFT, KEY_RIGHTSHIFT, KEY_LEFTCTRL, KEY_RIGHTCTRL]
```

## /etc/interception/dual-function-keys/lenovo.yaml
```yaml
TIMING:
  TAP_MILLISEC: 200
  DOUBLE_TAP_MILLISEC: 150

MAPPINGS:
  - KEY: KEY_CAPSLOCK
    TAP: KEY_ESC
    HOLD: KEY_LEFTCTRL
  - KEY: KEY_ENTER
    TAP: KEY_ENTER
    HOLD: KEY_RIGHTCTRL
  - KEY: KEY_LEFTSHIFT
    TAP: [ KEY_LEFTSHIFT, KEY_9, ]
    HOLD: KEY_LEFTSHIFT
  - KEY: KEY_RIGHTSHIFT
    TAP: [ KEY_RIGHTSHIFT, KEY_0, ]
    HOLD: KEY_RIGHTSHIFT
  - KEY: KEY_LEFTCTRL
    TAP: [ KEY_LEFTSHIFT, KEY_LEFTBRACE, ]
    HOLD: KEY_LEFTCTRL
  - KEY: KEY_RIGHTCTRL
    TAP: [ KEY_RIGHTSHIFT, KEY_RIGHTBRACE, ]
    HOLD: KEY_RIGHTCTRL
```

## /etc/interception/dual-function-keys/logitech.yaml
```yaml
TIMING:
  TAP_MILLISEC: 200
  DOUBLE_TAP_MILLISEC: 150

MAPPINGS:
  - KEY: KEY_CAPSLOCK
    TAP: KEY_ESC
    HOLD: KEY_LEFTCTRL
  - KEY: KEY_ENTER
    TAP: KEY_ENTER
    HOLD: KEY_RIGHTCTRL
  - KEY: KEY_LEFTSHIFT
    TAP: KEY_KPLEFTPAREN
    HOLD: KEY_LEFTSHIFT
  - KEY: KEY_RIGHTSHIFT
    TAP: KEY_KPRIGHTPAREN
    HOLD: KEY_RIGHTSHIFT
  - KEY: KEY_LEFTCTRL
    TAP: [ KEY_LEFTSHIFT, KEY_LEFTBRACE, ]
    HOLD: KEY_LEFTCTRL
  - KEY: KEY_RIGHTCTRL
    TAP: [ KEY_RIGHTSHIFT, KEY_RIGHTBRACE, ]
    HOLD: KEY_RIGHTCTRL
```

## /etc/interception/dual-function-keys/dock.yaml
```yaml
TIMING:
  TAP_MILLISEC: 200
  DOUBLE_TAP_MILLISEC: 150

MAPPINGS:
  - KEY: KEY_CAPSLOCK
    TAP: KEY_ESC
    HOLD: KEY_LEFTCTRL
  - KEY: KEY_ENTER
    TAP: KEY_ENTER
    HOLD: KEY_RIGHTCTRL
  - KEY: KEY_LEFTSHIFT
    TAP: [ KEY_LEFTSHIFT, KEY_9, ]
    HOLD: KEY_LEFTSHIFT
  - KEY: KEY_RIGHTSHIFT
    TAP: [ KEY_RIGHTSHIFT, KEY_0, ]
    HOLD: KEY_RIGHTSHIFT
  - KEY: KEY_LEFTCTRL
    TAP: [ KEY_LEFTSHIFT, KEY_LEFTBRACE, ]
    HOLD: KEY_LEFTCTRL
  - KEY: KEY_RIGHTCTRL
    TAP: [ KEY_RIGHTSHIFT, KEY_RIGHTBRACE, ]
    HOLD: KEY_RIGHTCTRL
```

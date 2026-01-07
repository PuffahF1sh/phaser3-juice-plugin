# Phaser Juice Plugin API Documentation

This document explains the effects and parameters available in `phaserJuice.js`.

## Overview

The `phaserJuice` class provides a set of juice effects for Phaser 3 sprites. Most effects use tweens and allow for configuration overrides.

**Usage:**
```javascript
this.juice = new phaserJuice(this); // 'this' is the Phaser Scene
this.juice.shake(target);
```

**Method Chaining:**
You can chain methods by setting a target first using `add(target)` or by relying on the return value of effects.
```javascript
this.juice.add(sprite).shake().flash();
```

**Chaining with Parameters:**
When using method chaining, if you wish to provide configuration options for an effect, you must pass `null` as the first argument (the target). This signals the effect to use the previously added target.

```javascript
this.juice.add(sprite)
    .shake(null, { duration: 500 })
    .fadeIn(null, { duration: 200 });
```

## Shared Conccepts

### Configuration Object
Most effects accept a `config` object as a parameter. This object allows you to override the default settings for the effect. If a property is not specified in the `config` object, the default value for that effect is used.

Common properties available for override in most effects:
- `duration`: (number) Duration of the effect in ms.
- `delay`: (number) Delay before starting the effect in ms.
- `paused`: (boolean) Whether the effect starts paused.
- `ease`: (string) The ease function to use.
- `yoyo`: (boolean) Whether the tween yoyos.
- `repeat`: (number) Number of times to repeat (-1 for infinite).
- `onStart`: (function) Callback when the effect starts.
- `onComplete`: (function) Callback when the effect completes.
- Specific properties like `x`, `y`, `alpha`, `scaleX`, `scaleY`, `angle` depending on the effect.

### Destroy Parameter
Most effects take an optional `destroy` boolean parameter. If `true`, the effect (tween) will be removed/destroyed when the `onComplete` event fires. Default is `false`.

---

## Methods

### `add(target)`
Sets the target sprite for subsequent chained method calls.

- **Parameters:**
    - `target` (object): The sprite to target.
- **Returns:** The `phaserJuice` instance for chaining.

---

### `shake(target, config, destroy)`
Shakes the sprite. Defaults to shaking on the x-axis.

- **Parameters:**
    - `target` (object): Sprite to shake.
    - `config` (object, optional): Configuration overrides.
    - `destroy` (boolean, optional): Destroy tween on complete. Default `false`.

- **Default Config:**
    ```javascript
    {
        x: 5,
        y: 0,
        duration: 50,
        yoyo: true,
        repeat: 8,
        ease: 'Bounce.easeInOut',
        delay: 0,
        paused: false
    }
    ```

### `shakeY(target)`
Helper alternative that shakes the sprite on the y-axis instead of x.

- **Parameters:**
    - `target` (object): Sprite to shake.

- **Configuration:** Uses `shake` with `{ x: 0, y: 5 }`.

---

### `wobble(target, config, destroy)`
Adds a slight wobble to the sprite.

- **Parameters:**
    - `target` (object): Sprite to wobble.
    - `config` (object, optional): Configuration overrides.
    - `destroy` (boolean, optional): Destroy tween on complete. Default `false`.

- **Default Config:**
    ```javascript
    {
        x: 20,
        y: 0,
        duration: 150,
        yoyo: true,
        repeat: 5,
        ease: 'Sine.easeInOut',
        delay: 0,
        paused: false
    }
    ```

### `wobbleY(target)`
Helper alternative that wobbles the sprite on the y-axis instead of x.

- **Parameters:**
    - `target` (object): Sprite to wobble.

- **Configuration:** Uses `wobble` with `{ x: 0, y: 20 }`.

---

### `scaleUp(target, config, destroy)`
Scales up the sprite.

- **Parameters:**
    - `target` (object): Sprite to grow.
    - `config` (object, optional): Configuration overrides.
    - `destroy` (boolean, optional): Destroy tween on complete. Default `false`.

- **Default Config:**
    ```javascript
    {
        scaleX: target.scaleX + 0.25,
        scaleY: target.scaleY + 0.25,
        duration: 750,
        delay: 0,
        paused: false
    }
    ```

### `scaleDown(target, config, destroy)`
Scales down the sprite.

- **Parameters:**
    - `target` (object): Sprite to shrink.
    - `config` (object, optional): Configuration overrides.
    - `destroy` (boolean, optional): Destroy tween on complete. Default `false`.

- **Default Config:**
    ```javascript
    {
        scaleX: target.scaleX - 0.25,
        scaleY: target.scaleY - 0.25,
        duration: 750,
        delay: 0,
        paused: false
    }
    ```

---

### `pulse(target, config, destroy)`
Pulses the sprite (scales up and back down).

- **Parameters:**
    - `target` (object): Sprite to pulse.
    - `config` (object, optional): Configuration overrides.
    - `destroy` (boolean, optional): Destroy tween on complete. Default `false`.

- **Default Config:**
    ```javascript
    {
        scaleX: target.scaleX * 1.25,
        scaleY: target.scaleY * 1.25,
        duration: 750,
        repeat: 2,
        yoyo: true,
        ease: 'Quad.easeInOut',
        delay: 0,
        paused: false
    }
    ```

---

### `flash(target, duration, color)`
Flashes the sprite with a specific color.
**Note:** `flash` does not use a tween and does not accept a `config` object or `destroy` parameter.

- **Parameters:**
    - `target` (object): Sprite to flash.
    - `duration` (number, optional): Duration of the flash in ms. Default `150`.
    - `color` (string, optional): Color to flash. Default `'0xffffff'`.

---

### `rotate(target, config, destroy)`
Rotates the sprite.

- **Parameters:**
    - `target` (object): Sprite to rotate.
    - `config` (object, optional): Configuration overrides.
    - `destroy` (boolean, optional): Destroy tween on complete. Default `false`.

- **Default Config:**
    ```javascript
    {
        angle: 360,
        duration: 500,
        ease: 'Circular.easeInOut',
        delay: 0,
        paused: false
    }
    ```

---

### `bounce(target, config, destroy)`
Bounces the sprite on the y-axis.

- **Parameters:**
    - `target` (object): Sprite to bounce.
    - `config` (object, optional): Configuration overrides.
    - `destroy` (boolean, optional): Destroy tween on complete. Default `false`.

- **Default Config:**
    ```javascript
    {
        y: 25,
        duration: 1000,
        ease: 'Bounce',
        delay: 0,
        paused: false
    }
    ```

---

### `fadeIn(target, config, destroy)`
Fades in the sprite (sets alpha to 1).

- **Parameters:**
    - `target` (object): Sprite to fade in.
    - `config` (object, optional): Configuration overrides.
    - `destroy` (boolean, optional): Destroy tween on complete. Default `false`.

- **Default Config:**
    ```javascript
    {
        alpha: 1,
        duration: 750,
        ease: 'Circular.easeIn',
        delay: 0,
        paused: false
    }
    ```

### `fadeOut(target, config, destroy)`
Fades out the sprite (sets alpha to 0).

- **Parameters:**
    - `target` (object): Sprite to fade out.
    - `config` (object, optional): Configuration overrides.
    - `destroy` (boolean, optional): Destroy tween on complete. Default `false`.

- **Default Config:**
    ```javascript
    {
        alpha: 0,
        duration: 750,
        ease: 'Circular.easeOut',
        delay: 0,
        paused: false
    }
    ```

### `fadeInOut(target, config, destroy)`
Fades the sprite in and out.

- **Parameters:**
    - `target` (object): Sprite to fade in and out.
    - `config` (object, optional): Configuration overrides.
    - `destroy` (boolean, optional): Destroy tween on complete. Default `false`.

- **Default Config:**
    ```javascript
    {
        alpha: 0,
        duration: 500,
        yoyo: true,
        repeat: 3,
        ease: 'Circular.easeInOut',
        delay: 0,
        paused: false
    }
    ```

---

### `flipX(target, direction, config, destroy)`
Flips the sprite on the x-axis.
**Warning:** This effect scales the sprite and can cause unintended side effects found in scaling (e.g. flipping physics bodies).

- **Parameters:**
    - `target` (object): Sprite to flip.
    - `direction` (boolean, optional): `true` to flip (-1 scale), `false` to flip back (1 scale). Default `true`.
    - `config` (object, optional): Configuration overrides.
    - `destroy` (boolean, optional): Destroy tween on complete. Default `false`.

- **Default Config:**
    ```javascript
    {
        scaleX: direction ? -1 : 1,
        duration: 500,
        ease: 'Sine.easeInOut',
        delay: 0,
        paused: false
    }
    ```

### `flipY(target, direction, config, destroy)`
Flips the sprite on the y-axis.
**Warning:** This effect scales the sprite.

- **Parameters:**
    - `target` (object): Sprite to flip.
    - `direction` (boolean, optional): `true` to flip (-1 scale), `false` to flip back (1 scale). Default `true`.
    - `config` (object, optional): Configuration overrides.
    - `destroy` (boolean, optional): Destroy tween on complete. Default `false`.

- **Default Config:**
    ```javascript
    {
        scaleY: direction ? -1 : 1,
        duration: 500,
        ease: 'Sine.easeInOut',
        delay: 0,
        paused: false
    }
    ```

---

### `spinX(target, direction, config, destroy)`
Spins the sprite on the x-axis.
**Warning:** This effect scales the sprite.

- **Parameters:**
    - `target` (object): Sprite to spin.
    - `direction` (boolean, optional): `true` to spin (-1 scale), `false` to spin back (1 scale). Default `true`.
    - `config` (object, optional): Configuration overrides.
    - `destroy` (boolean, optional): Destroy tween on complete. Default `false`.

- **Default Config:**
    ```javascript
    {
        scaleX: direction ? -1 : 1,
        duration: 500,
        yoyo: true,
        repeat: 3,
        ease: 'Sine.easeInOut',
        delay: 0,
        paused: false
    }
    ```

### `spinY(target, direction, config, destroy)`
Spins the sprite on the y-axis.
**Warning:** This effect scales the sprite.

- **Parameters:**
    - `target` (object): Sprite to spin.
    - `direction` (boolean, optional): `true` to spin (-1 scale), `false` to spin back (1 scale). Default `true`.
    - `config` (object, optional): Configuration overrides.
    - `destroy` (boolean, optional): Destroy tween on complete. Default `false`.

- **Default Config:**
    ```javascript
    {
        scaleY: direction ? -1 : 1,
        duration: 500,
        yoyo: true,
        repeat: 3,
        ease: 'Sine.easeInOut',
        delay: 0,
        paused: false
    }
    ```

---

### `reset(target)`
Helper function to reset a sprite back to its original state.
Resets the sprite to:
- Alpha: 1
- Scale: 1
- Angle: 0
- Tint: None (`0xffffff`)

- **Parameters:**
    - `target` (object): Sprite to reset.


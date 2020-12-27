---
id: version-0.62-animatedvaluexy
title: Animated.ValueXY
original_id: animatedvaluexy
---

##### 本文档贡献者：[sunnylqm](https://github.com/search?q=sunnylqm&type=Users)(100.00%)

2D Value for driving 2D animations, such as pan gestures. Almost identical API to normal [`Animated.Value`](animatedvalue.md), but multiplexed. Contains two regular `Animated.Value`s under the hood.

## 示例

```SnackPlayer name=Animated.ValueXY
import React, { useRef } from "react";
import { Animated, PanResponder, StyleSheet, View } from "react-native";

const DraggableView = () => {
  const pan = useRef(new Animated.ValueXY()).current;

  const panResponder = PanResponder.create({
    onStartShouldSetPanResponder: () => true,
    onPanResponderMove: Animated.event([
      null,
      {
        dx: pan.x, // x,y are Animated.Value
        dy: pan.y,
      },
    ]),
    onPanResponderRelease: () => {
      Animated.spring(
        pan, // Auto-multiplexed
        { toValue: { x: 0, y: 0 } } // Back to zero
      ).start();
    },
  });

  return (
    <View style={styles.container}>
      <Animated.View
        {...panResponder.panHandlers}
        style={[pan.getLayout(), styles.box]}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
  box: {
    backgroundColor: "#61dafb",
    width: 80,
    height: 80,
    borderRadius: 4,
  },
});

export default DraggableView;
```

---

# 文档

## 方法

### `setValue()`

```jsx
setValue(value);
```

Directly set the value. This will stop any animations running on the value and update all the bound properties.

**参数：**

| 名称  | 类型   | 必填 | 说明 |
| ----- | ------ | ---- | ---- |
| value | number | 是   |      |

---

### `setOffset()`

```jsx
setOffset(offset);
```

Sets an offset that is applied on top of whatever value is set, whether via `setValue`, an animation, or `Animated.event`. Useful for compensating things like the start of a pan gesture.

**参数：**

| 名称   | 类型   | 必填 | 说明 |
| ------ | ------ | ---- | ---- |
| offset | number | 是   |      |

---

### `flattenOffset()`

```jsx
flattenOffset();
```

Merges the offset value into the base value and resets the offset to zero. The final output of the value is unchanged.

---

### `extractOffset()`

```jsx
extractOffset();
```

Sets the offset value to the base value, and resets the base value to zero. The final output of the value is unchanged.

---

### `addListener()`

```jsx
addListener(callback);
```

Adds an asynchronous listener to the value so you can observe updates from animations. This is useful because there is no way to synchronously read the value because it might be driven natively.

Returns a string that serves as an identifier for the listener.

**参数：**

| 名称     | 类型     | 必填 | 说明                                                                                        |
| -------- | -------- | ---- | ------------------------------------------------------------------------------------------- |
| callback | function | 是   | The callback function which will receive an object with a `value` key set to the new value. |

---

### `removeListener()`

```jsx
removeListener(id);
```

Unregister a listener. The `id` param shall match the identifier previously returned by `addListener()`.

**参数：**

| 名称 | 类型   | 必填 | 说明                               |
| ---- | ------ | ---- | ---------------------------------- |
| id   | string | 是   | Id for the listener being removed. |

---

### `removeAllListeners()`

```jsx
removeAllListeners();
```

Remove all registered listeners.

---

### `stopAnimation()`

```jsx
stopAnimation([callback]);
```

Stops any running animation or tracking. `callback` is invoked with the final value after stopping the animation, which is useful for updating state to match the animation position with layout.

**参数：**

| 名称     | 类型     | 必填 | 说明                                          |
| -------- | -------- | ---- | --------------------------------------------- |
| callback | function | 否   | A function that will receive the final value. |

---

### `resetAnimation()`

```jsx
resetAnimation([callback]);
```

Stops any animation and resets the value to its original.

**参数：**

| 名称     | 类型     | 必填 | 说明                                             |
| -------- | -------- | ---- | ------------------------------------------------ |
| callback | function | 否   | A function that will receive the original value. |

---

### `getLayout()`

```jsx
getLayout();
```

Converts `{x, y}` into `{left, top}` for use in style, e.g.

```jsx
style={this.state.anim.getLayout()}
```

---

### `getTranslateTransform()`

```jsx
getTranslateTransform();
```

Converts `{x, y}` into a useable translation transform, e.g.

```jsx
style={{
  transform: this.state.anim.getTranslateTransform()
}}
```

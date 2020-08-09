# Animations

Animations are very important to create a great user experience. Objects in motion have momentum and rarely come to a stop immediately. Animations allow you to convey physically believable motion in your interface.

So in React Native, there are two complementary animation systems:

- Animated API
- LayoutAnimation API

<br>

![](https://miro.medium.com/max/480/1*bB-d47zxIFGYdm9Hx76ueg.gif)

# Animated API

Animated API focuses on declarative relationships between inputs and outputs, with configurable transforms in between, and start/stop methods to control time-based animation execution.

Animated exports six animatable component types:
View, Text, Image, ScrollView, FlatList, and SectionList, but you can also create your own using Animated.createAnimatedComponent()

# Methods you should know in Animated API!

There are three main Animated methods that you can use to create animations:

1.  **Animated.timing():** Maps time range to easing value.

1.  **Animated.decay():** starts with an initial velocity and gradually slows to a stop.

1.  **Animated.spring():** Simple single-spring physics model (Based on Rebound and Origami).

#### How to call these methods

There are three ways to call these animations methods along with calling them individually:

1. **Animated.parallel()**: Starts an array of animations all at the same time.

<br>

1. **Animated.sequence()**: Starts an array of animations in order, waiting for each to complete before starting the next. If the currently running animation is stopped, no following animations will be started.
   <br>

1. **Animated.stagger()**: An array of animations may run in parallel (overlap), but are started in sequence with successive delays. Very similar to Animated.parallel() but allows you to add delays to the animations.

## Example 
```js
import React, { useRef, useEffect } from 'react';
import { Animated, Text, View } from 'react-native';

const FadeInView = (props) => {
  const fadeAnim = useRef(new Animated.Value(0)).current  // Initial value for opacity: 0

  React.useEffect(() => {
    Animated.timing(
      fadeAnim,
      {
        toValue: 1,
        duration: 10000,
      }
    ).start();
  }, [fadeAnim])

  return (
    <Animated.View                 // Special animatable View
      style={{
        ...props.style,
        opacity: fadeAnim,         // Bind opacity to animated value
      }}
    >
      {props.children}
    </Animated.View>
  );
}

// You can then use your `FadeInView` in place of a `View` in your components:
export default () => {
  return (
    <View style={{flex: 1, alignItems: 'center', justifyContent: 'center'}}>
      <FadeInView style={{width: 250, height: 50, backgroundColor: 'powderblue'}}>
        <Text style={{fontSize: 28, textAlign: 'center', margin: 10}}>Fading in</Text>
      </FadeInView>
    </View>
  )
}
```
# Exercises

let's do some Exercises together with rect-native Animated API

- add fade animation to the button in your Home page 
- add animation to ScrollView in your List page
[this link will help you](https://reactnative.dev/docs/animations)

# LayoutAnimation API

LayoutAnimation is very powerful and can be quite useful, it provides much less control than Animated and other animation libraries, so you may need to use another approach if you can't get LayoutAnimation to do what you want.

to know more about LayoutAnimation [here](https://github.com/facebook/react-native/blob/master/Libraries/LayoutAnimation/LayoutAnimation.js)

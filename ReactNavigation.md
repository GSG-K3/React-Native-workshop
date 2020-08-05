# React Navigation:

React Navigation is made up of some core utilities and those are then used by navigators to create the navigation structure in your app.

# Create Bottom Tab Navigator

A simple tab bar on the bottom of the screen that lets you switch between different routes.

# Installation

Open a Terminal in your project's folder and run:

```js
npm install @react-navigation/native
```

```js
expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view
```

The libraries we've installed so far are the building blocks and shared foundations for navigators

to use BottomTabNavigator you have to intall

```js
npm install @react-navigation/bottom-tabs

```

# Example:

for this expample let's pretend you have three pages you want to switch between them useing bottom tab navigator so first you import them to the app.js file

NavigationContainer is a component which manages our navigation tree and contains the navigation state. This component must wrap all navigators structure

```js
import React from 'react';
import Home from './components/Home';
import List from './components/List';
import NewItem from './components/NewItems';

import { NavigationContainer } from '@react-navigation/native';
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';

import { MaterialCommunityIcons } from '@expo/vector-icons';
const Tab = createBottomTabNavigator();

const TabNavigator = () => (
  <Tab.Navigator>
    <Tab.Screen name="List" component={List} />
    <Tab.Screen name="NewItem" component={NewItem} />
    <Tab.Screen
      name="Home"
      component={Home}
      options={{
        tabBarIcon: ({ size }) => {
          <MaterialCommunityIcons name="home" size={size} />;
        },
      }}
    />{' '}
    // the tab.screen accepts options props where you can set an icon change
    color,title and many things
  </Tab.Navigator>
);

export default function App() {
  return (
    <NavigationContainer>
      <TabNavigator />
    </NavigationContainer>
  );
}
```

# Resources:

- [React Navigation](https://reactnavigation.org/)

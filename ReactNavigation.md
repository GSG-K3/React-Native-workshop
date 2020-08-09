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

for this expample let's pretend you have two pages you want to switch between them using bottom tab navigator so first you import them to the app.js file

NavigationContainer is a component which manages our navigation tree and contains the navigation state. This component must wrap all navigators structure

creating a BottomTab navigator
createBottomTabNavigator is a function that returns an object containing 2 properties: Screen and Navigator. Both of them are React components used for configuring the navigator. The Navigator should contain Screen elements as its children to define the configuration for routes.

A route can be specified by using the Screen component. The Screen component accepts a name prop which corresponds to the name of the route we will use to navigate, and a component prop which corresponds to the component it'll render.

the Tab.Navigator component accepts following props:

- initialRouteName:The name of the route to render on first load of the navigator.

- screenOptions:Default options to use for the screens in the navigator.

- tabBarOptions :An object containing the props for the default tab bar component. If you're using a custom tab bar, these will be passed as props to the tab bar and you can handle them.

The tab.screen accepts options props where you can set an icon change
color and many things

```js
import React from 'react';
import Home from './Screens/Home';
import List from './Screens/List';

import { NavigationContainer } from '@react-navigation/native';
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';
import Icon from 'react-native-vector-icons/FontAwesome';

const Tab = createBottomTabNavigator();

const TabNavigator = () => (
<Tab.Navigator
    tabBarOptions={{
      activeBackgroundColor: '#841584',
      inactiveTintColor: 'gray',
      activeTintColor: 'white',
    }}
    screenOptions={({ route }) => ({
      tabBarIcon: ({ focused, color, size }) => {
        let iconName;

        if (route.name === 'Home') {
          iconName = focused ? 'home' : 'home';
        } else if (route.name === 'example') {
          iconName = focused ? 'user' : 'user';
        }

        // You can return any component that you like here!
        return <Icon name={iconName} size={size} color={color} />;
      },
    })}
  >
    <Tab.Screen
      name="Home"
      component={Home}
      options={{
        tabBarBadge: 3,
      }}
    />
    <Tab.Screen name="List" component={List} />
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

# Exercise

return to your app and split the home function code into pages on called Home and the other page called List

- the home page containe the form of adding new user
- the List page containe the users cards
  then switch between the pages using navigatin Tab bottom

# Resources:

- [React Navigation](https://reactnavigation.org/)

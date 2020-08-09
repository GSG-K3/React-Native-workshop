# React Native Elements
In Mobile Apps UI has huge impact on the users,so it's important thing to use UI library to help you create amazing experience for the users.
 React Native Elements is a styling library with pre-built components to replace the basic, limited React Native components. It’s similar to Material UI, giving you useable styles that you can customize in your own way. Every one of the components in React Native Elements is wrapped with the basic React Native <View /> component with styling based on the props you indicate.

 Befor we start , we have to Install React Native Elements in our project 
 ```
$ yarn add react-native-elements
# or with npm
$  npm install react-native-elements
```
Then Install react-native-vector-icons
```
$ npm i --save react-native-vector-icons
```
let's take a look on the [React Native Elements Components](https://react-native-elements.github.io/react-native-elements/docs/overview) to see how much useful it can be.

now we can start using React Native Elements by adding `ThemeProvider` and `theme` in our app:

```js
import { ThemeProvider } from 'react-native-elements';

const theme = {  
  Button: {        //If you want to have the same styling for 
    titleStyle: {  // every Button you can add your magic here
      color: 'white',// I hope you are more creative than me
    },
    buttonStyle: {
        borderRadius: 5,
        margin: 10,
        },
  },
};

const MyApp = () => {
  return (
    <ThemeProvider theme={theme} >
      {/* Rest of your app code */}
    </ThemeProvider>
  );
};
```



create now file to make our Home page, import all the elements you need from `react-native-elements` ,add Header, Input, Button for example :

---
> **_NOTE:_**
> you can use `expo-constants`, make's your app look better if don't want to add a Header. 
>```console
>$ expo install expo-constants
>```
>import it :
>```js
>import Constants from 'expo-constants';
>```
>add it to  `<View>` style this way :
>```js
>paddingTop: Constants.statusBarHeight,
>```
>this means you will set a paddingTop to your component equal to the status bar, and since the status bar height changes with each (android / ios) device, you can't just put a fixed value. 
>
---

```js
import { Button ,Text,Header, Input} from 'react-native-elements';
import {StyleSheet,View} from 'react-native'
import Icon from 'react-native-vector-icons/FontAwesome';
import React, { useState } from 'react';
import Constants from 'expo-constants';

const Home = ()=> {
  const [name, setName] = useState(null);
  const [email, setEmail] = useState(null);
return (
    <View >
         <Header
            leftComponent={{
                 icon: 'menu',
                  color: '#fff' 
                  }}
            centerComponent={{
                 text: 'MY APP', 
                 style: { 
                     color: '#fff' } 
                     }}
            rightComponent={{
                 icon: 'comment', 
                 color: '#fff' 
                 }}
            backgroundColor='#841584'
            />    
    <View style={styles.container}>  
      <Input
        label='Enter your name'
        leftIcon={
            <Icon
            name='user'
            size={24}
            color='#841584'
            />
        }
        placeholder='Name'
        onChangeText={(text)=>setName(text)}
        />
        <Input
        label='Enter your Email'
        leftIcon={
            <Icon
            name='at'
            size={24}
            color='#841584'
            />}
        placeholder='E-mail'
        onChangeText={(text)=>setEmail(text)}
        />
      <Button
      title="Submit"
      buttonStyle={{backgroundColor:"#841584"}}
      onPress={() => console.log(name , email)}
      />
    </View>
    </View>
  );
}

const styles = StyleSheet.create({
    container: {
      backgroundColor: '#fff',
      paddingTop: Constants.statusBarHeight,
      height:'100%',
      padding:10,
    },
  });

```
import your Home page in to your App function and see if you need to add anything else

now .... we have to move on,to learn more .



 ### Resources:
- [React Native Elements](https://react-native-elements.github.io/react-native-elements/docs/)
- [A Look at the React Native Elements UI Toolkit](https://www.digitalocean.com/community/tutorials/react-react-native-elements)

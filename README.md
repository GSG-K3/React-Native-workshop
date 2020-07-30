# React-Native-workshop
Introduction For React Native 

## React-Native 

React Native is a JavaScript framework Allow you to writes real, natively rendering mobile applications for iOS and Android ,based on React.
You can create code just once and use it to power both their iOS and Android apps. This translates to huge time and resource savings. ,React Native has the ability to render APIs in Objective-C (for iOS) or Java (for Android),your application will render using “bridge” to become real mobile UI components,and will look and feel like any other mobile application,your React Native apps can access platform features like the phone camera, or the user’s location.

![Test Image 1](https://www.netguru.com/hs-fs/hubfs/image10-Jul-03-2020-11-20-54-82-AM.png?width=1600&name=image10-Jul-03-2020-11-20-54-82-AM.png)

Now we can start building our first React Native App ,to do that you can follow the steps below:
### 1.Install React Native :
Assuming that you not familiar with mobile development,you will need Node 12 LTS to use npm to install the Expo CLI command line utility:
```
$ npm install -g expo-cli
```
Then run the following commands to create a new React Native project :
```
$ expo init myFirstNative
$ cd myFirstNative
$ code .
```

### 2.let's modify it
Open App.js in your text editor and edit some lines:

```js
import React from 'react';
import { StyleSheet, Text, View, Button, Alert } from 'react-native';

export default function App() {

return (
    <View style={styles.container}>
      <Text style={styles.title}>This Is My First React Native App</Text>
      <View style={styles.buttonContainer}>
      <Button
      title="click me"
      color="#841584"
      onPress={() => Alert.alert('Good Job Freinds')}
      />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
  title: {
    fontSize:25,
  },
  buttonContainer:{
    padding: 10
  },
  });
```
You can take alook at [React Native Components and API](https://reactnative.dev/docs/components-and-apis) If you want to add more elements to your app, and to learn more about iOS and Android-specific components.

run the following command in your terminal
```
$ npm start
```
Now If you want to see your changes....there is two ways to do it:

- Install the Expo client app on your iOS or Android phone and connect to the same wireless network as your computer. On Android, use the Expo app to scan the QR code from your terminal to open your project. On iOS, use the built-in QR code scanner of the Camera app.
- you can launch your app on an [Android Virtual Device](https://docs.expo.io/workflow/android-studio-emulator/) by running npm run android, or on the [iOS Simulator](https://docs.expo.io/workflow/ios-simulator/) by running npm run ios (macOS only).

You can use the first way to save time.

### 3.Let's build a simple connection with database :

I choose [SQLite](https://docs.expo.io/versions/v38.0.0/sdk/sqlite/) for this example ,you can find more options for storing data, I found SQLite a good choice and easy to learn. :stuck_out_tongue_winking_eye: The truth is because the sqlStatement very familiar to me, other option was not familiar.
#### SQLite 
gives your app access to a database that can be queried through a WebSQL-like API. The database is persisted across restarts of your app.

Now we have to install SQLite in our app 
```
$ expo install expo-sqlite
```
In your App.js , import SQLite like this :
```js
import * as SQLite from 'expo-sqlite';
```
Creating database will be in one line `SQLite.openDatabase('databaseName.db')` ,so you don't need to build a server to do the connection between your app and the database.
For create , select and insert we can use `db.transaction(callback, error, success)` method ,transaction supports one method :`tx.executeSql(sqlStatement, arguments, success, error)`.
here is an example for creating table and adding users to database using transaction:

```js
import React, {useState, useEffect} from 'react';
import { StyleSheet, View, Button, Alert,
  TextInput, SafeAreaView } from 'react-native';
import * as SQLite from 'expo-sqlite';


export default function App() {
  const [name , setName]=useState(null);
  const [email , setEmail]=useState(null)
//this line will open a connection with database or create one if it's not existed
  const db = SQLite.openDatabase('mynative.db');   //database name should end with .db

  useEffect(()=>{
      db.transaction(tx => {
        tx.executeSql(  //this will never execute unless the table not existed ,that means it will execute for on time only
          'create table if not exists users (id integer primary key not null, name text not null, email text not null)'
        );
         //every time you reload your app this line will be executed
          tx.executeSql('select * from users;', [],(_, { rows }) =>{  
            console.log(rows._array)  //you can see the result in your terminal
        }
        );
        }
      );  
  
  })

  const addUser = () => {
    if(name!=null && email!= null){
      db.transaction(
        tx => {  
          tx.executeSql('insert into users (name, email) values ($1, $2);',
          [name,email],
          () => Alert.alert('you added user successfully'),
          (error) => {
            if(error) Alert.alert('try again !!')});
          
        }
      );
    }
  }


  return (
    <View style={styles.container}>
       <SafeAreaView >
      <View>
        <TextInput 
        placeholder='Name'
        value={name}
        onChangeText={(text)=>setName(text)}
        style={styles.input}
        />
        <TextInput 
        placeholder='Email'
        value={email}
        onChangeText={(text)=>setEmail(text)}
        style={styles.input}
        />
        <Button
         title='Add User'
         color='#841584'
         onPress={ addUser}
          />
      </View>
    </SafeAreaView>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
  input:{
    width:200,
    height:40,
    margin:15,
    
  },
});
```
The result that returned from `executeSql()` will be like :
```js
{
  insertId,      //(number) The row ID of the row that the SQL statement inserted into the database, if a row was inserted.
  rowsAffected,  // (number) The number of rows that were changed by the SQL statement.
  rows: {
    length,      //(number) The number of rows returned by the query.
    item(),      //(function) rows.item(index) returns the row with the given index. If there is no such row, returns null.
    _array,      //The actual array of rows returned by the query.
  },
}
```

:computer: I hope that was useful for you :computer:




### Resources:
- [expo](https://expo.io/learn)
- [React-native setup](https://reactnative.dev/docs/environment-setup#docsNav)
- [SQLite](https://docs.expo.io/versions/latest/sdk/sqlite/)

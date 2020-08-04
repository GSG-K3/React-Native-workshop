# React Native & Database

### Let's build a simple connection to your App with database :

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
         tx.executeSql('select * from users;',
            [],
            (_, { rows: { _array } }) => console.log(_array),//here you can do your magic with data
            () => console.log("error fetching")
            );  //you can see the result in your terminal
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
### Resources:
- [SQLite](https://docs.expo.io/versions/latest/sdk/sqlite/)
- [React-Native with SQLite](https://medium.com/swlh/react-native-with-sqlite-1ec64702e35e)
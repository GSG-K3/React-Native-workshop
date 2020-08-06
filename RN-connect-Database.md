# React Native & Database

### Let's build a simple connection to your App with database :

I choose [SQLite](https://docs.expo.io/versions/v38.0.0/sdk/sqlite/) for this example ,you can find more options for storing data, I found SQLite a good choice and easy to learn. :stuck_out_tongue_winking_eye: The truth is because the sqlStatement very familiar to me, other option was not familiar.

#### SQLite

gives your app access to a database that can be queried through a WebSQL-like API. The database is persisted across restarts of your app.

Now we have to install SQLite in our app

```console
$ expo install expo-sqlite
```

In your App.js , import SQLite like this :

```js
import * as SQLite from 'expo-sqlite';
```

Creating database will be in one line `SQLite.openDatabase('databaseName.db')` ,so you don't need to build a server to do the connection between your app and the database.
For create , select and insert we can use `db.transaction(callback, error, success)` method ,transaction supports one method :`tx.executeSql(sqlStatement, arguments, success, error)`.
here is an example for creating table and adding users to database using transaction:

return to your Home page and modify your function
```js
import React, {useState, useEffect} from 'react';
import { StyleSheet, View, Alert } from 'react-native';
import { Button ,Text,Header, Input} from 'react-native-elements';
import Icon from 'react-native-vector-icons/FontAwesome';
import * as SQLite from 'expo-sqlite';
import Constants from 'expo-constants';

const Home = ()=> {
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

  const addUser = () => {  //this function will add a new row to database
    if(name!=null && email!= null){ //if you reload the app you will be able to see the new row in your terminal
      db.transaction(
        tx => {
          tx.executeSql('insert into users (name, email) values ($1, $2);',//sqlStatement
          [name,email], //arguments
          () => Alert.alert('you added user successfully'), //handle success
          (error) => { //handle error
            if(error) Alert.alert('try again !!')});

        }
      );
    }
  }


  return (
    <View>
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
            label='Enter your Name'
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
            leftIcon={<Icon
            name='at'
            size={24}
            color='#841584'
            />}
            placeholder='E-mail'
            onChangeText={(text)=>setEmail(text)}
        />
        <Button
         title='Add User'
         buttonStyle={{backgroundColor:"#841584"}}
         onPress={ addUser}
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

export default Home

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

After adding some users to our database we can render what we added in any way you feel it's suitable .

```js
const [users, setUsers] = useState(null); 

useEffect(() => {
    db.transaction((tx) => {
      tx.executeSql(
        'create table if not exists users (id integer primary key not null, name text not null, email text not null)'
      );
      if (!users) {
        tx.executeSql(
          'select * from users;',
          [],
          (_, { rows: { _array } }) => setUsers(_array),
          () => console.log('error fetching')
        );
      }
    });
  }, [users]);
  ```
Now in the return of the function you can display the data in List, Cards ...etc
import Card, ListItem from react-native-elements and ScrollView from react-native

```js
 <ScrollView style={styles.container}>
        <View>
          <Input
            label="Enter your name"
            leftIcon={<Icon name="user" size={24} color="#841584" />}
            placeholder="Name"
            onChangeText={(text) => setName(text)}
          />
          <Input
            label="Enter your Email"
            leftIcon={<Icon name="at" size={24} color="#841584" />}
            placeholder="E-mail"
            onChangeText={(text) => setEmail(text)}
          />
          <Button
            title="Add User"
            buttonStyle={{ backgroundColor: '#841584' }}
            onPress={addUser}
          />
        </View>
        <View>
          {users ? (
            <Card containerStyle={{ padding: 0 }} title="Users">
              {users.map((user, i) => {
                return (
                  <ListItem
                    key={i}
                    title={user.name}
                    subtitle={user.email}
                    roundAvatar
                    leftAvatar={{
                      source: {
                        uri:
                          'https://cdn0.iconfinder.com/data/icons/professional-avatar-5/48/manager_male_avatar_men_character_professions-512.png',
                      },
                    }}
                  />
                );
              })}
            </Card>
          ) : null}
        </View>
      </ScrollView>
```
If you have any Problems call 911 , for customers service press #1 , for Credit press #3 ,
if you want to kill me press #47654 .

Move on to the next topic .


### Resources:

- [SQLite](https://docs.expo.io/versions/latest/sdk/sqlite/)
- [React-Native with SQLite](https://medium.com/swlh/react-native-with-sqlite-1ec64702e35e)

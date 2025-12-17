# oddball-code-challenge-repo-1765981042679-bergman-mobile-front-end-engineer

# Coding Challenge

## Problem Description
Hi Josh, this coding challenge is for the Mobile Front End Engineer position. Your task is to create a simple mobile application using React Native that displays a list of users. This challenge is designed to assess your skills at an intermediate level, so please ensure your implementation meets the functional requirements below.

## Requirements
- Create a React Native application that fetches user data from a mock API and displays it in a flat list.
- Each user should display their name and email.
- Implement basic navigation to a user detail screen when a user is clicked.
- Include a button on the detail screen that allows users to "Like" the user, which should increase a "Like" count displayed on the detail screen.
- Write unit tests for the components using Jest and include end-to-end tests with Detox.

## Technical Specifications  
- Use React Native for the mobile application.
- You may use Expo for easier setup.
- Ensure that the application is responsive and works on both iOS and Android.
- Follow best practices for code structure and component design.

## Starter Files

### File 1: App.js
```javascript
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import UserList from './UserList';
import UserDetail from './UserDetail';

const Stack = createStackNavigator();

const App = () => {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="UserList">
        <Stack.Screen name="UserList" component={UserList} />
        <Stack.Screen name="UserDetail" component={UserDetail} />
      </Stack.Navigator>
    </NavigationContainer>
  );
};

export default App;
```

### File 2: UserList.js  
```javascript
import React, { useEffect, useState } from 'react';
import { View, Text, FlatList, TouchableOpacity } from 'react-native';

const UserList = ({ navigation }) => {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/users')
      .then(response => response.json())
      .then(data => setUsers(data));
  }, []);

  const renderItem = ({ item }) => (
    <TouchableOpacity onPress={() => navigation.navigate('UserDetail', { user: item })}>
      <Text>{item.name} - {item.email}</Text>
    </TouchableOpacity>
  );

  return (
    <View>
      <FlatList
        data={users}
        renderItem={renderItem}
        keyExtractor={item => item.id.toString()}
      />
    </View>
  );
};

export default UserList;
```

### File 3: UserDetail.js
```javascript
import React, { useState } from 'react';
import { View, Text, Button } from 'react-native';

const UserDetail = ({ route }) => {
  const { user } = route.params;
  const [likes, setLikes] = useState(0);

  const handleLike = () => {
    setLikes(likes + 1);
  };

  return (
    <View>
      <Text>Name: {user.name}</Text>
      <Text>Email: {user.email}</Text>
      <Text>Likes: {likes}</Text>
      <Button title="Like" onPress={handleLike} />
    </View>
  );
};

export default UserDetail;
```

## Sample Data
You can use the following sample data for testing:

```json
[
  {
    "id": 1,
    "name": "Leanne Graham",
    "email": "Sincere@april.biz"
  },
  {
    "id": 2,
    "name": "Ervin Howell",
    "email": "Shanna@melissa.tv"
  }
]
```

## Evaluation Criteria
- Code quality and cleanliness.
- Correctness of the implementation (functionality).
- Responsiveness of the UI.
- Quality of tests written (unit and end-to-end).
- Overall user experience.

## Submission Instructions
- Please submit your complete project as a ZIP file.
- Ensure that your code is well-commented and follows best practices.
- Include instructions for running your application and tests in a README file.
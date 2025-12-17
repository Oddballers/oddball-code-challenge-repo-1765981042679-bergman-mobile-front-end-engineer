# oddball-code-challenge-repo-1765981042679-name-mobile-front-end-engineer

# Coding Challenge

## Problem Description

Hi <Name>, this coding challenge is for the Mobile Front End Engineer position. Your task is to create a simple mobile application using React Native that interacts with users.

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

## Starter File

### File 1: UserList.js

```javascript
import React, { useEffect, useState } from 'react';
import { View, Text, FlatList, TouchableOpacity } from 'react-native';

const UserList = ({ navigation }) => {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/users')
      .then((response) => response.json())
      .then((data) => setUsers(data));
  }, []);

  const renderItem = ({ item }) => (
    <TouchableOpacity
      onPress={() => navigation.navigate('UserDetail', { user: item })}
    >
      <Text>
        {item.name} - {item.email}
      </Text>
    </TouchableOpacity>
  );

  return (
    <View>
      <FlatList
        data={users}
        renderItem={renderItem}
        keyExtractor={(item) => item.id.toString()}
      />
    </View>
  );
};

export default UserList;
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

- Ensure that your code is well-commented and follows best practices.
- Include instructions for running your application and tests in a README file.

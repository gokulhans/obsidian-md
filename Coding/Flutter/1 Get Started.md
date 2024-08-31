##### Change main.dart page code to this. 

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Hello Flutter'),
        ),
        body: const Center(
          child: Text('Welcome to Flutter!'),
        ),
      ),
    );
  }
}
```

##### Create these folders

```
lib/  
│  
├── models/ # Data models representing the business logic entities  
│ └── user.dart # Example model  
│  
├── views/ # UI screens and widgets  
│ ├── home_screen.dart # Home screen UI  
│ └── login_screen.dart # Login screen UI  
│  
├── controllers/ # Business logic controllers (For MVC/MVP patterns)  
│ └── user_controller.dart  
│  
├── blocs/ # Business logic components (For BLoC pattern)  
│ └── user_bloc.dart  
│  
├── services/ # Services like API or database management  
│ ├── api_service.dart # Service for network calls  
│ └── db_service.dart # Service for database operations  
│  
├── utils/ # Utility functions and constants  
│ ├── constants.dart # Application constants  
│ └── utils.dart # Utility functions  
│  
└── main.dart # Entry point of the app
```
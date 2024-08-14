## IntelliJ IDEA project: Create controller/service/dto

<img width="285" alt="Screenshot 2024-08-09 at 13 19 28" src="https://github.com/user-attachments/assets/b3a4d7c0-fcb5-463a-a160-98ac34df2e10">


DatoriumApiApplication.java
```java
package com.datorium.Datorium.API;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.*;

@SpringBootApplication
@CrossOrigin // CORS policy
public class DatoriumApiApplication  { // Main class

	public static void main(String[] args) { //this is the only thing supposed to be here
		SpringApplication.run(DatoriumApiApplication.class, args);
	}
}
```


### CONTROLLERS:

MessageController.java
```java
package com.datorium.Datorium.API.Controllers;

import com.datorium.Datorium.API.DTOs.Message;
import com.datorium.Datorium.API.Services.MessageService;

import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/message")
public class MessageController {

    private MessageService messageService;
    public MessageController(){
            messageService = new MessageService();
    }
        //CRUD
        //AddMessage
        //UpdateMessage
        //GetMessage
        //DeleteMessage

    @PostMapping("/add") //messageController is requesting data from messageService
    public String add(@RequestBody Message message){
        return messageService.add(message);
    }

}
```

UserController.java
```java
package com.datorium.Datorium.API.Controllers;

import com.datorium.Datorium.API.DTOs.User;
import com.datorium.Datorium.API.Services.UserService;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.PostMapping;

@RestController
@RequestMapping("/user")
public class UserController {

    private UserService userService;
    public UserController(){
        userService = new UserService();
    }
    //CRUD
    //AddUser
    //UpdateUser
    //GetUser
    //DeleteUser

    @PostMapping("/add") //userController is requesting data from userService
    public int add(@RequestBody User user){
        return userService.add(user);
    }
}
```


### DTOs:

Message.java
```java
package com.datorium.Datorium.API.DTOs;

public class Message {
    public String message;
}
```

User.java
```java
package com.datorium.Datorium.API.DTOs;

public class User {
    public String name;
}
```


### SERVICES:

MessageService.java
```java
package com.datorium.Datorium.API.Services;

import com.datorium.Datorium.API.DTOs.Message;

public class MessageService {
    public String add(Message message){
        return "New message added";
    }
}
```

UserService.java
```java
package com.datorium.Datorium.API.Services;

import com.datorium.Datorium.API.DTOs.User;

public class UserService {
    public int add(User user){
        return 0;
    }
}
```

## POSTMAN:

<img width="938" alt="Screenshot 2024-08-09 at 13 26 06" src="https://github.com/user-attachments/assets/bd114764-f358-4247-afd5-5cf8ecbbdcb6">

<img width="931" alt="Screenshot 2024-08-09 at 13 24 45" src="https://github.com/user-attachments/assets/f74453c4-55ea-4897-899d-088310d49214">




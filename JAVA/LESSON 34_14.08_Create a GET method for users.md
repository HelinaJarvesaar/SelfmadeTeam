## IntelliJ IDEA project: Create a GET method for users
1. Create UserController endpoint to get all users
2. Create a UserService method to get all users
3. Create a UserRepository method to get all users
4. Add user with a postman
5. Try to get all the users with GET method
6. Repeat step 4 and 5

<img width="243" alt="Screenshot 2024-08-14 at 21 54 31" src="https://github.com/user-attachments/assets/ddbfdab4-b7f6-435b-8aab-e1aeb6c9ec29">

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

UserController.java
```java
package com.datorium.Datorium.API.Controllers;

import com.datorium.Datorium.API.DTOs.User;
import com.datorium.Datorium.API.Services.UserService;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/user")
public class UserController {

    private UserService userService;
    public UserController(){
        userService = new UserService();
    }

    @PostMapping("/add") //userController is requesting data from userService
    public int add(@RequestBody User user){
        return userService.add(user);
    }

    @GetMapping("/allUsers")
    public List<User> getAllUsers(){
        return userService.getAllUsers();
    }

}
```
UserService.java
```java
package com.datorium.Datorium.API.Services;

import com.datorium.Datorium.API.DTOs.User;
import com.datorium.Datorium.API.REPO.UserRepo;

import java.util.ArrayList;
import java.util.List;

public class UserService {
    private UserRepo userRepo;
    public UserService() {
        userRepo = new UserRepo();
    }

    public int add(User user){
        return userRepo.add(user);
    }

    public List<User> getAllUsers(){
        return userRepo.getAllUsers();
    }
}
```

UserRepo.java
```java
package com.datorium.Datorium.API.REPO;

import com.datorium.Datorium.API.DTOs.User;

import java.util.ArrayList;
import java.util.List;

public class UserRepo {

    private ArrayList<User> users = new ArrayList<>();

    public int add(User user){
        users.add(user);
        return users.size();
    }

    public List<User> getAllUsers(){
        return users;
    }
}
```

User.java
```java
package com.datorium.Datorium.API.DTOs;

public class User {
    public String name;

}
```

Add user with POSTMAN:
<img width="939" alt="Screenshot 2024-08-14 at 22 04 03" src="https://github.com/user-attachments/assets/4c40f1f7-f29f-43bd-a026-1f88301dbd50">


Get all users with POSTMAN:
<img width="935" alt="Screenshot 2024-08-14 at 22 05 52" src="https://github.com/user-attachments/assets/0c0e64e9-fc98-487b-9198-cc671e45ae4c">



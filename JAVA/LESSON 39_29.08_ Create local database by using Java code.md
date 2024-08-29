# TEAMWORK:

1. Use the example of SQL in Java and add an "AddUser" method inside the previous Datorium API project - User (or Cheese) repository.
2. Try and run postman and verify with db browser that the data is there

NOTE: previously we returned int in this method, change it to void. (You will have to make changes inside userController and userService as well

Example code:

```java
import java.sql.DriverManager;
import java.sql.SQLException;
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        var scanner = new Scanner(System.in);
        System.out.println("Please provide your name: ");
        var personsName = scanner.nextLine();

        String url = "jdbc:sqlite:my.db";
        try (var conn = DriverManager.getConnection(url)) {
            if (conn != null) {
               var statement = conn.createStatement();
                statement.execute("INSERT INTO people (name) VALUES ('" + personsName + "')");
            }
        } catch (SQLException e) {
            System.err.println(e.getMessage());
        }
    }
}
```


- COPY the code from today's lesson. Open the project with Controllers/Services/Repositories (we used it 2 weeks ago).

- Open UserRepository

- Inside add(User user) method, paste the code.

Changed UserRepo.java:
```java
package com.datorium.Datorium.API.REPO;

import com.datorium.Datorium.API.DTOs.User;
import java.util.ArrayList;
import java.sql.DriverManager;
import java.sql.SQLException;


public class UserRepo {

    private ArrayList<User> users = new ArrayList<>();
    String url = "jdbc:sqlite:my.db";

    public void add(User user){
        try (var conn = DriverManager.getConnection(url)) {
            if (conn != null) {
                var statement = conn.createStatement();
                statement.execute("CREATE TABLE IF NOT EXISTS people (id INTEGER PRIMARY KEY AUTOINCREMENT, name varchar(20))");
                statement.execute("INSERT INTO people (name) VALUES ('" + user.name + "')");
            }
        } catch (SQLException e) {
            System.err.println(e.getMessage());
        }
    }

    public ArrayList<User> get(){
        return users;
    }
    public User update(int userIndex, User updateUserDTO){
        var user = users.get(userIndex);
        user.name = updateUserDTO.name;
        return user;
    }
}
```

Changed UserController.java
```java
package com.datorium.Datorium.API.Controllers;

import com.datorium.Datorium.API.DTOs.UpdateUserDTO;
import com.datorium.Datorium.API.DTOs.User;
import com.datorium.Datorium.API.Services.UserService;
import org.springframework.web.bind.annotation.*;

import java.util.ArrayList;

@RestController
@RequestMapping("/user")
public class UserController {

    private final UserService userService;
    public UserController(){
        userService = new UserService();
    }

    @PostMapping("/add") //userController is requesting data from userService
    public void add(@RequestBody User user){
        userService.add(user);
    }

    @GetMapping("/get")
    public ArrayList<User> get(){
        return userService.get();
    }

    @PostMapping ("/update")
    public User update (@RequestBody UpdateUserDTO updateUserDTO){
        return userService.update(updateUserDTO.userIndex, updateUserDTO.user);
    }

}
```

Changed UserService.java:
```java
package com.datorium.Datorium.API.Services;

import com.datorium.Datorium.API.DTOs.User;
import com.datorium.Datorium.API.REPO.UserRepo;

import java.util.ArrayList;

public class UserService {
    private final UserRepo userRepo;
    public UserService() {
        userRepo = new UserRepo();
    }

    public void add(User user){
        userRepo.add(user);
    }

    public ArrayList<User> get(){
        return userRepo.get();
    }

    public User update(int userIndex, User updateUserDTO){
        return userRepo.update(userIndex, updateUserDTO);
    }
}

```

There is also need to: Open Modul Settings -> Global Libraries -> "+" From Marven... -> download library: jdbc-sqlite 🔍 -> OK

POSTMAN:


<img width="621" alt="Screenshot 2024-08-29 at 23 55 35" src="https://github.com/user-attachments/assets/d4f7cc08-4fed-490f-94b9-eccd2c095490">


BD Browser:


<img width="629" alt="Screenshot 2024-08-29 at 23 57 33" src="https://github.com/user-attachments/assets/c732d1de-d23c-4afd-be5a-60cd33fafde3">



 





# Test the /user/update endpoint.


User.java
```java
package com.datorium.Datorium.API.DTOs;

public class User {
    public int id;
    public String name;
}
```

UserRepo.java
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
        String url = "jdbc:sqlite:my.db";
        var resultList = new ArrayList <User>();
        try (var conn = DriverManager.getConnection(url)) { //connection to DB
            if (conn != null) {  //sure that connection is done
                var statement = conn.createStatement(); //Create action to DB what to do
                var result = statement.executeQuery("SELECT id,name FROM people");
                // Result is like different box, but more abstract

                while(result.next()){ // goes through abstract box
                    var user = new User(); // if founds element in box, creates new user
                    user.id = result.getInt("id");
                    user.name = result.getString("name"); // sets name to user
                    resultList.add(user); //adds user to the box
                }// while loop stops when there is no new element
            }
        } catch (SQLException e) {
            System.err.println(e.getMessage());
        }
        return resultList;
    }
    public User update(User user){
        try (var conn = DriverManager.getConnection(url)) {
            if (conn != null) {
                var statement = conn.createStatement();
                statement.execute("UPDATE people SET name = '" + user.name + "' WHERE id = " + user.id);
            }
        } catch (SQLException e) {
            System.err.println(e.getMessage());
        }
        return user;
    }
}
```

UserService.java
```java
package com.datorium.Datorium.API.Services;

import com.datorium.Datorium.API.DTOs.User;
import com.datorium.Datorium.API.REPO.UserRepo;
import org.apache.coyote.BadRequestException;

import java.util.ArrayList;

public class UserService {
    private final UserRepo userRepo;

    public UserService() {
        userRepo = new UserRepo();
    }

    public void add(User user) throws BadRequestException {
        if (user.name == null || user.name.isEmpty()) {
            throw new BadRequestException("User name is empty");
        }
        userRepo.add(user);
    }

    public ArrayList<User> get(){
        return userRepo.get();
    }

    public User update(User user){
        userRepo.update(user);
        return user;  // this is a hack, we should remove this
    }
}
```

UserController.java
```java
package com.datorium.Datorium.API.Controllers;

import com.datorium.Datorium.API.DTOs.User;
import com.datorium.Datorium.API.Services.UserService;
import org.apache.coyote.BadRequestException;
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
    public void add(@RequestBody User user) throws BadRequestException{
        userService.add(user);
    }

    @GetMapping("/get")
    public ArrayList<User> get(){
        return userService.get();
    }

    @PostMapping ("/update")
    public User update (@RequestBody User user){
         userService.update(user);
        return user;
    }

}
```

POSTMAN: 
1. add users
2. get users
<img width="676" alt="Screenshot 2024-09-11 at 22 51 53" src="https://github.com/user-attachments/assets/7b380c24-e5e6-4806-94ec-0fc1e8f2d0d7">

3. update user
<img width="672" alt="Screenshot 2024-09-11 at 22 52 54" src="https://github.com/user-attachments/assets/670add4d-6587-46c2-9e3f-7dc5ca05408b">

4. get updated users
<img width="674" alt="Screenshot 2024-09-11 at 22 53 21" src="https://github.com/user-attachments/assets/8c058c58-02ee-4eec-a294-3a7ce901538b">






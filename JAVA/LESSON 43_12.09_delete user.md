# Adding DELETE function to our User code:

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

    public void delete(int id){
        try (var conn = DriverManager.getConnection(url)) {
            if (conn != null) {
                var statement = conn.createStatement();
                statement.execute("DELETE FROM people WHERE id = " + id);
            }
        } catch (SQLException e) {
            System.err.println(e.getMessage());
        }

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
        return user;  // TODO: THIS Is A HACK, we should remove this
    }

    public void delete (int id){
        userRepo.delete(id);
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

@CrossOrigin (origins = "*")
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

    @DeleteMapping("/delete")
    public void delete(@RequestParam (value = "id") int id){ //http:/localhost:8080/user/delete?id=123
        userService.delete(id);
    }

}
```

DatoriumApiApplication.java
```java
package com.datorium.Datorium.API;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.*;


@SpringBootApplication
@CrossOrigin (origins = "*")// CORS policy
public class DatoriumApiApplication  { // Main class

	public static void main(String[] args) { //this is the only thing supposed to be here
		SpringApplication.run(DatoriumApiApplication.class, args);
	}
}
```

## Asking ChatGPT to generate front-end to our code 
### (and change colors to make it more beautiful 😉 )

<img width="491" alt="Screenshot 2024-09-14 at 16 02 45" src="https://github.com/user-attachments/assets/5c646af5-30a2-416a-8ffd-9a7e233d7982">

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>User Management</title>
    <style>
        body {
            font-family: 'Montserrat', sans-serif;
            background-color: #a9a394;
            color: #333;
            margin: 0;
            padding: 0;
        }

        h1 {
            text-align: center;
            font-size: 2.5em;
            color: #333;
            margin-top: 20px;
        }

        h2 {
            color: #333;
            margin-bottom: 10px;
        }

        form {
            background-color: #e0d9cb;
            padding: 20px;
            border-radius: 8px;
            margin-bottom: 20px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }

        label {
            display: block;
            margin-bottom: 8px;
            color: #333;
        }

        input {
            width: 96%;
            padding: 10px;
            margin-bottom: 15px;
            border: 1px solid #d1d8e0;
            border-radius: 5px;
            font-size: 1em;
        }

        button {
            background-color: #a9a394;
            color: #333;
            border: none;
            padding: 10px 15px;
            border-radius: 30px;
            cursor: pointer;
            font-size: 1em;
        }

        button:hover {
            background-color: #6f5a78;
        }

        table {
            width: 100%;
            margin-top: 20px;
            border-collapse: collapse;
        }

        table, th, td {
            border: 1px solid #d1d8e0;
        }

        th, td {
            padding: 12px;
            text-align: left;
        }

        th {
            background-color: #6f5a78;
            color: white;
        }

        td {
            background-color: #e0d9cb;
        }

        .container {
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
        }

        ul {
            list-style: none;
            padding: 0;
        }

        ul li {
            background-color: #e0d9cb;
            padding: 10px;
            border: 1px solid #d1d8e0;
            border-radius: 5px;
            margin-bottom: 10px;
        }

    </style>
</head>
<body>

<div class="container">
    <h1>User Management</h1>

    <!-- Add User Form -->
    <h2>Add User</h2>
    <form id="addUserForm">
        <label for="userName">Name:</label>
        <input type="text" id="userName" name="name" required>
        <button type="button" onclick="addUser()">Add User</button>
    </form>

    <!-- Update User Form -->
    <h2>Update User</h2>
    <form id="updateUserForm">
        <label for="updateUserId">User ID:</label>
        <input type="number" id="updateUserId" name="id" required>
        <label for="updateUserName">Name:</label>
        <input type="text" id="updateUserName" name="name" required>
        <button type="button" onclick="updateUser()">Update User</button>
    </form>

    <!-- Get Users -->
    <h2>Users List</h2>
    <button type="button" onclick="getUsers()">Get Users</button>
    <ul id="userList"></ul>

    <!-- Delete User Form -->
    <h2>Delete User</h2>
    <form id="deleteUserForm">
        <label for="deleteUserId">User ID:</label>
        <input type="number" id="deleteUserId" name="id" required>
        <button type="button" onclick="deleteUser()">Delete User</button>
    </form>

    <!-- Users Table (optional view) -->
    <table>
        <thead>
            <tr>
                <th>ID</th>
                <th>Name</th>
                <th>Action</th>
            </tr>
        </thead>
        <tbody id="userTableBody">
            <!-- User data will be appended here -->
        </tbody>
    </table>
</div>

<script>
    const baseUrl = 'http://localhost:8080/user';

    // Add user functionality
    function addUser() {
        const name = document.getElementById('userName').value;
        fetch(`${baseUrl}/add`, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({ name: name })
        }).then(response => {
            if (response.ok) {
                alert('User added successfully');
                getUsers();  // Refresh users list
            } else {
                alert('Error adding user');
            }
        });
    }

    // Update user functionality
    function updateUser() {
        const id = document.getElementById('updateUserId').value;
        const name = document.getElementById('updateUserName').value;
        fetch(`${baseUrl}/update`, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({ id: id, name: name })
        }).then(response => {
            if (response.ok) {
                alert('User updated successfully');
                getUsers();  // Refresh users list
            } else {
                alert('Error updating user');
            }
        });
    }

    // Fetch users functionality
    function getUsers() {
        fetch(`${baseUrl}/get`)
            .then(response => response.json())
            .then(users => {
                const userList = document.getElementById('userList');
                const tableBody = document.getElementById('userTableBody');
                userList.innerHTML = '';
                tableBody.innerHTML = '';
                
                users.forEach(user => {
                    // For list view
                    const listItem = document.createElement('li');
                    listItem.textContent = `ID: ${user.id}, Name: ${user.name}`;
                    userList.appendChild(listItem);

                    // For table view
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td>${user.id}</td>
                        <td>${user.name}</td>
                        <td><button onclick="deleteUser(${user.id})">Delete</button></td>
                    `;
                    tableBody.appendChild(row);
                });
            });
    }

    // Delete user functionality
    function deleteUser(userId) {
        const id = userId || document.getElementById('deleteUserId').value;
        fetch(`${baseUrl}/delete?id=${id}`, {
            method: 'DELETE'
        }).then(response => {
            if (response.ok) {
                alert('User deleted successfully');
                getUsers();  // Refresh users list
            } else {
                alert('Error deleting user');
            }
        });
    }

    // Initial load of users
    getUsers();
</script>

</body>
</html>
```
Saved this as "index.html", open it and outcome is like this:

<img width="512" alt="Screenshot 2024-09-14 at 16 06 08" src="https://github.com/user-attachments/assets/964d0738-2b3c-4aca-88a2-34419007a97e">





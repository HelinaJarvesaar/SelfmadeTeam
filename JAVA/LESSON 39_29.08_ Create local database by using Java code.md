# HOMEWORK:

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

 





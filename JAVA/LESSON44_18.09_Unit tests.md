# Making new project in IntelliJ IDEA

1. Make a new folder for Your new project in Your computer
   
2. Download new API https://start.spring.io (You can write Your own project name, click "Generate") and put it in Your new Project folder
   
<img width="504" alt="Screenshot 2024-09-22 at 13 26 14" src="https://github.com/user-attachments/assets/e0a59d5f-85a9-44c3-aa11-744120c70d83">

3. In IntelliJ: File ➡︎ Open ➡︎ finding my new project folder and open the new API that I just downloaded.


## New Project "TestExample"
<img width="263" alt="Screenshot 2024-09-22 at 13 31 57" src="https://github.com/user-attachments/assets/de9313a1-41e5-463c-984b-23bc932ab551">

TestExampleApplication.java
```java
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class TextExampleApplication {

	public static void main(String[] args) {

		var userService = new UserService();

		System.out.println(userService.getFullName("Oskars", "Klaumanis"));
		SpringApplication.run(TextExampleApplication.class, args);
	}
}
```

UserService.java
```java
package com.example.demo;

public class UserService {

    public String randomnumber = "1234";
    public String getFullName(String name, String surname){
        return name + surname;
    }

}
```

## 1. DEBUG

1. Put the `RED DOT` ( "Breakpoint" program run stops right there) on some line (e.g 16) in TestExampleApplication.java
   ➡︎ press `Debug` ➡︎ Pres `Step into` ➡︎ press "pink method" (e.g "getFullName)

  <img width="502" alt="Screenshot 2024-09-22 at 14 04 44" src="https://github.com/user-attachments/assets/cc8f96d8-6077-46e7-83c2-324b194d57ef">

  ➡︎ program opens this method in UserService.java and we are able to see what type of data was received from the "name" and "surname" ➡︎
 
  <img width="498" alt="Screenshot 2024-09-22 at 14 08 21" src="https://github.com/user-attachments/assets/221594e5-517a-44ed-a950-e7d250d16cf5">



  
![image](https://github.com/user-attachments/assets/4f65f6cb-fb7f-4e65-a870-20667b8fa74f)



## 2. Testign manually

TestExampleApplicationTests.java
```java
package com.example.demo;

import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.util.Assert;

@SpringBootTest
class TextExampleApplicationTests {
	// Hey I need method that gives me my fullName  - this is businesslogic
	@Test
	void WHEN_NameIsOskarsAndSurnameIsKlaumanis_THEN_result_Oskars_Klaumanis(){
		// Arrange - prepare data and services
		var userService = new UserService();

		//Act - Do some action, usually call a method
		var fullName = userService.getFullName("Oskars", "Klaumanis");

		// Assert - Test weather or not the result is correct
		Assert.isTrue(fullName.equals("Oskars Klaumanis"), "Hey, the name should be with a space between name and surname");
	}
	
}
```






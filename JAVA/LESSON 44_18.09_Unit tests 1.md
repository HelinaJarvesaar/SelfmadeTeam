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

___

## 1. DEBUGGING - testing manually

https://www.jetbrains.com/help/idea/debugging-code.html


Put the `RED DOT`  🔴 ( "Breakpoint" program run stops right there) on some line (e.g 16) in TestExampleApplication.java ➡︎

   ➡︎ press `Debug` ➡︎ press `Step into` ➡︎ press "pink method" (e.g "getFullName)  ➡︎

   <img width="502" alt="Screenshot 2024-09-22 at 14 04 44" src="https://github.com/user-attachments/assets/cc8f96d8-6077-46e7-83c2-324b194d57ef">
   
   ➡︎ program opens this method in UserService.java and we are able to see what type of data was received from the "name" and "surname" ➡︎

   <img width="498" alt="Screenshot 2024-09-22 at 14 08 21" src="https://github.com/user-attachments/assets/221594e5-517a-44ed-a950-e7d250d16cf5">
   
   ➡︎ after checking data, press again `Step into`, program opens DatoriumApiApplication.java ➡︎

   ➡︎ press `Step over`, "System.out.println" is launched and in Console we'll see "OskarsKlaumanis" ➡︎

   <img width="490" alt="Screenshot 2024-09-22 at 14 23 27" src="https://github.com/user-attachments/assets/099a3897-17fe-4136-88ef-edf13b791752">
   
   <img width="490" alt="Screenshot 2024-09-22 at 14 23 27" src="https://github.com/user-attachments/assets/cbe8a1a1-47e4-43d8-a51a-5249ac9bfceb">
   
   ➡︎ press `Step over` again and in Console we'll see "SPRING logo"

   <img width="493" alt="Screenshot 2024-09-22 at 14 35 33" src="https://github.com/user-attachments/assets/70960e95-2d60-4d74-b687-ffbe28344ad2">


___

## 2. UNIT TESTS

Writing code to test my code - a specific code that we want to write to make sure small portion of our program is working correctly, we go through all edge cases

- Naming Unit Tests: https://www.baeldung.com/java-unit-testing-best-practices

	(e.g The name of unit test should explain on what kind of scenario what should happen)
- We should hard code the data in unit tests!
  
### What makes good unit test:

<img width="879" alt="Screenshot 2024-09-22 at 19 13 10" src="https://github.com/user-attachments/assets/fde9bb11-0a28-4fac-8163-48af83a85159">

### TDD - TestDrivenDevelopment (google)

  
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

### Testing Unit Tests:

1. Run test:
   
   in code right click on `test name` (e.g “void WHEN_Name…”) OR on  the `class name` (e.c class DatroiumApiApplication” OR on the left side on the `test file`

   & "Run DatoriumApiApplicationTest" (we check weather `Assert.` statement `isTrue`, and if it is not, the message appears):

   <img width="498" alt="Screenshot 2024-09-22 at 15 03 22" src="https://github.com/user-attachments/assets/5fc44ad0-9e72-45b6-bba0-874904bf9833">

   
3. If test failed: look for the info, click on `WHEN...`

   <img width="489" alt="Screenshot 2024-09-22 at 15 09 38" src="https://github.com/user-attachments/assets/69cdde81-29ca-4adf-bca8-7418c11267d8">

4. Debug test:

   <img width="498" alt="Screenshot 2024-09-22 at 15 12 34" src="https://github.com/user-attachments/assets/5a8c01ba-f761-47d9-8da1-73f9e5638255">

5. Fix the method (e.g. add space " " between names):

UserService.java
```java
package com.example.demo;

public class UserService {

    public String randomnumber = "1234";
    public String getFullName(String name, String surname){
        return name + " "  surname;
    }

}
```
5. Now we do not need to run the whole code, just run unit test like this:

   <img width="490" alt="Screenshot 2024-09-22 at 15 30 54" src="https://github.com/user-attachments/assets/162ede00-ceec-4d07-bffa-69710b8d5e45">
   
   <img width="498" alt="Screenshot 2024-09-22 at 15 33 44" src="https://github.com/user-attachments/assets/b7fcb9a2-2a67-4d5a-aaad-f8ac021c1dac">


# HOMEWORK
Hi, I want to be able to get a sum of 2 numbers, but if the sum is above 100, then I want to receive 0 instead.

1. Create MathService

2. Create a method sum()

3. Create a unit test for this method.

```java
// mathService.java

package com.example.demo;

public class MathService {

    public int getSum(int number1, int number2) {
        if (number1 + number2 > 100) {
            return 0;
        }
        return number1 + number2;
    }
}

// TextExampleApplication.java

package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class TextExampleApplication {

	public static void main(String[] args) {

		var mathService = new MathService();

		System.out.println(mathService.getSum(45, 45));
		SpringApplication.run(TextExampleApplication.class, args);
	}
}

// TextExampleApplicationTests.java

package com.example.demo;

import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.util.Assert;

@SpringBootTest
class TextExampleApplicationTests {
	// Hi, I want to be able to get a sum of 2 numbers,
	// but if the sum is above 100, then I want to receive 0 instead.

	@Test

	void WHEN_getSumIsBelow100_THEN_ResultIsGetSum(){
		var mathService = new MathService();

		var sum = mathService.getSum(45, 45);

		Assert.isTrue(sum == 90 , "Hey want to get sum of 2 numbers if the sum is under 100 and 0 if above 100");
	}

	@Test
	void WHEN_getSumIs100_THEN_ResultIs100(){
		var mathService = new MathService();

		var sum = mathService.getSum(50, 50);

		Assert.isTrue(sum == 100, "Hey want to get sum of 2 numbers if the sum is under 100 and 0 if above 100");
	}

	@Test
	void WHEN_getSumIsAbove100_THEN_ResultIs0(){
		var mathService = new MathService();

		var sum = mathService.getSum(50, 60);

		Assert.isTrue(sum == 0, "Hey if the sum of 2 numbers is above 100 I want to receive 0");
	}
}
```




   






```java
package com.datorium.Datorium.API;



import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import java.util.ArrayList;

@SpringBootApplication
@RestController
@CrossOrigin
public class DatoriumApiApplication {

	public static void main(String[] args) {
		System.out.println("asd");
		SpringApplication.run(DatoriumApiApplication.class, args);
	}


	@GetMapping("/ping")
	public String ping() {
		return "pong";
	}

	@GetMapping("/hello")
	public String hello(@RequestParam(value = "name", defaultValue = "World") String name) {
		return String.format("Hello %s!", name);
	}
	@GetMapping("/sum")
	public int sum(@RequestParam(value = "number1") int number1, @RequestParam(value = "number2") int number2){
		return number1 + number2;
	}

	@GetMapping("/multiply")
	public int multiply(@RequestParam(value = "number1") int number1, @RequestParam(value = "number2") int number2){
		return number1 * number2;
	}

// 1. Create an array in the endpoint, fill the array with data and access it from the URL

	@GetMapping("/array1")
	public int[] array() {
		return new int[]{1, 2, 3, 4};
	}

	@GetMapping("/names")
	public ArrayList<String> names(){
		ArrayList<String> names = new ArrayList<String>();
		names.add("Svetlana");
		names.add("Irina");
		names.add("Elina");
		names.add("Beatrice");
		names.add("Helina");
		return  names;

	}

	@GetMapping("/array")
	public int[][] getArray() {
        	int rows = 3;
		int cols = 3;
		int[][] array = new int[rows][cols];

		// Fill the array with sample data (e.g., incrementing numbers)
        	int value = 1;
        	for (int i = 0; i < rows; i++) {
            		for (int j = 0; j < cols; j++) {
                		array[i][j] = value++;
            		}
        	}
		return array;
	}

// 2. Create an object (new class, cheese or wine or whatever) in the endpoint,
// fill the object, access it from the URL

	@GetMapping("/group")
	public Group group() {
		Group group = new Group("SelfmadeTeam", 5);
		return group;
	}
		public class Group{
			public String name;
			public int members;

			public Group (String name, int members ){
				this.name = name;
				this.members = members;
			}
		}

// 3. Create a new endpoint, that generates a two dimensional int array.
// Endpoint should be in /draw and should return two dimensional array

	@GetMapping("/draw")
	public int[][] draw(){
		return new int[][]{
			new int[]{0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 , 0, 0, 0},
			new int[]{0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 , 0, 0, 0},
			new int[]{0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 0, 0 , 0, 0, 0},
			new int[]{0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 0 , 0, 0, 0},
			new int[]{0, 1, 0, 0, 1, 1, 0, 1, 0, 1, 1, 0 , 0, 1, 0},
			new int[]{0, 1, 1, 1, 1, 1, 0, 1, 0, 1, 1, 1 , 1, 1, 0},
			new int[]{0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 , 1, 0, 0},
			new int[]{0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 1, 0 , 0, 0, 0},
			new int[]{0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 0 , 0, 0, 0},
			new int[]{0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 0, 0 , 0, 0, 0},
			new int[]{0, 0, 0, 1, 1, 1, 1, 1, 1, 0, 0, 0 , 0, 0, 0},
			new int[]{0, 0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0 , 0, 0, 0},
			new int[]{0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0 , 0, 0, 0},
			new int[]{0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 , 0, 0, 0},
			new int[]{0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 , 0, 0, 0}};
	}

	@GetMapping("/draw2")
	public int[][] draw2() {
		return new int[][]{
		            {1, 0, 0, 0, 1},
		            {0, 1, 0, 1, 0},
		            {0, 0, 1, 0, 0},
		            {0, 1, 0, 1, 0},
		            {1, 0, 0, 0, 1}};
    	}

}
```
<img width="250" alt="Screenshot 2024-07-29 at 13 56 58" src="https://github.com/user-attachments/assets/c883c0b3-4771-46a9-b2bf-41f8ef661790">



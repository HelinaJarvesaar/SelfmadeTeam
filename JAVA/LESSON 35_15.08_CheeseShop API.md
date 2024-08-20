## Cheese Shop
1. CheeseShopController
2. CheeseShopService
3. CheeseShopRepository
4. Add / Update / Get

<img width="226" alt="Screenshot 2024-08-20 at 16 49 15" src="https://github.com/user-attachments/assets/49975e44-d568-4371-91ef-af102273a8bc">



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

CheeseShopController.java
```java
package com.datorium.Datorium.API.Controllers;

import com.datorium.Datorium.API.DTOs.Cheese;
import com.datorium.Datorium.API.DTOs.UpdateCheeseDTO;
import com.datorium.Datorium.API.Services.CheeseShopService;
import org.springframework.web.bind.annotation.*;

import java.util.ArrayList;

@RestController
@RequestMapping("/cheese")
public class CheeseShopController {

    private final CheeseShopService cheeseShopService;
    public CheeseShopController(){
        cheeseShopService = new CheeseShopService();
    }

    @PostMapping("/add")
    public int add(@RequestBody Cheese cheese){
        return cheeseShopService.add(cheese);
    }

    @GetMapping("/get")
    public ArrayList<Cheese> get(){
        return cheeseShopService.get();
    }

    @PostMapping ("/update")
    public Cheese update (@RequestBody UpdateCheeseDTO updateCheeseDTO){
        return cheeseShopService.update(updateCheeseDTO.name, updateCheeseDTO.weight, updateCheeseDTO.cheese);
    }
}
```
CheeseShopService.java
```java
package com.datorium.Datorium.API.Services;

import com.datorium.Datorium.API.DTOs.Cheese;
import com.datorium.Datorium.API.REPO.CheeseShopRepo;

import java.util.ArrayList;

public class CheeseShopService {
    private final CheeseShopRepo cheeseShopRepo;
    public CheeseShopService() {
        cheeseShopRepo = new CheeseShopRepo();
    }

    public int add(Cheese cheese){
        return cheeseShopRepo.add(cheese);
    }

    public ArrayList<Cheese> get(){
        return cheeseShopRepo.get();
    }

    public Cheese update(String name, int weight, Cheese updateCheeseDTO){
        return cheeseShopRepo.update(name, weight, updateCheeseDTO);
    }
}
```

CheeseShopRepo.java
```java
package com.datorium.Datorium.API.REPO;

import com.datorium.Datorium.API.DTOs.Cheese;
import java.util.ArrayList;

public class CheeseShopRepo {

    private final ArrayList<Cheese> cheeses = new ArrayList<>(); //mocked db

    public int add(Cheese cheese) {
        cheeses.add(cheese);
        return cheeses.size();
    }

    public ArrayList<Cheese> get() {
        return cheeses;
    }

    public Cheese update(String name, int weight, Cheese updateCheeseDTO) {
        for (Cheese cheese : cheeses) {
            if (cheese.name.equals(updateCheeseDTO.name)) {
                cheese.weight = weight;
                return cheese;
            }
        }
        return null;
    }
}
```

Cheese.java
```java
package com.datorium.Datorium.API.DTOs;

public class Cheese {
    public String name;
    public int weight;
}
```

UpdateCheeseShopDTO.java
```java
package com.datorium.Datorium.API.DTOs;

public class UpdateCheeseDTO {
    public Cheese cheese;
    public String name;
    public int weight;
}
```


ADD cheese with POSTMAN:
<img width="854" alt="Screenshot 2024-08-20 at 17 38 59" src="https://github.com/user-attachments/assets/874e7221-4e1d-497a-8c05-af38badc4723">

GET all cheeses with POSTMAN:
<img width="851" alt="Screenshot 2024-08-20 at 17 40 10" src="https://github.com/user-attachments/assets/869322a9-f7bb-43f0-9623-b6bafab0da65">

UPDATE cheese weight with POSTMAN:
<img width="856" alt="Screenshot 2024-08-20 at 17 36 11" src="https://github.com/user-attachments/assets/fbb4cda6-e0d3-4f4c-b840-22274dc9be96">

AFTER UPDATE GET all cheeses with POSTMAN:
<img width="850" alt="Screenshot 2024-08-20 at 17 42 02" src="https://github.com/user-attachments/assets/c118cd0a-160e-4035-b2d3-b5824146a964">


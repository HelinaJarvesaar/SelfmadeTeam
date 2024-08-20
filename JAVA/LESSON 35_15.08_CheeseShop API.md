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
        return cheeseShopService.update(updateCheeseDTO.cheeseIndex, updateCheeseDTO.cheese);
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
    private CheeseShopRepo cheeseShopRepo;
    public CheeseShopService() {
        cheeseShopRepo = new CheeseShopRepo();
    }

    public int add(Cheese cheese){
        return cheeseShopRepo.add(cheese);
    }

    public ArrayList<Cheese> get(){
        return cheeseShopRepo.get();
    }

    public Cheese update(int cheeseIndex, Cheese updateCheeseDTO){
        return cheeseShopRepo.update(cheeseIndex, updateCheeseDTO);
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

    public int add(Cheese cheese){
        cheeses.add(cheese);
        return cheeses.size();
    }

    public ArrayList<Cheese> get(){
        return cheeses;
    }

    public Cheese update(int cheeseIndex, Cheese updateCheeseDTO){
        var cheese = cheeses.get(cheeseIndex);
        cheese.name = updateCheeseDTO.name;
        return cheese;
    }
}
```

Cheese.java
```java
package com.datorium.Datorium.API.DTOs;

public class Cheese {
    public String name;
}
```

UpdateCheeseShopDTO.java
```java
package com.datorium.Datorium.API.DTOs;

public class UpdateCheeseDTO {
    public Cheese cheese;
    public int cheeseIndex;
}
```


ADD cheese with POSTMAN:
<img width="935" alt="Screenshot 2024-08-20 at 16 52 04" src="https://github.com/user-attachments/assets/96d55eb4-4679-45b1-b87b-ea852c8008b9">

GET all cheeses with POSTMAN:
<img width="932" alt="Screenshot 2024-08-20 at 16 53 05" src="https://github.com/user-attachments/assets/a5bc0a31-90b9-4144-b6c2-0dcb8fd56154">

UPDATE cheese with POSTMAN:
<img width="938" alt="Screenshot 2024-08-20 at 16 55 28" src="https://github.com/user-attachments/assets/983c1da7-7360-436d-b764-a89547d16b42">

AFTER UPDATE GET all cheeses with POSTMAN:
<img width="939" alt="Screenshot 2024-08-20 at 16 56 08" src="https://github.com/user-attachments/assets/7f80290e-cac2-452a-a15f-ae7943b47784">


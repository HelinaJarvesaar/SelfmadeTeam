# Before:

```java
package com.example.demo;

import java.util.ArrayList;
import java.util.Random;

public class CityService {
    public City getRandomCity() throws Exception {
        // 0. Prepare a list of cities
        ArrayList<City> cities = new ArrayList<>();
 
        //1. Count total amount of citizens -> 100
        var totalCitizenCount = 0;
        for (City city: cities){
            totalCitizenCount += city.getPopulation();
        }
        //2. Choose random number -> 56
        Random random = new Random();
        int randomValue = random.nextInt(totalCitizenCount);

        //3. Loop going through all of the cities
        //4. Choose the city with correct lottery ticket
        //population -> 25
        //randomValue -> 56
        //We subtract 56 - 25 = 31
        // BECAUSE ITS NOT BELOW OR EQUAL TO 0, GO TO NEXT
        // 31 - 75 -> because it's below 0, we choose this city
        for(City city: cities){
            randomValue -= city.getPopulation();

            if(randomValue <= 0){
                return city;
            }
        }
        throw new Exception("Something wrong");
    }
}
```


# After splitting the getRandomCity into 3 different methods:
```java
package com.example.demo.CityLottery;

import java.util.ArrayList;
import java.util.Random;

public class CityService {

    private ICityRepository cityRepository;

    public CityService(ICityRepository cityRepository) {
        this.cityRepository = cityRepository;
    }
    public City getRandomCity() throws Exception {

        ArrayList<City> cities = new ArrayList<>();
        int totalCitizenCount = calculateTotalPopulation(cities);
        int randomValue = getRandomValue(totalCitizenCount);

        return selectCity(cities, randomValue);

    }
        public int calculateTotalPopulation(ArrayList<City> cities){
            int totalCitizenCount = 0;
            for (City city: cities){
                totalCitizenCount += city.getPopulation();
            }
            return totalCitizenCount;
        }

        public int getRandomValue(int totalCitizenCount){
            Random random = new Random();
            int randomValue = random.nextInt(totalCitizenCount);
            return randomValue;
        }

        public City selectCity(ArrayList<City> cities,int randomValue) throws Exception{
            for(City city: cities){
                randomValue -= city.getPopulation();
                if(randomValue <= 0){
                    return city;
                }
            }
            throw new Exception("Something wrong");
        }
}
```

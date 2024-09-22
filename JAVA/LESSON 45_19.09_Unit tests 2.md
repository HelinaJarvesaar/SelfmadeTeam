# HOMEWORK

1. Create a game where you have to guess a number.

2. If the number is too big, then we return 3

3. If the number is too small, we return 2

4. If the number is exactly the same, we return 1.


EDIT: If you are advanced enough, just use enums

Game.java
```java
package com.example.demo;

public class Game{

    public int number;

    public void setNumber(int number){
        this.number = number;
    }
    public int takeAGuess (int guess) {
        if (guess == number) {
            return 1;
        }
        if (guess < number) {
            return 2;
        }
        else {
            return 3;
        }
    }
}
```

GameTests.java

```java
package com.example.demo;

import org.junit.jupiter.api.Test;
import org.springframework.util.Assert;


public class GameTests {

    @Test
    void WHEN_GuessEqualsNumber_THEN_Return_1() {
        // Arrange
        var game = new Game();
        game.setNumber(5);

        // Act
        var response = game.takeAGuess(5);

        // Assert
        Assert.isTrue(response == 1, "It's supposed to be 1");
    }
    @Test
    void WHEN_GuessIsTooBig_THEN_Return_3() {
        // Arrange
        var game = new Game();
        game.setNumber(5);

        // Act
        var response = game.takeAGuess(90);

        // Assert
        Assert.isTrue(response == 3, "It's supposed to be 3");
    }

    @Test
    void WHEN_GuessIsTooSmall_THEN_Return_2() {
        // Arrange
        var game = new Game();
        game.setNumber(5);

        // Act
        var response = game.takeAGuess(1);

        // Assert
        Assert.isTrue(response == 2, "It's supposed to be 2");
    }
}
```

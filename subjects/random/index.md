---
layout: default
title: Randomness
meta: 
todo: 
---
{% include licence.md %}

## Randomness

When programming, you may occasionally need to simulate random events. Situations such as the unpredictability of weather, or surprising moves on the AI's part in a computer game can often be simulated with random number generators, running on a computer. In Java, there is a ready-made class `Random`, which you can use in the following way:

```java
import java.util.Random;

public class Randomizing {
    public static void main(String[] args) {
        Random randomizer = new Random(); // creates a random number generator
        int i = 0;

        while (i < 10) {
            // Generates and prints out a new random number on each round of the loop
            System.out.println(randomizer.nextInt(10));
            i++;
        }
    }
}
```

In the code above, you first create an instance of the class `Random` with the keyword `new` -- exactly as when creating objects implementing other classes. An object of type Random has the method `nextInt` that can be given an integer value as parameter. The method returns a random integer within the *range 0..(the integer given as parameter- 1)*.

The printout of this program could be as follows:

```output
2
2
4
3
4
5
6
0
7
8
```

We will need floating point numbers, for example when dealing with probability calculations. In computing, probabilities are usually calculated with numbers within the range [0..1]. An object of the class Random can return random floating point numbers with the method `nextDouble`. Let us consider the following probabilities of weather conditions:

* Sleet with the probability 0.1 (10%)
* Snow with the probability 0.3 (30%)
* Sunny with the probability 0.6 (60%)

Using the estimates above, let us create a weather forecaster.

```java
import java.util.ArrayList;
import java.util.Random;

public class WeatherForecaster {
    private Random random;

    public WeatherForecaster() {
        this.random = new Random();
    }

    public String forecastWeather() {
        double probability = this.random.nextDouble();

        if (probability <= 0.1) {
            return "Sleet";
        } else if (probability <= 0.4) { // 0.1 + 0.3
            return "Snow";
        } else { // the rest, 1.0 - 0.4 = 0.6
            return "Sunny";
        }
    }

    public int forecastTemperature() {
        return (int) ( 4 * this.random.nextGaussian() - 3 );
    }
}
```

The method `forecastTemperature` is interesting in many ways. Within this method, we are calling the method `this.random.nextGaussian()`, just like any other time we have called a method in the previous examples. Interestingly, this method of the class `Random` returns a value from the normal distribution (if you have no interest in the different varieties of random figures, that's okay!).

```java
public int forecastTemperature() {
    return (int) ( 4 * this.random.nextGaussian() - 3 );
}
```

In the expression above, interesting is the section (`int`). This part of the expression changes the bracketed floating point number into an integer value. A corresponding method transforms integer values into floating point numbers: (`double`) integer. This is called an *explicit type conversion*.

Let us create a class with a main method that uses the class `WeatherForecaster`.

```java
public class Program {

    public static void main(String[] args) {
        WeatherForecaster forecaster = new WeatherForecaster();

        // Use a list to help you organise things
        ArrayList<String> days = new ArrayList<String>();
        Collections.addAll(days, "Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun");

        System.out.println("Weather forecast for the next week:");
        for(String day : days) {
            String weatherForecast = forecaster.forecastWeather();
            int temperatureForecast = forecaster.forecastTemperature();

            System.out.println(day + ": " + weatherForecast + " " + temperatureForecast + " degrees.");
        }
    }
}
```

The printout from this program could be as follows:

```output
Weather forecast for the next week:
Mon: Snow 1 degrees.
Tue: Snow 1 degrees.
Wed: Sunny -2 degrees.
Thu: Sunny 0 degrees.
Fri: Snow -3 degrees.
Sat: Snow -3 degrees.
Sun: Sunny -5 degrees.
```

{% include_relative exercises/001.md %}
{% include_relative exercises/002.md %}
{% include_relative exercises/003.md %}
{% include_relative exercises/004.md %}
{: .exercises }
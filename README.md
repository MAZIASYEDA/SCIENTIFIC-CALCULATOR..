# SCIENTIFIC-CALCULATOR..
//MAKE MY FIRST SCIENTIFIC CALCULATOR.

#include <stdio.h>
#include <math.h>

// Unit conversions

// Length: meters to feet
float metersToFeet(float meters) {
    return meters * 3.281;
}

// Length: feet to meters
float feetToMeters(float feet) {
    return feet / 3.281;
}

// Mass: kilograms to pounds
float kilogramsToPounds(float kilograms) {
    return kilograms * 2.205;
}

// Mass: pounds to kilograms
float poundsToKilograms(float pounds) {
    return pounds / 2.205;
}

// Temperature: Celsius to Fahrenheit
float celsiusToFahrenheit(float celsius) {
    return (celsius * 9 / 5) + 32;
}

// Temperature: Fahrenheit to Celsius
float fahrenheitToCelsius(float fahrenheit) {
    return (fahrenheit - 32) * 5 / 9;
}

// Polar to Rectangular coordinates conversion
void polarToRectangular(float r, float theta, float* x, float* y) {
    *x = r * cos(theta);
    *y = r * sin(theta);
}

// Rectangular to Polar coordinates conversion
void rectangularToPolar(float x, float y, float* r, float* theta) {
    *r = sqrt(x * x + y * y);
    *theta = atan2(y, x);
}

int main() {
    // Unit conversions
    float meters = 10.0;
    printf("%.2f meters = %.2f feet\n", meters, metersToFeet(meters));

    float feet = 32.808;
    printf("%.2f feet = %.2f meters\n", feet, feetToMeters(feet));

    float kilograms = 5.0;
    printf("%.2f kilograms = %.2f pounds\n", kilograms, kilogramsToPounds(kilograms));

    float pounds = 11.025;
    printf("%.2f pounds = %.2f kilograms\n", pounds, poundsToKilograms(pounds));

    float celsius = 25.0;
    printf("%.2f Celsius = %.2f Fahrenheit\n", celsius, celsiusToFahrenheit(celsius));

    float fahrenheit = 77.0;
    printf("%.2f Fahrenheit = %.2f Celsius\n", fahrenheit, fahrenheitToCelsius(fahrenheit));

    // Polar to Rectangular coordinates conversion
    float radius = 5.0;
    float angle = 45.0 * M_PI / 180.0; // Convert degrees to radians
    float x, y;
    polarToRectangular(radius, angle, &x, &y);
    printf("\nPolar coordinates (r = %.2f, θ = %.2f radians) in rectangular form: x = %.2f, y = %.2f\n", radius, angle, x, y);

    // Rectangular to Polar coordinates conversion
    float xCoord = 2.0;
    float yCoord = 2.0;
    float r, theta;
    rectangularToPolar(xCoord, yCoord, &r, &theta);
    printf("Rectangular coordinates (x = %.2f, y = %.2f) in polar form: r = %.2f, θ = %.2f radians\n", xCoord, yCoord, r, theta);

    return 0;
}

      










    

    

    
          
            





    

            

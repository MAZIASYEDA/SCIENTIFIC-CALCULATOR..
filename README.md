# SCIENTIFIC-CALCULATOR..
//MAKE MY FIRST SCIENTIFIC CALCULATOR.

#include <stdio.h>
#include <math.h>

// Function to calculate the derivative of a function at a given point using forward difference method
double derivative(double (*f)(double), double x, double h) {
    return (f(x + h) - f(x)) / h;
}

// Function to calculate the indefinite integral of a function within a given range using the trapezoidal rule
double indefiniteIntegral(double (*f)(double), double a, double b, int n) {
    double h = (b - a) / n;
    double sum = 0.5 * (f(a) + f(b));

    for (int i = 1; i < n; ++i) {
        double x = a + i * h;
        sum += f(x);
    }

    return h * sum;
}

// Function to calculate the definite integral of a function within a given range using the trapezoidal rule
double definiteIntegral(double (*f)(double), double a, double b, int n) {
    double h = (b - a) / n;
    double sum = 0.5 * (f(a) + f(b));

    for (int i = 1; i < n; ++i) {
        double x = a + i * h;
        sum += f(x);
    }

    return h * sum;
}

// Example function: f(x) = x^2
double exampleFunction(double x) {
    return x * x;
}

int main() {
    double x = 2.0; // Point at which derivative is calculated
    double h = 0.0001; // Step size for derivative approximation

    printf("Derivative of f(x) = x^2 at x = %.2f is %.2f\n", x, derivative(exampleFunction, x, h));

    double lowerLimit = 0.0; // Lower limit for integration
    double upperLimit = 2.0; // Upper limit for integration
    int divisions = 10000; // Number of divisions for numerical integration

    printf("Indefinite integral of f(x) = x^2 from %.2f to %.2f is %.2f\n", lowerLimit, upperLimit, indefiniteIntegral(exampleFunction, lowerLimit, upperLimit, divisions));

    printf("Definite integral of f(x) = x^2 from %.2f to %.2f is %.2f\n", lowerLimit, upperLimit, definiteIntegral(exampleFunction, lowerLimit, upperLimit, divisions));

    return 0;
}



 
    




      










    

    

    
          
            





    

            

# SCIENTIFIC-CALCULATOR..
//MAKE MY FIRST SCIENTIFIC CALCULATOR.

#include <stdio.h>
#include <stdlib.h>
#include <math.h>

// Function to calculate modulus (remainder)
int calculateModulus(int num, int divisor) {
    return num % divisor;
}

// Function to calculate percentage
double calculatePercentage(double value, double total) {
    return (value / total) * 100.0;
}

// Function to calculate Greatest Common Divisor (GCD) using Euclidean Algorithm
int calculateGCD(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

// Function to calculate Least Common Multiple (LCM)
int calculateLCM(int a, int b) {
    return (a * b) / calculateGCD(a, b);
}

// Function to calculate floor (round down)
int calculateFloor(double num) {
    return (int)floor(num);
}

// Function to calculate ceiling (round up)
int calculateCeiling(double num) {
    return (int)ceil(num);
}

int main() {
    int num, divisor, a, b;
    double value, total;

    printf("Enter two numbers for modulus (remainder): ");
    scanf("%d %d", &num, &divisor);
    printf("Modulus (remainder): %d\n", calculateModulus(num, divisor));

    printf("Enter value and total for percentage calculation: ");
    scanf("%lf %lf", &value, &total);
    printf("Percentage: %.2lf%%\n", calculatePercentage(value, total));

    printf("Enter two numbers for GCD and LCM calculation: ");
    scanf("%d %d", &a, &b);
    printf("GCD: %d\n", calculateGCD(a, b));
    printf("LCM: %d\n", calculateLCM(a, b));

    double numForFloorCeiling;
    printf("Enter a number for floor and ceiling calculation: ");
    scanf("%lf", &numForFloorCeiling);
    printf("Floor: %d\n", calculateFloor(numForFloorCeiling));
    printf("Ceiling: %d\n", calculateCeiling(numForFloorCeiling));

    return 0;
}





    

    
          
            





    

            

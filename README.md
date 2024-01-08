# SCIENTIFIC-CALCULATOR..
//MAKE MY FIRST SCIENTIFIC CALCULATOR.

#include <stdio.h>
#include <math.h>

int main() {
    double num, base, result;

    printf("Enter the number: ");
    scanf("%lf", &num);

    printf("Enter the base: ");
    scanf("%lf", &base);

    if (num <= 0 || base <= 0 || base == 1) {
        printf("Error! Logarithm is undefined for these values.\n");
    } else {
        result = log(num) / log(base); // Using change of base formula
        printf("Logarithm of %.2lf to the base %.2lf is: %.4lf\n", num, base, result);
    }

    return 0;
}







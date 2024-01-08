# SCIENTIFIC-CALCULATOR..
//MAKE MY FIRST SCIENTIFIC CALCULATOR.

#include <stdio.h>
#include <math.h>

// Function to calculate factorial
int factorial(int n) {
    if (n == 0 || n == 1) {
        return 1;
    } else {
        return n * factorial(n - 1);
    }
}

int main() {
    int choice;
    double num1, num2, result;
    
    printf("Select operation:\n");
    printf("1. Exponentiation\n");
    printf("2. Cube\n");
    printf("3. Factorial\n");
    printf("4. Absolute Value\n");
    printf("5. Nth Root\n");
    printf("Enter your choice: ");
    scanf("%d", &choice);

    switch (choice) {
        case 1:
            printf("Enter base and exponent for exponentiation: ");
            scanf("%lf %lf", &num1, &num2);
            result = pow(num1, num2);
            printf("Result: %.2lf\n", result);
            break;
        case 2:
            printf("Enter a number for cube: ");
            scanf("%lf", &num1);
            result = pow(num1, 3);
            printf("Result: %.2lf\n", result);
            break;
        case 3:
            printf("Enter a number for factorial: ");
            scanf("%lf", &num1);
            if (num1 >= 0 && num1 == (int)num1) {
                result = factorial(num1);
                printf("Result: %.0lf\n", result);
            } else {
                printf("Error! Factorial is defined for non-negative integers only.\n");
            }
            break;
        case 4:
            printf("Enter a number for absolute value: ");
            scanf("%lf", &num1);
            result = fabs(num1);
            printf("Result: %.2lf\n", result);
            break;
        case 5:
            printf("Enter base and nth root for nth root calculation: ");
            scanf("%lf %lf", &num1, &num2);
            if (num1 >= 0 || (int)num2 == num2) {
                result = pow(num1, 1.0 / num2);
                printf("Result: %.2lf\n", result);
            } else {
                printf("Error! Nth root is defined for non-negative bases and integer roots.\n");
            }
            break;
        default:
            printf("Error! Invalid choice.\n");
    }

    return 0;
}





    

            

# SCIENTIFIC-CALCULATOR..
//MAKE MY FIRST SCIENTIFIC CALCULATOR.
#include <stdio.h>

int main() {
    float num1, num2, result;
    char operation;

    printf("Enter operator (+, -, *, /): ");
    scanf("%c", &operation);

    printf("Enter two numbers: ");
    scanf("%f %f", &num1, &num2);

    switch(operation) {
        case '+':
            result = num1 + num2;
            printf("Result: %.2f\n", result);
            break;
        case '-':
            result = num1 - num2;
            printf("Result: %.2f\n", result);
            break;
        case '*':
            result = num1 * num2;
            printf("Result: %.2f\n", result);
            break;
        case '/':
            if (num2 == 0) {
                printf("Error! Division by zero is not allowed.\n");
            } else {
                result = num1 / num2;
                printf("Result: %.2f\n", result);
            }
            break;
        default:
            printf("Error! Invalid operator.\n");
    }

    return 0;
}

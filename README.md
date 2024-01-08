# SCIENTIFIC-CALCULATOR..
//MAKE MY FIRST SCIENTIFIC CALCULATOR.

#include <stdio.h>
#include <math.h>

int main() {
    double angle, result;
    char operation;

    printf("Enter operation (s for sine, c for cosine, t for tangent): ");
    scanf("%c", &operation);

    printf("Enter angle in degrees: ");
    scanf("%lf", &angle);

    // Convert degrees to radians for trigonometric functions
    double radianAngle = angle * (M_PI / 180.0);

    switch(operation) {
        case 's':
            result = sin(radianAngle);
            printf("Sine of %.2lf degrees is: %.4lf\n", angle, result);
            break;
        case 'c':
            result = cos(radianAngle);
            printf("Cosine of %.2lf degrees is: %.4lf\n", angle, result);
            break;
        case 't':
            if (angle == 90 || angle == 270) {
                printf("Tangent is undefined for angles 90 and 270 degrees.\n");
            } else {
                result = tan(radianAngle);
                printf("Tangent of %.2lf degrees is: %.4lf\n", angle, result);
            }
            break;
        default:
            printf("Error! Invalid operation.\n");
    }

    return 0;
}



    

    
          
            





    

            

# SCIENTIFIC-CALCULATOR..
//MAKE MY FIRST SCIENTIFIC CALCULATOR.

#include <stdio.h>

// Structure to represent a complex number
struct Complex {
    float real;
    float imaginary;
};

// Function to add two complex numbers
struct Complex addComplex(struct Complex a, struct Complex b) {
    struct Complex result;
    result.real = a.real + b.real;
    result.imaginary = a.imaginary + b.imaginary;
    return result;
}

// Function to subtract two complex numbers
struct Complex subtractComplex(struct Complex a, struct Complex b) {
    struct Complex result;
    result.real = a.real - b.real;
    result.imaginary = a.imaginary - b.imaginary;
    return result;
}

// Function to multiply two complex numbers
struct Complex multiplyComplex(struct Complex a, struct Complex b) {
    struct Complex result;
    result.real = a.real * b.real - a.imaginary * b.imaginary;
    result.imaginary = a.real * b.imaginary + a.imaginary * b.real;
    return result;
}

// Function to divide two complex numbers
struct Complex divideComplex(struct Complex a, struct Complex b) {
    struct Complex result;
    float divisor = b.real * b.real + b.imaginary * b.imaginary;
    result.real = (a.real * b.real + a.imaginary * b.imaginary) / divisor;
    result.imaginary = (a.imaginary * b.real - a.real * b.imaginary) / divisor;
    return result;
}

// Function to find the conjugate of a complex number
struct Complex conjugateComplex(struct Complex num) {
    struct Complex conjugate;
    conjugate.real = num.real;
    conjugate.imaginary = -num.imaginary;
    return conjugate;
}

int main() {
    struct Complex num1, num2;

    printf("Enter real and imaginary parts of first complex number: ");
    scanf("%f %f", &num1.real, &num1.imaginary);

    printf("Enter real and imaginary parts of second complex number: ");
    scanf("%f %f", &num2.real, &num2.imaginary);

    struct Complex sum = addComplex(num1, num2);
    printf("Sum: %.2f + %.2fi\n", sum.real, sum.imaginary);

    struct Complex difference = subtractComplex(num1, num2);
    printf("Difference: %.2f + %.2fi\n", difference.real, difference.imaginary);

    struct Complex product = multiplyComplex(num1, num2);
    printf("Product: %.2f + %.2fi\n", product.real, product.imaginary);

    if (num2.real == 0 && num2.imaginary == 0) {
        printf("Error! Division by zero is not allowed.\n");
    } else {
        struct Complex quotient = divideComplex(num1, num2);
        printf("Quotient: %.2f + %.2fi\n", quotient.real, quotient.imaginary);
    }

    struct Complex conjugate = conjugateComplex(num1);
    printf("Conjugate of first complex number: %.2f + %.2fi\n", conjugate.real, conjugate.imaginary);

    return 0;
}


 


    

    

    
          
            





    

            

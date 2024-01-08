# SCIENTIFIC-CALCULATOR..
//MAKE MY FIRST SCIENTIFIC CALCULATOR.

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Function to convert decimal to binary
char* decimalToBinary(int n) {
    char* binary = (char*)malloc(33 * sizeof(char)); // 32 bits for integer
    if (!binary) {
        printf("Memory allocation failed!\n");
        exit(1);
    }
    binary[32] = '\0';
    for (int i = 31; i >= 0; --i) {
        binary[i] = (n & 1) ? '1' : '0';
        n >>= 1;
    }
    return binary;
}

// Function to convert binary to decimal
int binaryToDecimal(const char* binary) {
    int decimal = 0;
    for (int i = 0; i < 32; ++i) {
        decimal <<= 1;
        if (binary[i] == '1') {
            decimal |= 1;
        }
    }
    return decimal;
}

// Function to perform binary addition
char* binaryAddition(const char* binary1, const char* binary2) {
    char* result = (char*)malloc(33 * sizeof(char));
    if (!result) {
        printf("Memory allocation failed!\n");
        exit(1);
    }
    result[32] = '\0';
    int carry = 0;
    for (int i = 31; i >= 0; --i) {
        int bit1 = binary1[i] - '0';
        int bit2 = binary2[i] - '0';
        int sum = bit1 + bit2 + carry;
        result[i] = (sum % 2) + '0';
        carry = sum / 2;
    }
    return result;
}

// Function to perform binary subtraction
char* binarySubtraction(const char* binary1, const char* binary2) {
    char* result = (char*)malloc(33 * sizeof(char));
    if (!result) {
        printf("Memory allocation failed!\n");
        exit(1);
    }
    result[32] = '\0';
    int borrow = 0;
    for (int i = 31; i >= 0; --i) {
        int bit1 = binary1[i] - '0';
        int bit2 = binary2[i] - '0';
        int diff = bit1 - bit2 - borrow;
        if (diff < 0) {
            diff += 2;
            borrow = 1;
        } else {
            borrow = 0;
        }
        result[i] = diff + '0';
    }
    return result;
}

// Function to perform binary multiplication
char* binaryMultiplication(const char* binary1, const char* binary2) {
    int result[64] = {0};
    char* multiplied = (char*)malloc(65 * sizeof(char));
    if (!multiplied) {
        printf("Memory allocation failed!\n");
        exit(1);
    }
    multiplied[64] = '\0';
    for (int i = 31; i >= 0; --i) {
        for (int j = 31; j >= 0; --j) {
            int bit1 = binary1[i] - '0';
            int bit2 = binary2[j] - '0';
            result[63 - (31 - i) - (31 - j)] += bit1 * bit2;
        }
    }
    int carry = 0;
    for (int i = 63; i >= 0; --i) {
        int sum = result[i] + carry;
        multiplied[i] = (sum % 2) + '0';
        carry = sum / 2;
    }
    return multiplied;
}

// Function to perform binary division
char* binaryDivision(const char* binary1, const char* binary2) {
    char* quotient = (char*)malloc(33 * sizeof(char));
    if (!quotient) {
        printf("Memory allocation failed!\n");
        exit(1);
    }
    quotient[32] = '\0';
    char* dividend = strdup(binary1);
    char* divisor = strdup(binary2);
    int dividendSign = 0;
    int divisorSign = 0;
    if (dividend[0] == '1') {
        dividendSign = 1;
        for (int i = 0; i < 32; ++i) {
            dividend[i] = (dividend[i] == '0') ? '1' : '0';
        }
        char* one = "00000000000000000000000000000001";
        char* addOne = binaryAddition(dividend, one);
        free(dividend);
        dividend = addOne;
    }
    if (divisor[0] == '1') {
        divisorSign = 1;
        for (int i = 0; i < 32; ++i) {
            divisor[i] = (divisor[i] == '0') ? '1' : '0';
        }
        char* one = "00000000000000000000000000000001";
        char* addOne = binaryAddition(divisor, one);
        free(divisor);
        divisor = addOne;
    }
    char* remainder = (char*)malloc(33 * sizeof(char));
    if (!remainder) {
        printf("Memory allocation failed!\n");
        exit(1);
    }
    remainder[32] = '\0';
    for (int i = 0; i < 32; ++i) {
        remainder[i] = dividend[i];
    }
    for (int i = 0; i < 32; ++i) {
        if (remainder[0] == '1') {
            char* sub = binarySubtraction(remainder, divisor);
            free(remainder);
            remainder = sub;
            char* add = binaryAddition(quotient, "00000000000000000000000000000001");
            free(quotient);
            quotient = add;
        } else {
            char* shift = (char*)malloc(33 * sizeof(char));
            if (!shift) {
                printf("Memory allocation failed!\n");
                exit(1);
            }
            shift[32] = '\0';
            for (int j = 1; j < 32; ++j) {
                shift[j - 1] = remainder[j];
            }
            shift[31] = '0';
            free(remainder);
            remainder = shift;
            char* shiftQ = (char*)malloc(33 * sizeof(char));
            if (!shiftQ) {
                printf("Memory allocation failed!\n");
                exit(1);
            }
            shiftQ[32] = '\0';
            for (int j = 1; j < 32; ++j) {
                shiftQ[j - 1] = quotient[j];
            }
            shiftQ[31] = '0';
            free(quotient);
            quotient = shiftQ;
        }
    }
    if ((dividendSign && !divisorSign) || (!dividendSign && divisorSign)) {
        char* one = "00000000000000000000000000000001";
        char* addOne = binaryAddition(quotient, one);
        free(quotient);
        quotient = addOne;
    }
    free(dividend);
    free(divisor);
    free(remainder);
    return quotient;
}

// Function to perform binary AND operation
char* binaryAND(const char* binary1, const char* binary2) {
    char* result = (char*)malloc(33 * sizeof(char));
    if (!result) {
        printf("Memory allocation failed!\n");
        exit(1);
    }
    result[32] = '\0';
    for (int i = 0; i < 32; ++i) {
        result[i] = (binary1[i] == '1' && binary2[i] == '1') ? '1' : '0';
    }
    return result;
}

// Function to perform binary OR operation
char* binaryOR(const char* binary1, const char* binary2) {
    char* result = (char*)malloc(33 * sizeof(char));
    if (!result) {
        printf("Memory allocation failed!\n");
        exit(1);
    }
    result[32] = '\0';
    for (int i = 0; i < 32; ++i) {
        result[i] = (binary1[i] == '1' || binary2[i] == '1') ? '1' : '0';
    }
    return result;
}

// Function to perform binary XOR operation
char* binaryXOR(const char* binary1, const char* binary2) {
    char* result = (char*)malloc(33 * sizeof(char));
    if (!result) {
        printf("Memory allocation failed!\n");
        exit(1);
    }
    result[32] = '\0';
    for (int i = 0; i < 32; ++i) {
        result[i] = (binary1[i] != binary2[i]) ? '1' : '0';
    }
    return result;
}

int main() {
    int num1, num2;

    printf("Enter first integer: ");
    scanf("%d", &num1);

    printf("Enter second integer: ");
    scanf("%d", &num2);

    char* binary1 = decimalToBinary(num1);
    char* binary2 = decimalToBinary(num2);

    printf("\nBinary representation of %d: %s\n", num1, binary1);
    printf("Binary representation of %d: %s\n", num2, binary2);

    char* addition = binaryAddition(binary1, binary2);
    printf("\nBinary addition: %s\n", addition);

    char* subtraction = binarySubtraction(binary1, binary2);
    printf("Binary subtraction: %s\n", subtraction);

    char* multiplication = binaryMultiplication(binary1, binary2);
    printf("Binary multiplication: %s\n", multiplication);

    if (num2 == 0) {
        printf("Error! Division by zero is not allowed.\n");
    } else {
        char* division = binaryDivision(binary1, binary2);
        printf("Binary division: %s\n", division);
    }

    char* binaryANDResult = binaryAND(binary1, binary2);
    printf("Binary AND: %s\n", binaryANDResult);

    char* binaryORResult = binaryOR(binary1, binary2);
    printf("Binary OR: %s\n", binaryORResult);

    char* binaryXORResult = binaryXOR(binary1, binary2);
    printf("Binary XOR: %s\n", binaryXORResult);

    free(binary1);
    free(binary2);
    free(addition);
    free(subtraction);
    free(multiplication);
    // Free memory for division if allocated
    // Free memory for binaryANDResult, binaryORResult, binaryXORResult

    return 0;
}










    

    

    
          
            





    

            

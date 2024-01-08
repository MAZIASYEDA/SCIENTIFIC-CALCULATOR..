# SCIENTIFIC-CALCULATOR..
//MAKE MY FIRST SCIENTIFIC CALCULATOR.

#include <stdio.h>

#define MAX_SIZE 10

// Function to print a matrix
void printMatrix(float matrix[MAX_SIZE][MAX_SIZE], int rows, int cols) {
    for (int i = 0; i < rows; ++i) {
        for (int j = 0; j < cols; ++j) {
            printf("%.2f\t", matrix[i][j]);
        }
        printf("\n");
    }
}

// Function to add two matrices
void addMatrices(float A[MAX_SIZE][MAX_SIZE], float B[MAX_SIZE][MAX_SIZE], float result[MAX_SIZE][MAX_SIZE], int rows, int cols) {
    for (int i = 0; i < rows; ++i) {
        for (int j = 0; j < cols; ++j) {
            result[i][j] = A[i][j] + B[i][j];
        }
    }
}

// Function to subtract two matrices
void subtractMatrices(float A[MAX_SIZE][MAX_SIZE], float B[MAX_SIZE][MAX_SIZE], float result[MAX_SIZE][MAX_SIZE], int rows, int cols) {
    for (int i = 0; i < rows; ++i) {
        for (int j = 0; j < cols; ++j) {
            result[i][j] = A[i][j] - B[i][j];
        }
    }
}

// Function to multiply two matrices
void multiplyMatrices(float A[MAX_SIZE][MAX_SIZE], float B[MAX_SIZE][MAX_SIZE], float result[MAX_SIZE][MAX_SIZE], int rowsA, int colsA, int colsB) {
    for (int i = 0; i < rowsA; ++i) {
        for (int j = 0; j < colsB; ++j) {
            result[i][j] = 0;
            for (int k = 0; k < colsA; ++k) {
                result[i][j] += A[i][k] * B[k][j];
            }
        }
    }
}

// Function to transpose a matrix
void transposeMatrix(float matrix[MAX_SIZE][MAX_SIZE], float result[MAX_SIZE][MAX_SIZE], int rows, int cols) {
    for (int i = 0; i < rows; ++i) {
        for (int j = 0; j < cols; ++j) {
            result[j][i] = matrix[i][j];
        }
    }
}

// Function to find the determinant of a 2x2 matrix
float determinant2x2(float matrix[2][2]) {
    return matrix[0][0] * matrix[1][1] - matrix[0][1] * matrix[1][0];
}

// Function to find the determinant of a matrix
float determinant(float matrix[MAX_SIZE][MAX_SIZE], int n) {
    if (n == 1) {
        return matrix[0][0];
    } else if (n == 2) {
        return determinant2x2((float (*)[2])matrix);
    } else {
        float det = 0;
        float temp[MAX_SIZE][MAX_SIZE];
        int sign = 1;
        for (int i = 0; i < n; ++i) {
            int subi = 0;
            for (int j = 1; j < n; ++j) {
                int subj = 0;
                for (int k = 0; k < n; ++k) {
                    if (k == i) {
                        continue;
                    }
                    temp[subi][subj] = matrix[j][k];
                    subj++;
                }
                subi++;
            }
            det += sign * matrix[0][i] * determinant(temp, n - 1);
            sign = -sign;
        }
        return det;
    }
}

// Function to find the cofactor of a matrix
void cofactor(float matrix[MAX_SIZE][MAX_SIZE], float temp[MAX_SIZE][MAX_SIZE], int p, int q, int n) {
    int i = 0, j = 0;
    for (int row = 0; row < n; ++row) {
        for (int col = 0; col < n; ++col) {
            if (row != p && col != q) {
                temp[i][j++] = matrix[row][col];
                if (j == n - 1) {
                    j = 0;
                    i++;
                }
            }
        }
    }
}

// Function to find the adjoint of a matrix
void adjoint(float matrix[MAX_SIZE][MAX_SIZE], float adj[MAX_SIZE][MAX_SIZE], int n) {
    if (n == 1) {
        adj[0][0] = 1;
        return;
    }
    int sign = 1;
    float temp[MAX_SIZE][MAX_SIZE];
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < n; ++j) {
            cofactor(matrix, temp, i, j, n);
            sign = ((i + j) % 2 == 0) ? 1 : -1;
            adj[j][i] = sign * determinant(temp, n - 1);
        }
    }
}

// Function to find the inverse of a matrix
int inverse(float matrix[MAX_SIZE][MAX_SIZE], float inv[MAX_SIZE][MAX_SIZE], int n) {
    float det = determinant(matrix, n);
    if (det == 0) {
        return 0;
    }
    float adj[MAX_SIZE][MAX_SIZE];
    adjoint(matrix, adj, n);
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < n; ++j) {
            inv[i][j] = adj[i][j] / det;
        }
    }
    return 1;
}

int main() {
    int rowsA, colsA, rowsB, colsB;

    printf("Enter the number of rows and columns for matrix A: ");
    scanf("%d %d", &rowsA, &colsA);

    printf("Enter the number of rows and columns for matrix B: ");
    scanf("%d %d", &rowsB, &colsB);

    if (rowsA > MAX_SIZE || colsA > MAX_SIZE || rowsB > MAX_SIZE || colsB > MAX_SIZE) {
        printf("Exceeded maximum matrix size.\n");
        return 1;
    }

    if (rowsA != rowsB || colsA != colsB) {
        printf("Matrix addition, subtraction, and multiplication require matrices of the same size.\n");
        return 1;
    }

    float matrixA[MAX_SIZE][MAX_SIZE], matrixB[MAX_SIZE][MAX_SIZE], result[MAX_SIZE][MAX_SIZE];

    printf("Enter elements of matrix A:\n");
    for (int i = 0; i < rowsA; ++i) {
        for (int j = 0; j < colsA; ++j) {
            scanf("%f", &matrixA[i][j]);
        }
    }

    printf("Enter elements of matrix B:\n");
    for (int i = 0; i < rowsB; ++i) {
        for (int j = 0; j < colsB; ++j) {
            scanf("%f", &matrixB[i][j]);
        }
    }

    printf("Matrix A:\n");
    printMatrix(matrixA, rowsA, colsA);

    printf("\nMatrix B:\n");
    printMatrix(matrixB, rowsB, colsB);

    printf("\nAddition of matrices A and B:\n");
    addMatrices(matrixA, matrixB, result, rowsA, colsA);
    printMatrix(result, rowsA, colsA);

    printf("\nSubtraction of matrices A and B:\n");
    subtractMatrices(matrixA, matrixB, result, rowsA, colsA);
    printMatrix(result, rowsA, colsA);

    if (colsA == rowsB) {
        printf("\nMultiplication of matrices A and B:\n");
        multiplyMatrices(matrixA, matrixB, result, rowsA, colsA, colsB);
        printMatrix(result, rowsA, colsB);
    } else {
        printf("\nMatrix multiplication is not possible due to incompatible dimensions.\n");
    }

    printf("\nTranspose of matrix A:\n");
    float transpose[MAX_SIZE][MAX_SIZE];
    transposeMatrix(matrixA, transpose, rowsA, colsA);
    printMatrix(transpose, colsA, rowsA);

    if (rowsA == colsA) {
        printf("\nDeterminant of matrix A: %.2f\n", determinant(matrixA, rowsA));
    } else {
        printf("\nDeterminant can be calculated only for square matrices.\n");
    }

    if (rowsA == colsA) {
        float inverseMatrix[MAX_SIZE][MAX_SIZE];
        if (inverse(matrixA, inverseMatrix, rowsA)) {
            printf("\nInverse of matrix A:\n");
            printMatrix(inverseMatrix, rowsA, colsA);
        } else {
            printf("\nMatrix A is singular. Inverse does not exist.\n");
        }
    } else {
        printf("\nInverse can be calculated only for square matrices.\n");
    }

    return 0;
}








    

    

    
          
            





    

            

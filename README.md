# SCIENTIFIC-CALCULATOR..
//MAKE MY FIRST SCIENTIFIC CALCULATOR.

#include <stdio.h>
#include <stdlib.h>
#include <math.h>

// Function to calculate mean
double calculateMean(int arr[], int n) {
    int sum = 0;
    for (int i = 0; i < n; ++i) {
        sum += arr[i];
    }
    return (double)sum / n;
}

// Function to compare elements for sorting
int compare(const void *a, const void *b) {
    return (*(int *)a - *(int *)b);
}

// Function to calculate median
double calculateMedian(int arr[], int n) {
    qsort(arr, n, sizeof(int), compare);
    if (n % 2 == 0) {
        return (double)(arr[n / 2 - 1] + arr[n / 2]) / 2.0;
    } else {
        return arr[n / 2];
    }
}

// Function to calculate variance
double calculateVariance(int arr[], int n, double mean) {
    double variance = 0;
    for (int i = 0; i < n; ++i) {
        variance += pow(arr[i] - mean, 2);
    }
    return variance / n;
}

// Function to calculate standard deviation
double calculateStandardDeviation(double variance) {
    return sqrt(variance);
}

int main() {
    int n;

    printf("Enter the number of elements: ");
    scanf("%d", &n);

    int arr[n];

    printf("Enter %d elements:\n", n);
    for (int i = 0; i < n; ++i) {
        scanf("%d", &arr[i]);
    }

    double mean = calculateMean(arr, n);
    printf("Mean: %.2lf\n", mean);

    double median = calculateMedian(arr, n);
    printf("Median: %.2lf\n", median);

    double variance = calculateVariance(arr, n, mean);
    printf("Variance: %.2lf\n", variance);

    double stdDeviation = calculateStandardDeviation(variance);
    printf("Standard Deviation: %.2lf\n", stdDeviation);

    return 0;
}


            

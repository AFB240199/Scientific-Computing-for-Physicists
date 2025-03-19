# **Task 02: Computational "Hello World"** 
---

## **Vector Sum with Julia**
```Julia
# Define scalar and dimensions
a = 3.0
N_values = [10, 10^6, 10^8]

# Iterate through each dimension
for N in N_values
    println("Checking N = $N")

    # Create vectors x and y
    x = fill(0.1, N)  # Vector of 0.1 with dimension N
    y = fill(7.1, N)  # Vector of 7.1 with dimension N

    # Calculate vector d
    d = (a * x) .+ y

    # Verify all elements in d are approximately equal to 7.4
    tolerance = 1e-15  # Adjust the tolerance as needed
    is_correct = all(abs.(d .- 7.4) .< tolerance)
    println("All elements approximately equal to 7.4: $is_correct")

end
```

## **Vector Sum with C**
```C
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <stdbool.h>

void compute_and_test(size_t N) {
    double a = 3.0;
    double x_value = 0.1;
    double y_value = 7.1;
    double *d = (double *)malloc(N * sizeof(double));

    if (d == NULL) {
        printf("Memory allocation failed for N = %zu\n", N);
        return;
    }

    // Compute the vector d
    for (size_t i = 0; i < N; i++) {
        d[i] = a * x_value + y_value;
    }

    // Verify all elements of d are approximately 7.4
    double epsilon = 1e-15;  // Tolerance for floating-point comparison
    bool is_correct = true;
    for (size_t i = 0; i < N; i++) {
        if (fabs(d[i] - 7.4) > epsilon) {
            is_correct = false;
            break;
        }
    }

    printf("Vector size: %zu, All elements approximately equal to 7.4: %s\n", N, is_correct ? "true" : "false");

    free(d); // Free allocated memory
}

int main() {
    size_t N_values[] = {10, 1000000, 100000000};

    for (int i = 0; i < 3; i++) {
        compute_and_test(N_values[i]);
    }

    return 0;
}
```

## **Matrix Multiplication with Julia**
```Julia

```

## **Matrix Multiplication with C**
```C
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <time.h>

void matrix_multiply(double *A, double *B, double *C, int N) {
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            C[i * N + j] = 0.0;  // Initialize element to 0
            for (int k = 0; k < N; k++) {
                C[i * N + j] += (A[i * N + k] * B[k * N + j]);
            }
        }
    }
}

int main() {
    int N = 100;  // Adjust for testing (10, 100, or 10000)
    double value_A = 3.0, value_B = 7.1;
    double *A = (double *)malloc(N * N * sizeof(double));
    double *B = (double *)malloc(N * N * sizeof(double));
    double *C = (double *)malloc(N * N * sizeof(double));

    if (!A || !B || !C) {
        printf("Memory allocation failed!\n");
        return 1;
    }

    // Initialize matrices A and B
    for (int i = 0; i < N * N; i++) {
        A[i] = value_A;
        B[i] = value_B;
    }

    clock_t start = clock();
    matrix_multiply(A, B, C, N);
    clock_t end = clock();

    printf("Time elapsed: %.2f seconds\n", (double)(end - start) / CLOCKS_PER_SEC);

    // Validate result with tolerance
    double expected = value_A * value_B;
    double tolerance = 1e-9;  // Allowable margin of error for floating-point calculations
    int valid = 1;

    for (int i = 0; i < N * N; i++) {
        if (fabs(C[i] - expected) > tolerance) {
            // Print mismatch and expected values
            printf("Mismatch at index %d: C[%d] = %lf, expected = %lf\n", i, i, C[i], expected);
            valid = 0;
            break;
        }
    }

    printf("Validation: %s\n", valid ? "Success" : "Failure");

    // Free allocated memory
    free(A);
    free(B);
    free(C);

    return 0;
}
```

## **Answers to the Questions**
1. I noticed that for N=10^8 Julia is a bit slow in giving back the expected answer.
2. At the start, I had a problem running the original code that I created for the vector sum (part 1) for any N an for both languages: indeed, the programm would give back a failure in the verification that the sums and products were consistent with the expected result, due to the limited precision of the computer in doing the computattions. For this reason, I had to introduce a tolerance above which the verification was successfull. It possible to notice that this tolerance has to be greater than e^(-16), which is the precision of the double data type in C. After this implementation the first programm was fine, but I still had problem with the second, which was focused on computing a matrix multiplication (part 3). This problem arises since the product of the two given matrices A and B is not C=AB=21.3 in any dimension N, but it is rescaled by a factor of N, so that we have AB= 21.3*N. For this reason, the programm correctly states that the elements of C are not equal to 21.3. If one perfom the correct rescaling by dividing the result for N, the programm will consistently verify that all the rescaled multiplications give 21.3.

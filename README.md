### LU Decomposition

LU decomposition of a matrix is the factorization of a given square matrix into two triangular matrices, one upper triangular matrix and one lower triangular matrix, such that the product of these two matrices gives the original matrix. It was introduced by Alan Turing in 1948, who also created the Turing machine.

LU Decomposition is a fundamental technique in linear algebra used to solve systems of linear equations, invert matrices, and compute determinants. It decomposes a given matrix into two triangular matrices, one lower (L) and one upper (U). This decomposition simplifies many matrix operations, making it an essential tool in various engineering applications.

### Doolittle Algorithm
The Doolittle Algorithm is a method for performing LU Decomposition, where a given matrix is decomposed into a lower triangular matrix L and an upper triangular matrix U. This decomposition is widely used in solving systems of linear equations, inverting matrices, and computing determinants.


### Gauss Elimination Method
Gaussian Elimination, also known as Gauss-Jordan Elimination, is a method used in linear algebra to solve systems of linear equations and to find the inverse of a matrix. It’s named after the mathematician Carl Friedrich Gauss and also the mathematician Wilhelm Jordan, who made significant contributions to its development.

According to the Gauss elimination method:

1. Any zero row should be at the bottom of the matrix.
2. The first non-zero entry of each row should be on the right-hand side of the first non-zero entry of the preceding row. This method reduces the matrix to row echelon form.


### LU Decomposition Method
LU Decomposition expresses a given square matrix A as the product of two matrices:

L: A lower triangular matrix with ones on the diagonal.
U: An upper triangular matrix. Mathematically, A can be written as

    A = LU  

To factor any square matrix into two triangular matrices i.e., one is a lower triangular matrix and the other is an upper triangular matrix, we can use the following steps.

1. Given a set of linear equations, first convert them into matrix form A X = C where A is the coefficient matrix, X is the variable matrix and C is the matrix of numbers on the right-hand side of the equations.
2. Now, reduce the coefficient matrix A, i.e., the matrix obtained from the coefficients of variables in all the given equations such that for ‘n’ variables we have an nXn matrix, to row echelon form using Gauss Elimination Method. The matrix so obtained is U.
3. To find L, we have two methods. The first one is to assume the remaining elements as some artificial variables, make equations using A = L U, and solve them to find those artificial variables. The other method is that the remaining elements are the multiplier coefficients because of which the respective positions became zero in the U matrix. (This method is a little tricky to understand by words but would get clear in the example below)
4. Now, we have A (the nXn coefficient matrix), L (the nXn lower triangular matrix), U (the nXn upper triangular matrix), X (the nX1 matrix of variables), and C (the nX1 matrix of numbers on the right-hand side of the equations).
5. The given system of equations is A X = C. We substitute A = L U. Thus, we have L U X = C. We put Z = U X, where Z is a matrix or artificial variables and solve for L Z = C first and then solve for U X = Z to find X or the values of the variables, which was required.
![Image](https://github.com/user-attachments/assets/fd1eb717-bc88-454d-96da-eee5a788f839)

## Implementation
#Method-1: Doolittle Algorithm

     MAX = 100

     def luDecomposition(mat, n):

     lower = [[0 for x in range(n)]
             for y in range(n)]
     upper = [[0 for x in range(n)]
             for y in range(n)]

    # Decomposing matrix into Upper
    # and Lower triangular matrix
     for i in range(n):

        # Upper Triangular
         for k in range(i, n):

            # Summation of L(i, j) * U(j, k)
            sum = 0
            for j in range(i):
                sum += (lower[i][j] * upper[j][k])

            # Evaluating U(i, k)
            upper[i][k] = mat[i][k] - sum

        # Lower Triangular
         for k in range(i, n):
            if (i == k):
                lower[i][i] = 1  # Diagonal as 1
            else:

                # Summation of L(k, j) * U(j, i)
                sum = 0
                for j in range(i):
                    sum += (lower[k][j] * upper[j][i])

                # Evaluating L(k, i)
                lower[k][i] = int((mat[k][i] - sum) /
                                  upper[i][i])

    # setw is for displaying nicely
    print("Lower Triangular\t\tUpper Triangular")

    # Displaying the result :
    for i in range(n):

        # Lower
        for j in range(n):
            print(lower[i][j], end="\t")
        print("", end="\t")

        # Upper
        for j in range(n):
            print(upper[i][j], end="\t")
        print("")


    # Driver code
    mat = [[2, -1, -2],
       [-4, 6, 3],
       [-4, -2, 8]]

    luDecomposition(mat, 3)

![Image](https://github.com/user-attachments/assets/34f7e257-6823-45b2-a96c-81dff4f4dad1)


  
#Method-2

    import numpy as np
    from scipy.linalg import lu

    # Example dataset as a matrix
    A = np.array([[2, 1, 1],
              [4, -6, 0],
              [-2, 7, 2]])

    # Perform LU decomposition
    P, L, U = lu(A)

    # Output the results
    print("Original Matrix (A):")
    print(A)

    print("\nPermutation Matrix (P):")
    print(P)

    print("\nLower Triangular Matrix (L):")
    print(L)

    print("\nUpper Triangular Matrix (U):")
    print(U)

    # Verify the decomposition
    # A = P @ L @ U
    reconstructed_A = P @ L @ U
    print("\nReconstructed Matrix (should be equal to A):")
    print(reconstructed_A)
![Image](https://github.com/user-attachments/assets/f0335531-ca12-403c-ac90-2b046ab3d995)





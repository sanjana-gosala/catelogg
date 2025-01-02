# catelogg
import java.util.*;
import java.io.*;

public class PolynomialSolver {

    // Method to decode a value in a given base
    public static int decodeValue(int base, String value) {
        return Integer.parseInt(value, base);  // Convert value to base 10 integer
    }

    // Method to calculate the Lagrange Interpolation Polynomial Coefficients
    public static double[] lagrangeInterpolation(int[] x, int[] y) {
        int n = x.length;
        double[] coefficients = new double[n];

        for (int i = 0; i < n; i++) {
            double coeff = y[i];

            for (int j = 0; j < n; j++) {
                if (i != j) {
                    coeff /= (x[i] - x[j]);
                }
            }
            coefficients[i] = coeff;
        }

        // Now, compute the polynomial coefficients
        double[] polynomialCoefficients = new double[n];

        for (int i = 0; i < n; i++) {
            double[] terms = new double[n];

            // Calculate the polynomial terms for each coefficient
            for (int j = 0; j < n; j++) {
                if (i != j) {
                    for (int k = 0; k < n; k++) {
                        if (k != i && k != j) {
                            terms[k] += coefficients[i] * Math.pow(x[j], k);
                        }
                    }
                }
            }

            // Add terms to the polynomial coefficients
            for (int j = 0; j < n; j++) {
                polynomialCoefficients[j] += terms[j];
            }
        }

        return polynomialCoefficients;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Taking dynamic input for n and k
        System.out.print("Enter the number of roots (n): ");
        int n = sc.nextInt();
        
        System.out.print("Enter the minimum number of roots (k): ");
        int k = sc.nextInt();

        // Arrays to store the decoded x (keys) and y (values)
        int[] x = new int[k];
        int[] y = new int[k];

        // Taking dynamic input for the roots
        System.out.println("Enter the roots (key, base, value):");
        for (int i = 0; i < k; i++) {
            System.out.print("Enter key for root " + (i+1) + ": ");
            x[i] = sc.nextInt();

            System.out.print("Enter base for root " + (i+1) + ": ");
            int base = sc.nextInt();

            System.out.print("Enter value for root " + (i+1) + ": ");
            String value = sc.next();

            // Decode the value based on the base
            y[i] = decodeValue(base, value);
        }

        // Calculate the polynomial coefficients using Lagrange interpolation
        double[] coefficients = lagrangeInterpolation(x, y);

        // Print the coefficients of the polynomial
        System.out.println("Polynomial Coefficients:");
        for (double coeff : coefficients) {
            System.out.println(coeff);
        }

        sc.close();
    }
}




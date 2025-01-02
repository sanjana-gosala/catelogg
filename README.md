# catelogg
import java.util.*;
import java.io.*;

public class PolynomialSolver {

 
    public static int decodeValue(int base, String value) {
        return Integer.parseInt(value, base);  
    }

   
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

      
        double[] polynomialCoefficients = new double[n];

        for (int i = 0; i < n; i++) {
            double[] terms = new double[n];

            
            for (int j = 0; j < n; j++) {
                if (i != j) {
                    for (int k = 0; k < n; k++) {
                        if (k != i && k != j) {
                            terms[k] += coefficients[i] * Math.pow(x[j], k);
                        }
                    }
                }
            }

           
            for (int j = 0; j < n; j++) {
                polynomialCoefficients[j] += terms[j];
            }
        }

        return polynomialCoefficients;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

       
        System.out.print("Enter the number of roots (n): ");
        int n = sc.nextInt();
        
        System.out.print("Enter the minimum number of roots (k): ");
        int k = sc.nextInt();

       
        int[] x = new int[k];
        int[] y = new int[k];

       
        System.out.println("Enter the roots (key, base, value):");
        for (int i = 0; i < k; i++) {
            System.out.print("Enter key for root " + (i+1) + ": ");
            x[i] = sc.nextInt();

            System.out.print("Enter base for root " + (i+1) + ": ");
            int base = sc.nextInt();

            System.out.print("Enter value for root " + (i+1) + ": ");
            String value = sc.next();

           
            y[i] = decodeValue(base, value);
        }

       
        double[] coefficients = lagrangeInterpolation(x, y);

        
        System.out.println("Polynomial Coefficients:");
        for (double coeff : coefficients) {
            System.out.println(coeff);
        }

        sc.close();
    }
}




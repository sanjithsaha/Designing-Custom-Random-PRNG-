import java.util.Scanner;

public class CustomPRNG {

    private long seed;
    private long modulus;
    private long multiplier;

    // Constructor to initialize PRNG parameters
    public CustomPRNG(long seed, long modulus, long multiplier) {
        this.seed = seed;
        this.modulus = modulus;
        this.multiplier = multiplier;
    }

    // Custom f(|x|, |n|) function
    private long customFunction(long x, long n) {
        long result = x * (n / x - 1);
        if (result <= n) return result;
        else return x;
    }

    // Generate next random number (0 <= r < 1)
    public double nextDouble() {
        seed = (multiplier * seed + 1) % modulus;
        seed = customFunction(seed, modulus);
        return (double) seed / modulus;
    }

    // Generate an array of random numbers
    public double[] generateRandomArray(int size) {
        double[] arr = new double[size];
        for (int i = 0; i < size; i++) {
            arr[i] = nextDouble();
        }
        return arr;
    }

    // Test/Usage of the PRNG
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        System.out.print("Enter seed: ");
        long seed = input.nextLong();
        System.out.print("Enter modulus: ");
        long modulus = input.nextLong();
        System.out.print("Enter multiplier: ");
        long multiplier = input.nextLong();
        System.out.print("Enter number of random values: ");
        int n = input.nextInt();

        CustomPRNG prng = new CustomPRNG(seed, modulus, multiplier);
        double[] randomNumbers = prng.generateRandomArray(n);

        System.out.println("\nGenerated Random Numbers:");
        for (double d : randomNumbers) {
            System.out.println(d);
        }
        input.close();
    }
}

import java.math.BigInteger;
import java.util.ArrayList;
import java.util.List;

class Mainn {

    public static void main(String[] args) {
        // Test case setup
        int totalShares = 4;  // Total number of shares
        int threshold = 3;    // Threshold for reconstruction

        // Define shares with bases and values
        List<Share> shares = new ArrayList<>();
        shares.add(new Share(BigInteger.valueOf(1), convertToBase10("4", 10)));   // Base 10: 4
        shares.add(new Share(BigInteger.valueOf(2), convertToBase10("111", 2)));  // Base 2: 7
        shares.add(new Share(BigInteger.valueOf(3), convertToBase10("12", 10)));  // Base 10: 12
        shares.add(new Share(BigInteger.valueOf(6), convertToBase10("213", 4)));  // Base 4: 39

        System.out.println("Generated Shares:");
        for (Share share : shares) {
            System.out.println(share);
        }

        // Suppose we use the first k shares to reconstruct the secret
        List<Share> selectedShares = shares.subList(0, threshold);
        BigInteger reconstructedSecret = reconstructSecret(selectedShares, threshold);
        System.out.println("Reconstructed Secret: " + reconstructedSecret);
    }

    public static BigInteger convertToBase10(String value, int base) {
        return new BigInteger(value, base);
    }

    public static BigInteger reconstructSecret(List<Share> shares, int threshold) {
        BigInteger secret = BigInteger.ZERO;
        int shareCount = shares.size();
        for (int i = 0; i < threshold; i++) {
            Share shareI = shares.get(i);
            BigInteger xi = shareI.x;
            BigInteger yi = shareI.y;
            BigInteger product = yi;

            for (int j = 0; j < threshold; j++) {
                if (i != j) {
                    Share shareJ = shares.get(j);
                    BigInteger xj = shareJ.x;
                    product = product.multiply(BigInteger.ZERO.subtract(xj))
                            .divide(xi.subtract(xj));
                }
            }
            secret = secret.add(product);
        }
        return secret;
    }

    static class Share {
        BigInteger x;
        BigInteger y;

        Share(BigInteger x, BigInteger y) {
            this.x = x;
            this.y = y;
        }

        @Override
        public String toString() {
            return "Share{" + "x=" + x + ", y=" + y + '}';
        }
    }
}

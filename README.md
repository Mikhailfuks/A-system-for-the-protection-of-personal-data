import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;
import java.util.Arrays;
import java.util.Base64;

public class PersonalDataProtectionSystem {

    // Example sensitive data
    private String name = "John Doe";
    private String email = "john.doe@example.com";
    private String phoneNumber = "123-456-7890";

    // Encryption key (should be stored securely)
    private String encryptionKey = "your_secure_key";

    public static void main(String[] args) {
        PersonalDataProtectionSystem system = new PersonalDataProtectionSystem();

        // Encrypt sensitive data
        system.encryptData();

        // Decrypt sensitive data
        system.decryptData();
    }

    // Encrypt sensitive data using AES encryption
    public void encryptData() {
        try {
            // Create a MessageDigest object for SHA-256 hashing
            MessageDigest digest = MessageDigest.getInstance("SHA-256");

            // Hash the encryption key
            byte[] keyHash = digest.digest(encryptionKey.getBytes());

            // Create an AES cipher object
            javax.crypto.Cipher cipher = javax.crypto.Cipher.getInstance("AES");

            // Initialize the cipher for encryption
            cipher.init(javax.crypto.Cipher.ENCRYPT_MODE, new javax.crypto.spec.SecretKeySpec(keyHash, "AES"));

            // Encrypt the sensitive data (replace with actual data)
            byte[] encryptedName = cipher.doFinal(name.getBytes());
            byte[] encryptedEmail = cipher.doFinal(email.getBytes());
            byte[] encryptedPhoneNumber = cipher.doFinal(phoneNumber.getBytes());

            // Encode the encrypted data in Base64 for storage or transmission
            String encodedName = Base64.getEncoder().encodeToString(encryptedName);
            String encodedEmail = Base64.getEncoder().encodeToString(encryptedEmail);
            String encodedPhoneNumber = Base64.getEncoder().encodeToString(encryptedPhoneNumber);

            System.out.println("Encrypted Name: " + encodedName);
            System.out.println("Encrypted Email: " + encodedEmail);
            System.out.println("Encrypted Phone Number: " + encodedPhoneNumber);

        } catch (NoSuchAlgorithmException | javax.crypto.NoSuchPaddingException | javax.crypto.IllegalBlockSizeException | javax.crypto.BadPaddingException e) {
            e.printStackTrace();
        }
    }

    // Decrypt sensitive data using AES decryption
    public void decryptData() {
        try {
            // Create a MessageDigest object for SHA-256 hashing
            MessageDigest digest = MessageDigest.getInstance("SHA-256");

            // Hash the encryption key
            byte[] keyHash = digest.digest(encryptionKey.getBytes());

            // Create an AES cipher object
            javax.crypto.Cipher cipher = javax.crypto.Cipher.getInstance("AES");

            // Initialize the cipher for decryption
            cipher.init(javax.crypto.Cipher.DECRYPT_MODE, new javax.crypto.spec.SecretKeySpec(keyHash, "AES"));

            // Decrypt the sensitive data (replace with actual data)
            byte[] decryptedName = cipher.doFinal(Base64.getDecoder().decode(encodedName));
            byte[] decryptedEmail = cipher.doFinal(Base64.getDecoder().decode(encodedEmail));
            byte[] decryptedPhoneNumber = cipher.doFinal(Base64.getDecoder().decode(encodedPhoneNumber));

            // Convert the decrypted data to strings
            String name = new String(decryptedName);
            String email = new String(decryptedEmail);
            String phoneNumber = new String(decryptedPhoneNumber);

            System.out.println("Decrypted Name: " + name);
            System.out.println("Decrypted Email: " + email);
            System.out.println("Decrypted Phone Number: " + phoneNumber);

        } catch (NoSuchAlgorithmException | javax.crypto.NoSuchPaddingException | javax.crypto.IllegalBlockSizeException | javax.crypto.BadPaddingException e) {
            e.printStackTrace();
        }
    }
}

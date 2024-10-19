# Exp-13-Implement-Message-Authentication-Code
# AIM:
To generate and verify a Message Authentication Code (MAC) for ensuring the integrity and authenticity of a message using a simple XOR operation.

# DESIGN STEPS:
Step 1:
Input a secret key and a message from the user.

Step 2:
Generate the MAC by applying a simple XOR operation between the secret key and the message.

Step 3:
The MAC is computed by repeating the key or message as necessary.

Step 4:
The user can input a received MAC, and the program verifies whether the received MAC matches the computed MAC.

Step 5:
The authenticity of the message is confirmed if the MACs match.

# PROGRAM:

#include <stdio.h>
#include <string.h>

#define MAC_SIZE 32 // Define MAC size in bytes

// Function to compute a simple MAC using XOR
void computeMAC(const char *key, const char *message, char *mac) {
    int key_len = strlen(key);
    int msg_len = strlen(message);
    
    // XOR the key and message, repeating if necessary
    for (int i = 0; i < MAC_SIZE; i++) {
        mac[i] = key[i % key_len] ^ message[i % msg_len]; // Simple XOR operation
    }
    mac[MAC_SIZE] = '\0'; // Null-terminate the MAC string
}

int main() {
    char key[100], message[100];
    char mac[MAC_SIZE + 1]; // Buffer for MAC (+1 for null terminator)
    char receivedMAC[MAC_SIZE + 1]; // Buffer for input of received MAC

    // Step 1: Input secret key
    printf("Enter the secret key: ");
    scanf("%s", key);

    // Step 2: Input the message
    printf("Enter the message: ");
    scanf("%s", message);

    // Step 3: Compute the MAC
    computeMAC(key, message, mac);

    // Step 4: Display the computed MAC in hexadecimal
    printf("Computed MAC (in hex): ");
    for (int i = 0; i < MAC_SIZE; i++) {
        printf("%02x", (unsigned char)mac[i]); // Print each byte as hex
    }
    printf("\n");

    // Step 5: Input the received MAC (for verification)
    printf("Enter the received MAC (as hex): ");
    for (int i = 0; i < MAC_SIZE; i++) {
        scanf("%02hhx", &receivedMAC[i]);
    }

    // Compare the computed MAC with the received MAC
    if (memcmp(mac, receivedMAC, MAC_SIZE) == 0) {
        printf("MAC verification successful. Message is authentic.\n");
    } else {
        printf("MAC verification failed. Message is not authentic.\n");
    }

    return 0;
}

# OUTPUT:
![image](https://github.com/user-attachments/assets/df7d71aa-fc63-4f8a-a3c6-682bab8d4001)




# RESULT:
The program for generating and verifying a Message Authentication Code (MAC) was executed successfully, demonstrating the integrity and authenticity of the message through a simple XOR-based MAC.

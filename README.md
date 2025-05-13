# CSA5125-CRYPTOGRAPHY-192311299#include <stdio.h>
#include <ctype.h>
#include <string.h>

void encrypt(char *text, int k) {
    for (int i = 0; text[i] != '\0'; ++i) {
        if (isalpha(text[i])) {
            char base = isupper(text[i]) ? 'A' : 'a';
            text[i] = (text[i] - base + k) % 26 + base;
        }
    }
}

void decrypt(char *text, int k) {
    for (int i = 0; text[i] != '\0'; ++i) {
        if (isalpha(text[i])) {
            char base = isupper(text[i]) ? 'A' : 'a';
            text[i] = (text[i] - base - k + 26) % 26 + base;
        }
    }
}

int main() {
    char text[100];
    int key;
    int choice;

    printf("Enter a message: ");
    fgets(text, sizeof(text), stdin);
    text[strcspn(text, "\n")] = '\0';  

    printf("Enter the key (1-25): ");
    scanf("%d", &key);

    if (key < 1 || key > 25) {
        printf("Invalid key. Must be between 1 and 25.\n");
        return 1;
    }

    printf("Choose an option:\n1. Encrypt\n2. Decrypt\nEnter your choice: ");
    scanf("%d", &choice);

    if (choice == 1) {
        encrypt(text, key);
        printf("Encrypted message: %s\n", text);
    } else if (choice == 2) {
        decrypt(text, key);
        printf("Decrypted message: %s\n", text);
    } else {
        printf("Invalid choice.\n");
    }

    return 0;
}

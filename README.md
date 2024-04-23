#include <stdio.h>
#include <ctype.h>

char shiftChar(char c, int key, int isEncrypt) {
  int offset = isEncrypt ? key : -key;
  int newAscii = c + offset;

  // Handle uppercase letters (ASCII 65-90)
  if (isalpha(c) && isupper(c)) {
    newAscii = (newAscii - 'A') % 26 + 'A';
  }

  // Handle lowercase letters (ASCII 97-122)
  else if (isalpha(c) && islower(c)) {
    newAscii = (newAscii - 'a') % 26 + 'a';
  }

  // Keep non-alphabetic characters unchanged
  return (char)newAscii;
}

void caesarCipher(char* message, int key, int isEncrypt) {
  for (int i = 0; message[i] != '\0'; i++) {
    message[i] = shiftChar(message[i], key, isEncrypt);
  }
}

int main() {
  char message[100];
  int key, choice;

  printf("Enter a message: ");
  fgets(message, sizeof(message), stdin);

  printf("1. Encrypt\n2. Decrypt\n");
  printf("Enter your choice: ");
  scanf("%d", &choice);

  printf("Enter the key (shift value): ");
  scanf("%d", &key);

  if (choice == 1) {
    caesarCipher(message, key, 1);
    printf("Encrypted message: %s\n", message);
  } else if (choice == 2) {
    caesarCipher(message, key, 0);
    printf("Decrypted message: %s\n", message);
  } else {
    printf("Invalid choice\n");
  }

  return 0;
}

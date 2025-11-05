#include <stdio.h>
#include <stdlib.h>

void encryptFile(char *src, char *dest, int key) {
    FILE *in = fopen(src, "rb");
    FILE *out = fopen(dest, "wb");
    if (!in || !out) {
        printf("Error opening file.\n");
        return;
    }

    char ch;
    while ((ch = fgetc(in)) != EOF)
        fputc(ch ^ key, out);

    fclose(in);
    fclose(out);
    printf("File encrypted successfully.\n");
}

void decryptFile(char *src, char *dest, int key) {
    encryptFile(src, dest, key);  // XOR reverses itself
    printf("File decrypted successfully.\n");
}

int main() {
    int choice, key;
    char input[100], output[100];

    while (1) {
        printf("\n1. Encrypt\n2. Decrypt\n3. Exit\nChoose: ");
        scanf("%d", &choice);

        if (choice == 3) break;
        printf("Enter input file: ");
        scanf("%s", input);
        printf("Enter output file: ");
        scanf("%s", output);
        printf("Enter key (1–255): ");
        scanf("%d", &key);

        if (choice == 1) encryptFile(input, output, key);
        else if (choice == 2) decryptFile(input, output, key);
        else printf("Invalid.\n");
    }
    return 0;
}

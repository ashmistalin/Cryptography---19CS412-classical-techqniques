# Cryptography---19CS412-classical-techqniques
## Register Number : 212221040021

# Caeser Cipher
Caeser Cipher using with different key values

# AIM:

To develop a simple C program to implement Caeser Cipher.

## DESIGN STEPS:

### Step 1:

Design of Caeser Cipher algorithnm 

### Step 2:

Implementation using C code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```
#include <stdio.h>
#include <ctype.h>
#include <string.h>

char ALPHABET[] = "abcdefghijklmnopqrstuvwxyz";

void encrypt(char* text, int shift) {
    for (int i = 0; text[i] != '\0'; i++) {
        if (isalpha(text[i])) {
            int index = tolower(text[i]) - 'a';
            text[i] = ALPHABET[(index + shift) % 26];
        }
    }
}

void decrypt(char* text, int shift) {
    encrypt(text, -shift);
}

int main() {
    char choice[10];
    char text[100];
    int shift;
    printf("Do you want to encrypt or decrypt? ");
    scanf("%s", choice);
    printf("Enter the text: ");
    scanf("%s", text);
    printf("Enter the shift: ");
    scanf("%d", &shift);

    if (strcmp(choice, "encrypt") == 0) {
        encrypt(text, shift);
        printf("Encrypted text: %s\n", text);
    } else if (strcmp(choice, "decrypt") == 0) {
        decrypt(text, shift);
        printf("Decrypted text: %s\n", text);
    } else {
        printf("Invalid choice.\n");
    }

    return 0;
}
```
## OUTPUT:
## Encryption:
![Screenshot (473)](https://github.com/ashmistalin/Ceaser_cipher/assets/103128410/1625b02f-588c-46e7-9073-8451412bf4fe)

## Decryption:
![Screenshot (474)](https://github.com/ashmistalin/Ceaser_cipher/assets/103128410/dc0d29b1-b4ef-4c69-9ad8-ae0210e72526)

## RESULT:
The program is executed successfully

---------------------------------

# PlayFair Cipher
Playfair Cipher using with different key values

# AIM:

To develop a simple C program to implement PlayFair Cipher.

## DESIGN STEPS:

### Step 1:

Design of PlayFair Cipher algorithnm 

### Step 2:

Implementation using C code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>
#define MX 5

void playfair(char ch1, char ch2, char key[MX][MX]) {
    int i, j, w, x, y, z;
    FILE *out;

    if ((out = fopen("cipher.txt", "a+")) == NULL) {
        printf("File Corrupted.");
        return;
    }

    for (i = 0; i < MX; i++) {
        for (j = 0; j < MX; j++) {
            if (ch1 == key[i][j]) {
                w = i;
                x = j;
            } else if (ch2 == key[i][j]) {
                y = i;
                z = j;
            }
        }
    }

    if (w == y) {
        x = (x + 1) % 5;
        z = (z + 1) % 5;
        printf("%c%c", key[w][x], key[y][z]);
        fprintf(out, "%c%c", key[w][x], key[y][z]);
    } else if (x == z) {
        w = (w + 1) % 5;
        y = (y + 1) % 5;
        printf("%c%c", key[w][x], key[y][z]);
        fprintf(out, "%c%c", key[w][x], key[y][z]);
    } else {
        printf("%c%c", key[w][z], key[y][x]);
        fprintf(out, "%c%c", key[w][z], key[y][x]);
    }

    fclose(out);
}

int main() {
    int i, j, k = 0, l, m = 0, n;
    char key[MX][MX], keyminus[25], keystr[10], str[25] = {0};
    char alpa[26] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    printf("\nEnter key: ");
    gets(keystr);
    printf("\nEnter the plain text: ");
    gets(str);
    n = strlen(keystr);

    for (i = 0; i < n; i++) {
        if (keystr[i] == 'j' || keystr[i] == 'J') {
            keystr[i] = 'I';
        }
        keystr[i] = toupper(keystr[i]);
    }

    for (i = 0; i < strlen(str); i++) {
        if (str[i] == 'j' || str[i] == 'J') {
            str[i] = 'I';
        }
        str[i] = toupper(str[i]);
    }

    j = 0;

    for (i = 0; i < 26; i++) {
        for (k = 0; k < n; k++) {
            if (keystr[k] == alpa[i]) {
                break;
            } else if (alpa[i] == 'J') {
                break;
            }
        }
        if (k == n) {
            keyminus[j] = alpa[i];
            j++;
        }
    }

    k = 0;

    for (i = 0; i < MX; i++) {
        for (j = 0; j < MX; j++) {
            if (k < n) {
                key[i][j] = keystr[k];
                k++;
            } else {
                key[i][j] = keyminus[m];
                m++;
            }
            printf("%c ", key[i][j]);
        }
        printf("\n");
    }

    printf("\n\nEntered text: %s\nCipher Text: ", str);

    for (i = 0; i < strlen(str); i++) {
        if (str[i + 1] == '\0') {
            playfair(str[i], 'X', key);
        } else {
            if (str[i] == str[i + 1]) {
                playfair(str[i], 'X', key);
                i++;
            } else {
                playfair(str[i], str[i + 1], key);
                i++;
            }
        }
    }
    return 0;
}
```
## OUTPUT:
![Screenshot (490)](https://github.com/ashmistalin/Vigenere_Cipher/assets/103128410/4e3378aa-e2ab-4356-b710-c63973101cd4)

## RESULT:
The program is executed successfully


---------------------------

# Hill Cipher
Hill Cipher using with different key values

# AIM:

To develop a simple C program to implement Hill Cipher.

## DESIGN STEPS:

### Step 1:

Design of Hill Cipher algorithnm 

### Step 2:

Implementation using C code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```
#include<stdio.h>
#include<conio.h>
#include<string.h>
int main()
{
    unsigned int a[3][3]={{6,24,1},{13,16,10},{20,17,15}};
    unsigned int b[3][3]={{8,5,10},{21,8,21},{21,12,8}};
    int i,j, t=0;
    unsigned int c[20],d[20];
    char msg[20];
    printf("Enter plain text  : ");
    scanf("%s",msg);
    for(i=0;i<strlen(msg);i++)
    { 
        c[i]=msg[i]-65;
        printf("%d ",c[i]);
    }
    for(i=0;i<3;i++)
    { 
        t=0;
        for(j=0;j<3;j++)
        {
            t=t+(a[i][j]*c[j]);
        }
        d[i]=t%26;
    }
    printf("\nEncrypted Cipher Text :");
    for(i=0;i<3;i++)
        printf(" %c",d[i]+65);
    for(i=0;i<3;i++)
    {
        t=0;
        for(j=0;j<3;j++)
        {
            t=t+(b[i][j]*d[j]);
        }
        c[i]=t%26;
    }
    printf("\nDecrypted Cipher Text :");
    for(i=0;i<3;i++)
        printf(" %c",c[i]+65);
    return 0;
}



```
## OUTPUT:
![Screenshot (489)](https://github.com/ashmistalin/Vigenere_Cipher/assets/103128410/609d2278-16ed-4e5e-953b-faaa5ae0aa95)

## RESULT:
The program is executed successfully

-------------------------------------------------

# Vigenere Cipher
Vigenere Cipher using with different key values

# AIM:

To develop a simple C program to implement Vigenere Cipher.

## DESIGN STEPS:

### Step 1:

Design of Vigenere Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

void vigenereEncrypt(char *plaintext, char *key, char *ciphertext) {
    int i, j, keyLen, textLen;
    char encryptedChar;

    keyLen = strlen(key);
    textLen = strlen(plaintext);

    for (i = 0, j = 0; i < textLen; ++i, ++j) {
        if (j == keyLen)
            j = 0;

        if (isalpha(plaintext[i])) {
            encryptedChar = ((toupper(plaintext[i]) + toupper(key[j])) % 26) + 'A';
            ciphertext[i] = encryptedChar;
        } else {
            ciphertext[i] = plaintext[i];
            --j;
        }
    }
    ciphertext[i] = '\0';
}

void vigenereDecrypt(char *ciphertext, char *key, char *plaintext) {
    int i, j, keyLen, textLen;
    char decryptedChar;

    keyLen = strlen(key);
    textLen = strlen(ciphertext);

    for (i = 0, j = 0; i < textLen; ++i, ++j) {
        if (j == keyLen)
            j = 0;

        if (isalpha(ciphertext[i])) {
            decryptedChar = ((toupper(ciphertext[i]) - toupper(key[j]) + 26) % 26) + 'A';
            plaintext[i] = decryptedChar;
        } else {
            plaintext[i] = ciphertext[i];
            --j;
        }
    }
    plaintext[i] = '\0';
}

int main() {
    char plaintext[100], key[100], ciphertext[100], decrypted[100];
    int choice;

    printf("Choose an option:\n");
    printf("1. Encryption\n");
    printf("2. Decryption\n");
    printf("Enter your choice: ");
    scanf("%d", &choice);

    printf("Enter the text: ");
    getchar(); 
    fgets(plaintext, sizeof(plaintext), stdin);
    printf("Enter the key: ");
    fgets(key, sizeof(key), stdin);
    plaintext[strcspn(plaintext, "\n")] = '\0';
    key[strcspn(key, "\n")] = '\0';

    switch(choice) {
        case 1:
            vigenereEncrypt(plaintext, key, ciphertext);
            printf("Encrypted Text: %s\n", ciphertext);
            break;
        case 2:
            vigenereDecrypt(plaintext, key, decrypted);
            printf("Decrypted Text: %s\n", decrypted);
            break;
        default:
            printf("Invalid choice.\n");
    }

    return 0;
}

```
## OUTPUT:
## Encryption:
![Screenshot (476)](https://github.com/ashmistalin/Vigenere_Cipher/assets/103128410/f0e13493-4309-4086-9ed7-88cacaadf333)

## Decryption:
![Screenshot (477)](https://github.com/ashmistalin/Vigenere_Cipher/assets/103128410/b4c335dc-6eec-49cc-84e2-39011147c7db)

## RESULT:
The program is executed successfully

-----------------------------------------------------------------------

# Rail Fence Cipher
Rail Fence Cipher using with different key values

# AIM:

To develop a simple C program to implement Rail Fence Cipher.

## DESIGN STEPS:

### Step 1:

Design of Rail Fence Cipher algorithnm 

### Step 2:

Implementation using C code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```
#include <stdio.h>
#include <string.h>

void railFenceEncrypt(char *plaintext, int rails, char *ciphertext) {
    int len = strlen(plaintext);
    int i, j, k = 0;
    char railFence[rails][len];

    for (i = 0; i < rails; i++) {
        for (j = 0; j < len; j++) {
            railFence[i][j] = '\0';
        }
    }

    int dir_down = 0;
    int row = 0;

    for (i = 0; i < len; i++) {
        if (row == 0 || row == rails - 1)
            dir_down = !dir_down;

        railFence[row][i] = plaintext[i];
        dir_down ? row++ : row--;
    }

    for (i = 0; i < rails; i++) {
        for (j = 0; j < len; j++) {
            if (railFence[i][j] != '\0')
                ciphertext[k++] = railFence[i][j];
        }
    }
    ciphertext[k] = '\0';
}

void railFenceDecrypt(char *ciphertext, int rails, char *plaintext) {
    int len = strlen(ciphertext);
    int i, j, k = 0;
    char railFence[rails][len];

    for (i = 0; i < rails; i++) {
        for (j = 0; j < len; j++) {
            railFence[i][j] = '\0';
        }
    }

    int dir_down = 0;
    int row = 0;

    for (i = 0; i < len; i++) {
        if (row == 0)
            dir_down = 1;
        if (row == rails - 1)
            dir_down = 0;

        railFence[row][i] = '*'; 

        dir_down ? row++ : row--;
    }

    for (i = 0; i < rails; i++) {
        for (j = 0; j < len; j++) {
            if (railFence[i][j] == '*' && k < len) {
                railFence[i][j] = ciphertext[k++];
            }
        }
    }

    row = 0;
    dir_down = 0;

    for (i = 0; i < len; i++) {
        if (row == 0)
            dir_down = 1;
        if (row == rails - 1)
            dir_down = 0;

        if (railFence[row][i] != '*')
            plaintext[i] = railFence[row][i];

        dir_down ? row++ : row--;
    }
    plaintext[i] = '\0';
}

int main() {
    char text[100], ciphertext[100], decrypted[100];
    int choice, rails;

    printf("Choose an option:\n");
    printf("1. Encryption\n");
    printf("2. Decryption\n");
    printf("Enter your choice: ");
    scanf("%d", &choice);

    printf("Enter the text: ");
    getchar(); 
    fgets(text, sizeof(text), stdin);

    printf("Enter the number of rails: ");
    scanf("%d", &rails);

    switch(choice) {
        case 1:
            railFenceEncrypt(text, rails, ciphertext);
            printf("Encrypted Text: %s\n", ciphertext);
            break;
        case 2:
            railFenceDecrypt(text, rails, decrypted);
            printf("Decrypted Text: %s\n", decrypted);
            break;
        default:
            printf("Invalid choice.\n");
    }

    return 0;
}

```
## OUTPUT:
## Encryption:
![Screenshot (480)](https://github.com/ashmistalin/RainFence_Cipher/assets/103128410/151e1d4f-191b-4aef-b63a-e8f5bb2bd4f4)

## Decryption:
![Screenshot (481)](https://github.com/ashmistalin/RainFence_Cipher/assets/103128410/fad936c4-a960-48ae-a26d-4562a8df6310)

## RESULT:
The program is executed successfully

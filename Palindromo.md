# Codigos-de-Clase
#include <stdio.h>


int main() {
    int numero;
    int res=0;
    int original, inverso = 0;
    int digito;
    int numIngres;
    
    printf("Ingrese un numero:\n");
    scanf("%d", &numero);
    numIngres = numero;
    
    if (numero < 0)
    res=1;
    
    if (res == 1){
        printf("%d no es un palindromo.\n", numIngres);
        return 0;
    }
    
    original = numero;
    while (numero > 0) {
        digito = numero % 10; 
        inverso = inverso * 10 + digito; 
        numero /= 10;
    }
    
    if (original == inverso) {
        printf("%d es un palindromo.\n", numIngres);
    } else {
        printf("%d no es un palindromo.\n", numIngres);
    }
    
    return 0;
}

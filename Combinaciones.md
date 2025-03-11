#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX 100

// Teclado del telefono
char *digitoALetra[] = {
    "", "", "abc", "def", "ghi", "jkl",
    "mno", "pqrs", "tuv", "wxyz"
};

// Funcion recursiva
void recursividad(char *digitos, int indice, char *actual, char **resultado, int *contador) {
    if (digitos[indice] == '\0') { // Caso base: Se generó una combinación completa
        resultado[*contador] = strdup(actual);
        (*contador)++;
        return;
    }

    // Obtiene las letras correspondientes al digito ingresado
    char *letras = digitoALetra[digitos[indice] - '0'];
    
    for (int i = 0; letras[i] != '\0'; i++) {
        actual[indice] = letras[i]; 
        recursividad(digitos, indice + 1, actual, resultado, contador);
    }
}

// Funcion para obtener las combinaciones
char **combinacionLetras(char *digitos, int *returnRes) {
    if (*digitos == '\0') { 
        *returnRes = 0;
        return NULL;
    }

    char **resultado = (char **)malloc(MAX * sizeof(char *)); // Almacena combinaciones
    char actual[5] = ""; 
    *returnRes = 0;

    recursividad(digitos, 0, actual, resultado, returnRes);
    return resultado;
}


int main() {
    char digitos[5]; 
    printf("Ingrese digitos del (2-9): \n");
    scanf("%4s", digitos);

    int contador = 0;
    char **combinaciones = combinacionLetras(digitos, &contador);

    printf("Combinaciones posibles:\n");
    for (int i = 0; i < contador; i++) {
        printf("%s ", combinaciones[i]);
        free(combinaciones[i]); 
    }
    printf("\n");


    free(combinaciones);
    return 0;
}

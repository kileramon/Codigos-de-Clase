#include <stdio.h>
#include <stdlib.h>

#define MAX (2^31 - 1)
#define MIN (-2^31)

int divicion(int dividendo, int divisor) {
    if (dividendo == MIN && divisor == -1) {
        return MAX;
    }

    // Signo del resultado
    int signo = ((dividendo < 0) ^ (divisor < 0)) ? -1 : 1;

    // Convertir dividendo y divisor a valores positivos usando long para evitar desbordamientos
    long long dvd = labs(dividendo);
    long long dvs = labs(divisor);
    long long cociente = 0;

    while (dvd >= dvs) {
        long long temp = dvs, multiplo = 1;

        while (dvd >= (temp << 1)) {
            temp <<= 1;
            multiplo <<= 1;
        }

        dvd -= temp;
        cociente += multiplo;
    }

    return signo * cociente;
}

int main() {
    int dividendo, divisor, resultado;
    printf("Ingrese el dividendo: \n");
    scanf("%d", &dividendo);
    printf("Ingrese el divisor: \n");
    scanf("%d", &divisor);

    resultado = divicion(dividendo, divisor);
    printf("El resultado: %d\n", resultado);

    return 0;
}

#include <stdio.h>
#include <stdlib.h>

// Comparacion para qsort()
int compara(const void *a, const void *b) {
    return (*(int*)a - *(int*)b);
}

// Funcion para calcular la quimica total
int QuimicaTotal(int* skill, int skillTam) {
    int totalSum = 0;
    for (int i = 0; i < skillTam; i++) {
        totalSum += skill[i];
    }

    // (n / 2)
    if (totalSum % (skillTam / 2) != 0) {
        return -1;
    }
    
    int SumaObjetivo = totalSum / (skillTam / 2); // Suma que debe tener cada equipo
    int quimica = 0;


    qsort(skill, skillTam, sizeof(int), compara);

    // Punteros
    int izq = 0; 
    int der = skillTam - 1;
    while (izq < der) {
        if (skill[izq] + skill[der] != SumaObjetivo) {
            return -1; // No es posible formar equipos
        }
        
        // Calcular la quimica
        quimica += skill[izq] * skill[der];

        izq++;
        der--;
    }

    return quimica;
}


int main() {
    int skill[] = {3, 7, 2, 8, 5, 5}; // Entrada
    int skillTam = sizeof(skill) / sizeof(skill[0]);
    int resultado;

    resultado = QuimicaTotal(skill, skillTam);
    printf("Quimica total: %d\n", resultado);

    return 0;
}

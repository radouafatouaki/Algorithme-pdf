#include <stdio.h>

int main() {
    int A, B, R, Q;      // A et B : les nombres, R : reste, Q : quotient
    int A_init, B_init;  // Pour garder les valeurs initiales

    // Saisie des deux nombres
    printf("Donner le premier nombre A : ");
    scanf("%d", &A);

    printf("Donner le deuxième nombre B : ");
    scanf("%d", &B);

    // Sauvegarde des valeurs initiales
    A_init = A;
    B_init = B;

    printf("\nDébut du calcul du PGCD\n\n");

    // Boucle de l'algorithme d'Euclide
    while (B != 0) {
        Q = A / B;   // Calcul du quotient
        R = A % B;   // Calcul du reste

        // Affichage de la division sous la forme A = B × Q + R
        printf("%d = %d × %d + %d\n", A, B, Q, R);

        // Affichage des valeurs actuelles de A, B et R
        printf("A = %d, B = %d, R = %d\n\n", A, B, R);

        // Mise à jour des valeurs pour la prochaine itération
        A = B;
        B = R;
    }

    // Fin de la boucle : A contient le PGCD
    printf("Le PGCD de %d et %d est : %d\n", A_init, B_init, A);

    // Vérification si les deux nombres sont premiers entre eux
    if (A == 1) {
        printf("Les nombres %d et %d sont premiers entre eux.\n", A_init, B_init);
    } else {
        printf("Les nombres %d et %d ne sont pas premiers entre eux.\n", A_init, B_init);
    }

    return 0;
}

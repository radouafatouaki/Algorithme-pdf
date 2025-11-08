#include <stdio.h>

int pgcd_affiche_etapes(int a, int b) {
    int a1 = a, b1 = b, q, r;
    if (a1 == 0 && b1 == 0) {
        printf("PGCD(0,0) indéfini.\n");
        return 0;
    }
    if (a1 < 0) a1 = -a1;
    if (b1 < 0) b1 = -b1;
    printf("\nÉtapes de l'algorithme d'Euclide pour PGCD(%d, %d):\n", a, b);
    while (b1 != 0) {
        q = a1 / b1;
        r = a1 % b1;
        printf("%d = %d * %d + %d\n", a1, b1, q, r);
        a1 = b1;
        b1 = r;
    }
    printf("PGCD = %d\n", a1);
    return a1;
}

int euclide_etendu(int a, int b, int *x, int *y) {
    int x0 = 1, y0 = 0, x1 = 0, y1 = 1, a0 = a, b0 = b, q, r, tmp;
    while (b0 != 0) {
        q = a0 / b0;
        r = a0 % b0;
        tmp = x0 - q * x1; x0 = x1; x1 = tmp;
        tmp = y0 - q * y1; y0 = y1; y1 = tmp;
        a0 = b0;
        b0 = r;
    }
    *x = x0;
    *y = y0;
    if (a0 < 0) a0 = -a0;
    return a0;
}

int main() {
    int a, b, c, d, x0, y0, x_part, y_part;
    printf("ÉQUATION DIOPHANTIENNE : a*x + b*y = c\n");
    printf("Entrez a : ");
    scanf("%d", &a);
    printf("Entrez b : ");
    scanf("%d", &b);
    d = pgcd_affiche_etapes(a, b);
    if (d == 0) {
        printf("Cas particulier : a = 0 et b = 0 → pas de solution.\n");
        return 0;
    }
    if (d == 1)
        printf("Les nombres %d et %d sont premiers entre eux (PGCD = 1).\n", a, b);
    else
        printf("Les nombres %d et %d ne sont pas premiers entre eux (PGCD = %d).\n", a, b, d);
    euclide_etendu(a, b, &x0, &y0);
    printf("Théorème de Bézout : il existe x0, y0 tels que a*x0 + b*y0 = d.\n");
    printf("Coefficients trouvés : x0 = %d, y0 = %d\n", x0, y0);
    printf("Vérification : %d*%d + %d*%d = %d\n", a, x0, b, y0, a*x0 + b*y0);
    printf("Entrez c : ");
    if (scanf("%d", &c) != 1) {
        printf("Erreur de lecture de c.\n");
        return 0;
    }
    if (c % d != 0) {
        printf("Pas de solution entière car %d ne divise pas %d.\n", d, c);
        return 0;
    }
    x_part = x0 * (c / d);
    y_part = y0 * (c / d);
    printf("Solution particulière : (x_p, y_p) = (%d, %d)\n", x_part, y_part);
    printf("Solution générale :\n");
    printf("x = %d + (%d)*k\n", x_part, b / d);
    printf("y = %d - (%d)*k\n", y_part, a / d);
    printf("où k est un entier.\n");
    printf("Programme terminé avec succès.\n");
    return 0;
}

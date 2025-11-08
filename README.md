#include <stdio.h>

int pgcd_affiche_etapes(int a, int b) {
    int a1 = a, b1 = b, q, r;
    if (a1 == 0 && b1 == 0) {
        printf("PGCD(0,0) indéfini.\n");
        return 0;
    }
    if (a1 < 0) a1 = -a1;
    if (b1 < 0) b1 = -b1;

    printf("Etape 1 : Calcul du PGCD\n");
    while (b1 != 0) {
        q = a1 / b1;
        r = a1 % b1;
        printf("%d = %d * %d + %d\n", a1, b1, q, r);
        a1 = b1;
        b1 = r;
    }
    printf("Le PGCD est : %d\n", a1);
    return a1;
}

int euclide_etendu(int a, int b, int *x, int *y) {
    int x0 = 1, y0 = 0, x1 = 0, y1 = 1;
    int a0 = a, b0 = b, q, r, tmp;

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

    printf("Donner a : ");
    scanf("%d", &a);
    printf("Donner b : ");
    scanf("%d", &b);

    d = pgcd_affiche_etapes(a, b);

    if (d == 0) {
        printf("Cas particulier : a = 0 et b = 0, pas de solution.\n");
        return 0;
    }

    if (d == 1)
        printf("Les deux nombres sont premiers entre eux.\n");
    else
        printf("Les deux nombres ne sont pas premiers entre eux.\n");

    printf("Entrez la valeur de c pour l'équation a*x + b*y = c : ");
    scanf("%d", &c);

    if (c % d != 0) {
        printf("Il n'existe pas de solution entière car %d ne divise pas %d.\n", d, c);
        return 0;
    } else {
        printf("Il existe au moins une solution entière car %d divise %d.\n", d, c);
    }

    printf("Etape 2 : Calcul des coefficients de Bézout\n");
    euclide_etendu(a, b, &x0, &y0);
    printf("Selon le théorème de Bézout : %d*(%d) + %d*(%d) = %d\n", a, x0, b, y0, a*x0 + b*y0);

    printf("Etape 3 : Calcul d'une solution particulière\n");
    x_part = x0 * (c / d);
    y_part = y0 * (c / d);
    printf("Une solution particulière de %d*x + %d*y = %d est : (x0, y0) = (%d, %d)\n", a, b, c, x_part, y_part);

    printf("Etape 4 : Solution générale\n");
    printf("x = %d + (%d)*k\n", x_part, b / d);
    printf("y = %d - (%d)*k\n", y_part, a / d);
    printf("où k est un entier.\n");

    return 0;
}

# DAX Measures — Gestion des Stocks

## 1. Entrées
Entrès = SUMX(
    FILTER(Mvt,Mvt[Sens]="E"),
    Mvt[QteMvt]
)

## 2. Sorties
Sorties = SUMX(
    FILTER(Mvt,Mvt[Sens]="S"),
    Mvt[QteMvt]
)

## 3. Solde
Solde = SUMX(
    Mvt,
    'Indicateurs'[Entrès]-'Indicateurs'[Sorties]
)

## 4. Solde Trimestriel
Solde_trim = DIVIDE(
    [Solde],
    COUNTX(VALUES(T_date[mois]),T_date[mois]),
    0
)

## 5. Solde par Famille
Solde_par_famille = DIVIDE(
    [Solde],
    COUNTX(VALUES(Mvt[Ref]),Mvt[Ref])
)

## 6. Total Ventes
Total Ventes = SUMX(
    FILTER(Mvt,Mvt[CodeTypeMvt]=3),
    Mvt[QteMvt]
)

## 7. Taux de Rotation
Taux de rotation = DIVIDE(
    [Total Ventes],
    [Solde_trim],
    0
)

## 8. MVT PAR CLIENT
MVT PAR CLIENT = SUMX(
    RELATEDTABLE(Mvt),
    Mvt[QteMvt]
)
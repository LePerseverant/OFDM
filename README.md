![ENSA_Logo](ENSA_Logo.png)


# [ Python ] Mise en place d'une chaîne de communication digitale - OFDM

Dans ce projet, nous allons explorer les bases d'un système OFDM du côté émission et réception. L'OFDM (multiplexage par répartition orthogonale de la fréquence) est un système multicarrier largement utilisé dans diverses transmissions sans fil comme LTE, WiMAX, DVB-T et DAB. Le principe clé d'un système multicarrier implique la division d'un flux de données à haut débit en plusieurs sous-porteuses étroites à débit réduit.

### Cette approche présente plusieurs avantages :

1. La durée du symbole étant inversement proportionnelle au débit de symboles, chaque sous-porteuse présente des symboles relativement longs. Ces symboles prolongés sont résistants aux problèmes tels que l'affaiblissement par trajets multiples, courant dans les systèmes sans fil.

2. En cas d'atténuation sévère d'une porteuse spécifique due aux caractéristiques sélectives en fréquence du canal (entraînant une réception très faible sur cette porteuse), seules les données de cette sous-porteuse sont perdues, et non la totalité du flux de données.

3. Les systèmes multicarriers facilitent l'allocation efficace des ressources entre plusieurs utilisateurs en attribuant différentes sous-porteuses à différents utilisateurs.
Veuillez considérer le schéma en blocs suivant, qui englobe les blocs fondamentaux du système OFDM :

![OFDM_channel](OFDM.png)

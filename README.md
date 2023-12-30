![ENSA_Logo](ENSA_Logo.png)


# [Python] Mise en place d'une chaîne de communication digitale - OFDM

Dans ce projet, nous allons explorer les bases d'un système OFDM du côté émission et réception. L'OFDM (multiplexage par répartition orthogonale de la fréquence) est un système multicarrier largement utilisé dans diverses transmissions sans fil comme LTE, WiMAX, DVB-T et DAB. Le principe clé d'un système multicarrier implique la division d'un flux de données à haut débit en plusieurs sous-porteuses étroites à débit réduit.

### Cette approche présente plusieurs avantages :

1. La durée du symbole étant inversement proportionnelle au débit de symboles, chaque sous-porteuse présente des symboles relativement longs. Ces symboles prolongés sont résistants aux problèmes tels que l'affaiblissement par trajets multiples, courant dans les systèmes sans fil.

2. En cas d'atténuation sévère d'une porteuse spécifique due aux caractéristiques sélectives en fréquence du canal (entraînant une réception très faible sur cette porteuse), seules les données de cette sous-porteuse sont perdues, et non la totalité du flux de données.

3. Les systèmes multicarriers facilitent l'allocation efficace des ressources entre plusieurs utilisateurs en attribuant différentes sous-porteuses à différents utilisateurs.
Veuillez considérer le schéma en blocs suivant, qui englobe les blocs fondamentaux du système OFDM :

![OFDM_channel](OFDM.png)

# Titre : Compréhension des systèmes OFDM - Analyse de l'émetteur et du récepteur

## Aperçu :
Ce cahier Jupyter offre une exploration approfondie du système de multiplexage par répartition orthogonale de la fréquence (OFDM), couvrant ses composants fondamentaux, ses opérations et ses avantages. Le cahier examine à la fois les aspects de l'émetteur et du récepteur d'OFDM, en mettant en lumière son application dans divers systèmes de communication sans fil tels que LTE, WiMAX, DVB-T et DAB.

## Table des matières :
1. Introduction à l'OFDM
2. Avantages de l'OFDM
3. Composants de l'émetteur :
   - Génération des sous-porteuses
   - Mappage des données aux sous-porteuses
   - Insertion des porteuses pilotes
   - Transformée de Fourier inverse rapide (IFFT)
   - Ajout de préfixe cyclique
   - Transmission du signal
4. Composants du récepteur :
   - Réception du signal
   - Suppression du préfixe cyclique
   - Transformée de Fourier rapide (FFT)
   - Démappage des sous-porteuses
   - Estimation du canal à l'aide des porteuses pilotes
   - Récupération des données
5. Conclusion

## Bibliothèques utilisées :
- NumPy
- Matplotlib
- Scipy

## Instructions d'exécution :
1. Assurez-vous que toutes les bibliothèques requises sont installées.
2. Exécutez les cellules dans l'ordre séquentiel.
3. Vérifiez les sorties et visualisations aux sections pertinentes.

## Utilisation :
Ce cahier sert de ressource pédagogique pour comprendre les blocs de base d'un système OFDM. Il peut être utilisé à des fins d'apprentissage, d'expérimentation avec différents paramètres et pour acquérir des informations sur le fonctionnement d'OFDM.

## Remerciements :
- Un sincère remerciement au ***Professeur*** **Fouad Aytouna** pour ses précieuses contributions, conseils et soutien tout au long.
- 
## Informations sur l'auteur :
- Nom : **[Redouane Benarif]**
- Contact : **[redouanebenarif@gmail.com]**
- Date de création : **[26-12-2023]**

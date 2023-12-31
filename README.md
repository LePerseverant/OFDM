![ENSA_Logo](ENSA_Logo.png)


# [Python] Mise en place d'une chaîne de communication digitale - OFDM

Dans ce projet, nous allons explorer les bases d'un système OFDM du côté émission et réception. L'OFDM (multiplexage par répartition orthogonale de la fréquence) est un système multicarrier largement utilisé dans diverses transmissions sans fil comme LTE, WiMAX, DVB-T et DAB. Le principe clé d'un système multicarrier implique la division d'un flux de données à haut débit en plusieurs sous-porteuses étroites à débit réduit.

## Cette approche présente plusieurs avantages :

1. La durée du symbole étant inversement proportionnelle au débit de symboles, chaque sous-porteuse présente des symboles relativement longs. Ces symboles prolongés sont résistants aux problèmes tels que l'affaiblissement par trajets multiples, courant dans les systèmes sans fil.

2. En cas d'atténuation sévère d'une porteuse spécifique due aux caractéristiques sélectives en fréquence du canal (entraînant une réception très faible sur cette porteuse), seules les données de cette sous-porteuse sont perdues, et non la totalité du flux de données.

3. Les systèmes multicarriers facilitent l'allocation efficace des ressources entre plusieurs utilisateurs en attribuant différentes sous-porteuses à différents utilisateurs.
Veuillez considérer le schéma en blocs suivant, qui englobe les blocs fondamentaux du système OFDM :

![OFDM_channel](OFDM.png)

## Aperçu :
Ce cahier Jupyter offre une exploration approfondie du système de multiplexage par répartition orthogonale de la fréquence (OFDM), couvrant ses composants fondamentaux, ses opérations et ses avantages. Le cahier examine à la fois les aspects de l'émetteur et du récepteur d'OFDM, en mettant en lumière son application dans divers systèmes de communication sans fil tels que LTE, WiMAX, DVB-T et DAB.

## Code Blocks :
- Composants de l'émetteur :
   - Génération des sous-porteuses
     ```python
     K = 64 # number of OFDM subcarriers
     CP = K//4  # length of the cyclic prefix: 25% of the block
     P = 8 # number of pilot carriers per OFDM block
     pilotValue = 3+3j # The known value each pilot transmits
     allCarriers = np.arange(K)  # indices of all subcarriers ([0, 1, ... K-1])
      
     pilotCarriers = allCarriers[::K//P] # Pilots is every (K/P)th carrier.
      
     # For convenience of channel estimation, let's make the last carriers also be a pilot
     pilotCarriers = np.hstack([pilotCarriers, np.array([allCarriers[-1]])])
     P = P+1 
      
     # data carriers are all remaining carriers
     dataCarriers = np.delete(allCarriers, pilotCarriers)
     ```
   - Mappage des données aux sous-porteuses
     ```python
     def Mapping(bits):
        return np.array([mapping_table[tuple(b)] for b in bits])
     QAM = Mapping(bits_SP)
     print ("First 5 QAM symbols and bits:")
     print (bits_SP[:5,:])
     print (QAM[:5])
     ```
   - Insertion des porteuses pilotes
     ```python
     def OFDM_symbol(QAM_payload):
        symbol = np.zeros(K, dtype=complex) # the overall K subcarriers
        symbol[pilotCarriers] = pilotValue  # allocate the pilot subcarriers 
        symbol[dataCarriers] = QAM_payload  # allocate the pilot subcarriers
        return symbol
     OFDM_data = OFDM_symbol(QAM)
     print ("Number of OFDM carriers in frequency domain: ", len(OFDM_data))
     ```
      - Transformée de Fourier inverse rapide (IFFT)
     ```python
     def IDFT(OFDM_data):
        return np.fft.ifft(OFDM_data)
     OFDM_time = IDFT(OFDM_data)
     print ("Number of OFDM samples in time-domain before CP: ", len(OFDM_time))
     ``` 
   - Ajout de préfixe cyclique
     ```python
     def addCP(OFDM_time):
        cp = OFDM_time[-CP:]               # take the last CP samples ...
        return np.hstack([cp, OFDM_time])  # ... and add them to the beginning
     OFDM_withCP = addCP(OFDM_time)
     print ("Number of OFDM samples in time domain with CP: ", len(OFDM_withCP))
     ```    
   - Transmission du signal
     ```python
     def channel(signal):
        convolved = np.convolve(signal, channelResponse)
        signal_power = np.mean(abs(convolved**2))
        sigma2 = signal_power * 10**(-SNRdb/10)  # calculate noise power based on signal power and SNR
    
        print ("RX Signal power: %.4f. Noise power: %.4f" % (signal_power, sigma2))
    
        # Generate complex noise with given variance
        noise = np.sqrt(sigma2/2) * (np.random.randn(*convolved.shape)+1j*np.random.randn(*convolved.shape))
        return convolved + noise
     OFDM_TX = OFDM_withCP
     OFDM_RX = channel(OFDM_TX)
     ```
- Composants du récepteur :
   - Réception du signal
   - Suppression du préfixe cyclique
   - Transformée de Fourier rapide (FFT)
   - Démappage des sous-porteuses
   - Estimation du canal à l'aide des porteuses pilotes
   - Récupération des données

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
- Un sincère remerciement au **Professeur Fouad Aytouna** pour ses précieuses contributions, conseils et soutien tout au long.
## Informations sur l'auteur :
- Nom : **[Redouane Benarif]**
- Contact : **[redouanebenarif@gmail.com]**
- Date de création : **[26-12-2023]**

# Challenge RootMe : CISCO - mot de passe

**Catégorie** : Réseau  
**Difficulté** : ⭐⭐  
**Objectif** : Trouver le mot de passe “Enable” à partir d'une configuration Cisco.

---

## 📝 Étapes de résolution

### 1. Lancer le challenge
- Rendez-vous sur la section **Network Challenges** de Root Me.
- Sélectionnez le challenge **CISCO - mot de passe**.
- Cliquez sur **start the challenges** pour démarrer l'exercice.

### 2. Analyse de la configuration Cisco
Dans la configuration, on trouve les éléments suivants :
```plaintext
hostname rmt-paris
!
security passwords min-length 8
no logging console
enable secret 5 $1$p8Y6$MCdRLBzuGlfOs9S.hXOp0.
!
username hub password 7 025017705B3907344E
username admin privilege 15 password 7 10181A325528130F010D24
username guest password 7 124F163C42340B112F3830
```
- enable secret 5 indique que le mot de passe Enable est chiffré avec une méthode de type 5 (md5crypt), une méthode réversible.
- Les autres mots de passe (pour hub, admin et guest) sont chiffrés en méthode 7, qui est également réversible.

### 3. Utilisation d'une plateforme de décryptage en ligne

Cisco utilise des méthodes d'encryption réversibles. Pour décrypter ces valeurs, on peut utiliser l'outil en ligne Cisco Password Cracker (disponible sur ifm.net.nz).

Étapes sur l'outil en ligne :
Rendez-vous sur le site Cisco Password Cracker.
Entrez les valeurs chiffrées des différents utilisateurs extraites de la configuration.
L'outil décrypte les mots de passe et affiche les résultats correspondants.

### 4. Résultats du décryptage

Après avoir soumis les valeurs, les résultats obtenus sont les suivants :

- hub : 6sK0_hub
- admin : 6sK0_admin
- guest : 6sK0_guest

###  5. Déduction du mot de passe Enable

En observant le schéma utilisé pour les autres comptes, il est logique de penser que le mot de passe Enable suit le même modèle.
Ainsi, le mot de passe Enable est :
```plaintext
6sK0_enable
``` 

**🛠 Outils et ressources utilisés**
- Plateforme Root Me : Pour accéder et lancer le challenge.
- Cisco Password Cracker : Outil en ligne permettant de décrypter les mots de passe Cisco.
- Documentation et articles spécialisés : Pour comprendre que l’encryption Cisco de type 5 et 7 est réversible.

**🏆 Solution finale**
Enable Password :`enable:6sK0_enable`


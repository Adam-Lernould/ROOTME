# Challenge RootMe : It happens, sometimes

**Catégorie** : Exploitation Web  
**Difficulté** : ⭐  
**Objectif** : Accéder à la section d'administration du site et obtenir le mot de passe.

---

## 📝 Étapes de résolution

### 1. Découverte du chemin d'accès
- **Analyse du site** :  
  On part de l'URL de base :  
  ```plaintext
  http://challenge01.root-me.org/realiste/ch3/
  ```
- **Bruteforce des répertoires** :
  Utilisation de l'outil dirb avec le dictionnaire fourni :
  ```bash
  dirb http://challenge01.root-me.org/realiste/ch3/ /usr/share/dict/dirb-wordlists/small.txt
  ```
- **Résultat** :  
  Le brute force révèle une page d'administration cachée à l'URL :
  ```plaintext
  http://challenge01.root-me.org/realiste/ch3/admin
  ```
## 2. Exploitation via l'interception proxy avec Burp Suite  

Pour accéder à la section administration, il faut modifier la méthode HTTP de la requête.  

- **Accès à la page admin** :
  
  Rendez-vous sur l'URL suivante dans votre navigateur :
  ```plaintext
  http://challenge01.root-me.org/realiste/ch3/admin
  ```
  La requête initiale (utilisant la méthode GET) sera interceptée par Burp Suite.

- **Modification de la requête** :
  
  Dans l'onglet Proxy > Intercept de Burp Suite, modifiez la requête en changeant la méthode GET en PUT.  
  Exemple de requête modifiée :
  ```http
  PUT /realiste/ch3/admin HTTP/1.1
  Host: challenge01.root-me.org
  [Autres en-têtes...]
  ```
-**Forwarding** :  

Une fois la modification effectuée, cliquez sur Forward pour envoyer la requête modifiée au serveur.  

## 3. Récupération du mot de passe  

  Réponse du serveur :  
  La réponse renvoyée par le serveur fournit le mot de passe nécessaire pour valider le challenge.
  
  Mot de passe trouvé :
  ```plaintext
  0010110111101001
  ```
 
**🛠 Outils utilisés**  
- dirb : Pour le brute force des répertoires et fichiers.  
- Burp Suite : Pour l'interception et modification des requêtes HTTP.  
- Navigateur Web (ex. Firefox) : Pour accéder aux URLs et interagir avec le proxy.  

**🏆 Solution finale**  

Mot de passe / Password :  
```plaintext
0010110111101001
```
  

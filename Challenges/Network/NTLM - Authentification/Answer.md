# Challenge RootMe : Authentification NTLM

- **Catégorie** : Réseau 
- **Difficulté** : ⭐⭐
- **Objectif** : Retrouver le mot de passe d'un utilisateur à partir d'une capture NTLMv2.

---

## 📝 Étapes de résolution

### 1. **Analyse des trames NTLM avec Wireshark**
   - **Trame Challenge (Type 2)** : Extraction du `Server Challenge` et du domaine :
     ```plaintext
     Server Challenge: 1944952f5b845db1
     Domain: catcorp.local (DNS)
     ```
   - **Trame Authenticate (Type 3)** : Récupération des éléments critiques :
     ```plaintext
     User: john.doe
     NTProofStr (HMAC-MD5): 5c336c6b69fd2cf7b64eb0bde3102162
     NTLMv2 Response: 01010000... (données complètes)
     ```

### 2. **Formatage du hash pour Hashcat**
   ```plaintext
   john.doe::catcorp.local:1944952f5b845db1:5c336c6b69fd2cf7b64eb0bde3102162:01010000...
   ```
### 3. Crack du mot de passe avec Hashcat
  -**Commande utilisée**:
    ``bash
    hashcat -m 5600 -O hash.txt crackstation-human-only.txt
    ```

    Si crackstation-human-only.txt n'est pas installé : 

    ```bash
    wget https://crackstation.net/files/crackstation-human-only.txt.gz
    gunzip crackstation-human-only.txt.gz
    ```

  -**Résultat : Mot de passe cracké en 56 secondes :**
    ```plaintext
    Password: rootbeer
    ```
### 🏆 Solution finale
--> Flag :
```plaintext
RM{john.doe@catcorp.local:rootbeer}
``` 
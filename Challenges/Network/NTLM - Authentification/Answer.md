# Challenge RootMe : Authentification NTLM

**Catégorie** : Réseau / Cryptographie  
**Difficulté** : ⭐⭐  .
**Objectif** : Retrouver le mot de passe d'un utilisateur à partir d'une capture NTLMv2.

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

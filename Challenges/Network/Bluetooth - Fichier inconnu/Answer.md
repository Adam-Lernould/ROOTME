# Challenge RootMe : Bluetooth - Fichier inconnu

**Catégorie** : Réseau / Analyse de paquets  
**Difficulté** : ⭐⭐  
**Objectif** : Extraire et analyser une capture Bluetooth afin d'obtenir le hash SHA1 de la concaténation de l'adresse MAC (en majuscules) et du nom du téléphone.

---

## 📝 Étapes de résolution

### 1. Ouverture de la capture dans Wireshark
- **Format du fichier** :  
  Le challenge était fourni sous forme d'un fichier `.bin`.  
  Pour faciliter l'analyse, j'ai renommé le fichier en `.btsnoop` afin que Wireshark le reconnaisse automatiquement comme une capture Bluetooth.
- **Chargement** :  
  J'ai ouvert le fichier dans Wireshark et appliqué un filtre pour isoler les trames pertinentes.

### 2. Identification des informations clés
- **Filtrage** :  
  En utilisant un filtre comme `bthci_evt.code == 0x07` (ou en recherchant directement le terme "Name" dans la colonne *Info*), j'ai repéré la trame **Remote Name Request Complete**.
- **Extraction** :
  - **Adresse MAC** :  
    La trame indiquait la BD_ADDR `0c:b3:19:b9:4f:c6`.  
    Conversion en majuscules → `0C:B3:19:B9:4F:C6`.
  - **Nom du téléphone** :  
    Le champ « Remote Name » contenait la valeur `GT-S7390G`.

### 3. Concaténation et calcul du hash SHA1
- **Concaténation** :  
  J'ai fusionné l'adresse MAC et le nom du téléphone sans aucun espace ni séparateur supplémentaire.  
  **Chaîne obtenue** :
  0C:B3:19:B9:4F:C6GT-S7390G

- **Calcul du hash** :  
J'ai utilisé la commande suivante dans un terminal sous Linux :
```bash
echo -n "0C:B3:19:B9:4F:C6GT-S7390G" | sha1sum
```

- **Résultat **:
```plaintext
c1d0349c153ed96fe2fadf44e880aef9e69c122b
```

**🛠 Outils utilisés**
- Wireshark : Pour l'analyse et l'extraction des trames Bluetooth
- Terminal (bash) : Pour le calcul du hash SHA1 avec sha1sum
- Éditeur de texte : Pour préparer et vérifier la chaîne de caractères à hasher

**🏆 Solution finale**
Flag :
```plaintext
c1d0349c153ed96fe2fadf44e880aef9e69c122b
```

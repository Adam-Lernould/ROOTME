# Challenge RootMe : Authentification NTLM

**Catégorie** : Réseau / Cryptographie  
**Difficulté** : ⭐⭐  
**Objectif** : Retrouver le mot de passe d'un utilisateur à partir d'une capture NTLMv2.

---

## 📝 Étapes de résolution

### 1. Analyse de la capture avec [A-Packets](https://apackets.com/)
L'outil en ligne permet une extraction automatisée du hash NTLMv2 :
```plaintext
john.doe::catcorp.local:1944952F5B845DB1:5C336C6B69FD2CF7B64EB0BDE3102162:01010000000000001A9790044B63DA0175304C546C6F34320000000002000E0043004100540043004F005200500001000800440043003000310004001A0063006100740063006F00720070002E006C006F00630061006C000300240044004300300031002E0063006100740063006F00720070002E006C006F00630061006C0005001A0063006100740063006F00720070002E006C006F00630061006C00070008001A9790044B63DA010900120063006900660073002F0044004300300031000000000000000000
```
**🕵️ Analyse Manuelle des Trames NTLMv2** 
- Trame Challenge - Type 2 :
Structure :
~~~~
  NTLMSSP_CHALLENGE (0x02)
├─ Server Challenge : 1944952f5b845db1 (8 octets)
├─ Target Name : CATCORP
├─ Target Info :
│  ├─ NetBIOS domain : CATCORP
│  ├─ DNS domain : catcorp.local
│  ├─ Computer name : DC01
│  └─ Timestamp : [Valeur temporelle]
└─ Version : Windows 10 (Build 17763)
~~~~

- Trame Authenticate - Type 3 : 
Données critiques :
~~~~
NTLMSSP_AUTH (0x03)
├─ User : john.doe
├─ Domain : catcorp.local (DNS)
├─ NTProofStr : 5C336C6B69FD2CF7B64EB0BDE3102162 (HMAC-MD5)
├─ NTLMv2 Response : 
│  ├─ Client Challenge : 75304C546C6F3432
│  ├─ Target Info : 
│  │  ├─ DNS domain : catcorp.local
│  │  ├─ Computer name : DC01.catcorp.local
│  │  └─ Service : cifs/DC01
│  └─ Timestamp : Feb 19, 2024 15:48:01.113269800 UTC
└─ Session Key : b96de84b47696a6800dfb52bf5935c75
~~~~

### 2. **Crack du hash avec Hashcat**
   - **Commande** :
     ```bash
     hashcat -m 5600 -a 0 hash.txt /usr/share/wordlists/rockyou.txt
     ```
   - **Résultat** : Mot de passe trouvé en quelques secondes :
     ```plaintext
     Password: rootbeer
     ```

### 3. **Alternative avec John the Ripper**
   - **Commande** :
     ```bash
     john --format=netntlmv2 hash.txt
     ```
   - **Résultat identique** : `rootbeer`

---

## 🛠 Outils utilisés
- **[A-Packets](https://apackets.com/)** : Extraction automatisée du hash
- **Hashcat (mode 5600)** : Crack rapide avec `rockyou.txt`
- **John the Ripper** : Alternative efficace pour NTLMv2
- **Wireshark** : Vérification manuelle optionnelle

---

## 🏆 Solution finale
**Flag** :  
```plaintext
RM{john.doe@catcorp.local:rootbeer}

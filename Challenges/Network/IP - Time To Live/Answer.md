# Challenge RootMe : IP - Time To Live

**Catégorie** : Analyse de capture réseau  
**Difficulté** : ⭐⭐    
**Objectif** : Retrouver le TTL suffisant pour atteindre la machine cible à partir d’un échange de paquets ICMP.

---

## 📝 Étapes de résolution

### 1. Analyse de la capture avec Wireshark
- **Téléchargement** : Récupérez la capture réseau fournie dans l’énoncé.
- **Filtrage** : Utilisez le filtre `icmp` pour isoler les paquets ICMP de l’échange.

### 2. Identification du paquet pertinent
- **Observation** : La machine cible (198.173.244.32) a répondu au paquet dont le numéro de trame est **71**.
- **Affichage du TTL** : Pour une bonne visibilité, il est recommandé d'afficher la colonne TTL :
  - Cliquez droit sur le champ **TTL** dans un paquet.
  - Sélectionnez **"Apply as a column"** (ou utilisez le raccourci `Ctrl+Shift+I`).
- Cela permet de visualiser rapidement, dans la liste des paquets, le TTL minimum qui a permis d'atteindre la machine cible.

### 3. Détermination du TTL minimum
- En analysant la colonne TTL, on constate que le TTL minimum qui a permis d’atteindre la machine cible est :
  ```plaintext
  13
  ```

### 4. Astuce complémentaire

Flow Graph : Vous pouvez également utiliser la fonction Statistics -> Flow Graph dans Wireshark pour visualiser l’évolution des TTL et comprendre rapidement le fonctionnement d’un traceroute.

**🛠 Outils utilisés**  
Wireshark : Pour l’analyse et l’inspection détaillée de la capture réseau.

**🏆 Solution finale**
Mot de passe :
```plaintext
13
```

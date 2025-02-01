# Challenge RootMe : Authentification Kerberos

- **Catégorie** : Réseau 
- **Difficulté** : ⭐⭐
- **Objectif** : Retrouver le mot de passe d'un utilisateur à partir d'une capture TELNET.

The flag format is:  

- RM{userPrincipalName:password}
A **SHA-256 hash** is provided to validate the response.

---

## 🔍 Initial Analysis: Data Extraction  

We started by analyzing the **`.pcapng`** file containing network traffic and focused on **Kerberos packets**.

### 1️⃣ Filtering Packets in Wireshark  
1. **Open the `.pcapng` file** with Wireshark.  
2. **Apply the `kerberos` filter** in the search bar.  
3. **Identify the AS-REQ packet** (Kerberos Authentication Request).  

We then examined the structure of the **AS-REQ** frame.

---

## 🛠 Extracting Key Information  
### 2️⃣ Retrieving the Encrypted Password Hash  
Within the **AS-REQ** frame, we navigated to:
- **Kerberos → as-req → padata → PA-ENC-TIMESTAMP → padata-value**  
  👉 **This contains the encrypted password hash.**  

### 3️⃣ Extracting the Username  
Within the same frame, we found:
- **Kerberos → req-body → cname → cname-string → CNameString**  
  👉 The extracted value was **`william.dupond`**.  
- **Realm: `CATCORP.LOCAL`**  

The full **userPrincipalName** is:

- william.dupond@CATCORP.LOCAL

---

## 🔑 Cracking the Password with Hashcat  
We identified that the hash type is **AES256-CTS-HMAC-SHA1-96 (etype 18)**.  
Consulting the Hashcat documentation, we found that **mode 19900** is the correct one.

### 4️⃣ Hashcat Command Used  
```bash
hashcat -m 19900 "$krb5pa$18$william.dupond$CATCORP.LOCAL$fc8bbe22b2c967b222ed73dd7616ea71b2ae0c1b0c3688bfff7fecffdebd4054471350cb6e36d3b55ba3420be6c0210b2d978d3f51d1eb4f" /usr/share/wordlists/rockyou.txt

```

### 5️⃣ Cracked Password
After running Hashcat, the password was successfully recovered:
```bash
kittycat12
```
🏁 Flag Validation
Since the flag format is:
```bash
RM{userPrincipalName:password}
```
We constructed:

RM{william.dupond@catcorp.local:kittycat12}

---

🏆 Tools Used
Wireshark → Packet analysis.
Hashcat → Password cracking for AES256-CTS-HMAC-SHA1-96.
Rockyou.txt → Wordlist for dictionary attack.
SHA-256 → Final flag validation.


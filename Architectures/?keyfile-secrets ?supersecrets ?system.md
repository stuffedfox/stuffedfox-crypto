# Encrypted keyfile + Encrypted system storage + additional secrets storage
Based on an encrypted DB/keyfile using a password and additional keyfile in order to decrypt. This architecture is based on the concept of "Master" and "Pseudo Master" passwords, where two passwords are used to segregate security between devices, in this case full/partial sytsem encryption, where the password for the DB/keyfile is the same as your disk encryption, since leaking either will give you access to the password manager DB or the keyfile respectively. In this archtecture the DB and the keyfile are stored under the same password on the KeyDrive, as the password manager itself is protected under the Pseudo Master password. The primary benefit of this system is reducing complexity by only requiring the user to memorize two passwords of sufficient entropy. While providing extremely convenient access to both the keyfile and DB, through a keyfile installed on your Authorized System, which will be unlocked via your Master Password. This allows the user to plug in the KeyDrive, while having autonomous access to the database in one central location. Since you can protect a LUKs block using passwords as well, this doesn't restrict you to an already authorized system. 

The primary design intent for this architecture is requiring access to both the KeyDrive, and the Decrypted system in order to provide a serious attack vector. With the decryted system storing a simple disk image of the drive, the decrypted system is argubaly the most likely attack vector in this scenario. So you should either store your secrets on a separately encrypted block, using a third password for disk encryption. Or practice better opsec, and encrypt your device when you leave it unattended. However if the system is encrypted, and the KeyDrive is not present, there is no serious attack vector present. However given the importance of using secure passwords, this isn't a huge concern for this particular architecture. Future architectures will expand upon this concept however. 

### Pros:
- Provides sufficiently advanced security, at low overhead.
- Easily modified to further improve security by simply adding a third separate password. (vulnerable to live system attacks)
- The KeyDrive is now fully encrypted, unless someone gets access to your system while decrypted, or knows the password/keyfile for decryption, it's guaranteed secure.
- Comprehensive architecture prevents user from being an attack vector due to poor opsec.
- Architecture also provides convenient and accessible ways to perform KeyDrive backups, either through imaging, or more complex means. All secure.
- Keyfile implementation allows user to comfortably store the DB wherever their security tolerance allows.
- Due to both Keyfile and DB being accessible through one password, onboarding additional systems is trivial. Through further integration in scripting, onboarding Authorized Systems can be trivial.
- Architecture doesn't strictly require a KeyDrive, a mountable KeyDrive image will substitute just fine with similar security to the compromised threat model described. 

### Cons:
- Architecture is more complex and involved, requiring more setup.
- Suffers from usual attack vectors (user leaving DB unlocked) and decrypted system attacks will always guarantee a minimum of the DB and keyfile (less than ideal)
- Potential to suffer from catastrophic failure permanently destroying all secrets. (mitigation is available through KeyDrive backups)
- Not clear whether DB should be stored on the KeyDrive, or the Authorized System. May lead to user confusion. As well as DB desyncing (potentially mitigated through "keepassxc sharing"
- DB keyfile could be argued as "redundant" through most attack vectors.

  Overall Rating: 7/10

  The architecture has been substantially improved, the user accessibility has significantly increased. General OpSec presence has improved considerably as well. It also provides substantially increased user utility through native DB access, secrets will never be inconvenient to access. 

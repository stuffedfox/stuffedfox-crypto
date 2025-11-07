# KeyDrive Architecture (or more accurately, architecture for the script that will be generating KeyDrives)

### Terminology
- key-store: generic unencrypted partition, most often used for less secure keyfile storage.
- secret: LUKS partition containing the DB and or keyfile
- system-secret: LUKS parition for handling secrets between systems in an automated manner without disturbing security.
- super-secret: LUKS partition for secure user secrets, the key should be stored in your DB. (ssh keys for instance)
- store: A generic partition or volume encrypted or not, for general use storage.

### Design philosophy
There are three primary goals behind the philosophy of the generation script. The first one is to keep it minimal, the script shouldn't be frequently used. The second is to provide automation, through some form of formatting table. The third goal is flexibility, the script shouldn't be on rails for any particular function, each user has it's usecases for different features, let users configure it how they see fit.

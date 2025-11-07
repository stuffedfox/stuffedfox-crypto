# Practical modular crypto implemented on top of established cryptographic software

### Goals:

- The primary goal of this project is to document the development of a framework that allows to flexibly store secrets in a generic and flexible manner, without compromising on security.
- The long term goal of this project is to create a generic security framework that allows you to store encrypted secrets on a generic USB drive, while providing sufficient redundancy to ensure you never get locked out, or run into access control issues.

### Problems currently faced:

- Proprietary cloud based password managers offer a lot of utility (syncing) while providing a substantial drawback of questionable, or unknown security practices on the backend. As well as a substantial database breach risk.
- Currently available opensource and locally hosted providers like keepassxc lack proper local/global infrastructure for flexible workflows.
- This lack of convenience on the open source side is likely to lead people into very fast and loose practices such as uploading keyfiles in places they shouldn't be, placing databases in uncessary levels of risk. Providing improved usability will allow individuals to practice better operational security.
- Develop and expand terminology and syntax to better describe the architectures.

### Current architecture focus and design goals:

- Keyfiles provide additional security at low overhead, however they remain inconvenient, potentially catastrophic, and a redundant security measure if not properly implemented.
- Remain hardware key agnostic, hardware keys are expensive. proprietary, and singular points of failure. Prefer open source, easily reproducible, and generally accessible solutions.
- Managing KBDX databases across multiple machines, and even through the internet via tools like rsync, and eventually git integration for version control.
- Develop a variety of architectures to best provide for the needs of anybody wishing to use this project.
- Using existing technology and software such as LUKs/LVM in order to provide additional security. 

### Terminology:

- UnauthorizedSystem: A system not controlled nor vetted by the end user, should be avoided at all costs, however the architecture should still be designed in a way to mitigate potential leaks and vulnerabilities via separation of secrets, tiered encryption, and good opsec practices.
- AuthorizedSystem: A system controlled and vetted by the user (potential point of attack) Assumed to have disk encryption, or at least a secure encrypted partition specifically for any additional provided utility.
- KeyDrive: A usb drive, flashed with some combination of partitions, LVM, LUKs and storing secrets used for authing, Private keys, SSH keys, password manager databases, keyfiles, anything of the sort.
- SecureTunnel: A secure transport through the internet, or some other form of IO such as USB. Using SSH as a backbone for support, and security.
- AuthServer: Future LAN git integration for providing access to files. and version control through a centralized git service hosted by the user. (in order to reduce attack surface area, never connect it to the broader internet)
- DB: Password Manager database, in this case a kbdx file, for keepassxc.
- Store: A Store is a analagous to a partition, or logical volume, within the contents of this project, Store naming is arbitrary and has no specific syntaxing. Just follow good naming etiquette.
- Architecture Naming: The syntax is started with a "prefix-ident", currently `!` `?` and `#` are accepted, `!` being unencrypted data, `?` being encrypted data, and `#` being a placeholder intended to demonstrate syntax, or as a wildcard for other "prefix-idents". The syntax is expanded further based on "key-idents" which serve to differentiate individual keys, `#1...9` currently only 1-9 are accepted, 0 is reserved for the DB. delineation of the syntaxing is accomplished via inserting a single hyphen between the prefix-ident, key-ident (if present), and the Store name. Complete syntaxing is as follows using a demonstration: `!-keyfile ?1-secrets ?2-supersecrets #-generic` where the keyfile is unencrypted, the secrets, and supersecrets are encrypted using distinct keys. And the generic Store, has no explicit configuration. The intention of this syntax documenation is to allow people to cleanly and explicitly generate architectures of their own.

### Future design goals, and project ambitions:

- Develop a working proof of concept KeyDrive, to demonstrate the architecture. 
- Provide automation in the form of scripting to make generation of generic keyfiles and KeyDrives easy.
- Automated interactions on the side of the KeyDrive, as well as AuthorizedSystems via Daemons.
- The architecture should be designed in such a way that it doesn't leave any traces of itself on UnauthorzedSystems, private/public computers or ephemeral distributions like tails.
- The AuthorizedSystem should check to ensure that the drive hasn't been tampered with in any manner, nor corrupted. (architecture dependent as fully encrypted architectures are extremely unlikely to have this issue)
- Any network interaction required should be conducted over secure, encrypted ssh tunnels, or through other known secure means, via file encryption, Using the KeyDrive itself to authenticate between AuthorizedSystems. (known as a SecureTunnel)

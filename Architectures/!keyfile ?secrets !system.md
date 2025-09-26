# Unencrypted keyfile plus encrypted secrets storage

Unencrypted keyfile stored in plaintext in a clean partition, with an additional partition providing access to encrypted secrets.

### Pros:
- easily implemented: unencrypted keyfile makes for easy deployment and usage, just plug in the drive, and point your DB to the keyfile.
- additional security at low cost: Provides a simple multifactor auth for your db, without being a secret by itself.
- provides an option to store encrypted secrets such as the DB authorized behind the password manager itself.

### Cons:
- Losing the keyfile completely means the DB is inaccessible.
- Doesn't protect the DB on the machine.
- If you do not have access to the drive, you cannot use your password manager.
- Backups of the keyfile negate MFA functionality.
- DB is locked behind the DB itself.

### Overall rating: 2/10

It's better than no security, provides moderate increase in complexity, but lacks sufficient design criteria to make it substantially more secure in the face of attacks.

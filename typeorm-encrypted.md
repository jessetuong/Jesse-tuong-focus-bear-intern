# typeorm-encrypted — Reflection

## Why double encrypt instead of relying on database encryption alone
- Encryption at rest only protects the data when the database engine is off — a stolen
disk or a raw backup file. While Postgres is running and a connection is authenticated,
at-rest encryption doesn't work.
- Field-level encryption keeps the sensitive columns as ciphertext inside the live
database, so an attacker who reaches the data still needs the application's encryption
key, which is generated stored outside the database.

## How typeorm-encrypted integrates with TypeORM entities
- It uses TypeORM's column `transformer` hook. You attach an EncryptionTransformer to a
@Column; TypeORM runs to() (encrypt) before every insert/update and from()
(decrypt) after every select. 
- Services and repositories are unchanged — the entity
property is always plaintext in JS and ciphertext in the column. The cost: ciphertext
is non-deterministic, so you cannot filter, sort, index, or enforce uniqueness on an
encrypted column.

## Best practices for managing encryption keys
- Use a random 32-byte key for AES-256-GCM.
- Put it in .env and ever commit it
- Keep it in a secrets manager (AWS KMS / Secrets Manager, Vault, Doppler) and inject
  it as a runtime env var; validate its presence at boot and fail closed if missing.
- Use a separate key per environment and restrict who can read the secret.

## Trade-offs: database-level vs application-level encryption

- Database-level encryption (at rest / TDE) is free and invisible — queries and indexes work normally, no real overhead. But it only protects a stolen disk or backup; anyone with a live DB connection (leaked creds, injection, dumps) still sees plaintext.

- Application-level encryption (typeorm-encrypted) keeps the data as ciphertext everywhere except inside the app, with the key stored separately from the database — so it survives a database compromise. The cost: you can't filter, sort, or index encrypted columns, values are larger, raw SQL debugging shows nothing useful, and you have to manage the key and its rotation.
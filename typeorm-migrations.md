1. Purpose of database migrations in TypeORM

Migrations let you evolve your database schema (add/remove tables, columns, indexes) in controlled, incremental, repeatable steps
Each migration is a script with an up() method (apply the change) and down() method (revert it), so schema changes are explicit and reversible
Keeps every environment (local, staging, production) on the exact same schema by running the same migration files, instead of manually editing tables

2. Migrations vs. seeding

Migrations: change the database structure — creating tables, adding columns, changing types, adding constraints
Seeding: inserts data into an already-existing structure — e.g., default roles, test users, sample records
Migrations must run first to create the schema; seeding then populates it. They solve different problems and shouldn't be mixed into the same script

3. Why version-controlling schema changes matters

Makes schema history traceable — you can see exactly when and why a column was added, alongside the code change that needed it
Lets every team member and every environment apply the same, ordered set of changes, avoiding "works on my machine" schema drift
Enables safe rollbacks if a change causes problems, since each change is a discrete, reversible unit
Required for CI/CD pipelines to apply schema changes automatically and consistently during deployment

4. Rolling back a migration

npx typeorm migration:revert
This runs the most recently applied migration's down() method, undoing just that one change
Running it multiple times reverts migrations one at a time, in reverse order of application
Important: rollback only works cleanly if down() was written correctly to reverse up() — if down() is missing/incomplete, the rollback may not fully restore the previous schema, so it's worth writing and testing both directions when creating a migration
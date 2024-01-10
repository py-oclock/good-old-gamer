# Good Old Gamer

Ce projet est un site web pour les vieux joueurs qui n'ont plus le temps de perdre du temps

## PostgreSQL

### Création préalable de la BDD et de l'utilisateur associé à la BDD

`sudo -i -u postgres psql` - pour entrer en mode commande SQL

`CREATE ROLE nomDeLutilisateur WITH LOGIN PASSWORD CREATEDB 'leMotDePasse';`

Ne pas oublier le rôle `CREATEDB` sinon l'utilisateur ne pourra pas push les schéma de BDD avec PRISMA.

## Dépendances

Les dépendances suivantes sont nécessaires pour exécuter ce projet :

- Nest.js - framework pour la création de l'API
- PRISMA - ORM
- bcrypt - pour le hash et la vérification des mots de passes

## Nest.js

### Installation

`npm i -g @nestjs/cli` (A faire une seul fois si le CLI de Nest n'est pas installé de manière global sur la machine)

`nest new project-name`

### Création de la partie authentification

`npm install --save @nestjs/passport passport passport-local`

#### Ajout du module et du service d'Auth

`nest g module auth`

`nest g service auth`

#### Ajout du module et du service User

`nest g module users`

`nest g service users`

## PRISMA

### Installation de base

`npm install prisma --save-dev`

### Fichier schema.prisma contenant les schéma de BDD

```ts
model User {
  id    Int     @id @default(autoincrement())
  email String  @unique
  name  String?
  posts Post[]
}

model Post {
  id        Int     @id @default(autoincrement())
  title     String
  content   String?
  published Boolean @default(false)
  author    User    @relation(fields: [authorId], references: [id])
  authorId  Int
}
```

### Création de la migration une fois les schéma définis

`npx prisma migrate dev --name init`

### Installation du client PRISMA pour manipuler la BDD depuis le code

`npm install @prisma/client`

## bcrypt

### Installation

`npm install bcrypt`

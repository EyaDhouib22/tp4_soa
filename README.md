# TP4 : Introduction à gRPC

**Matière:** SoA et Microservices
**Enseignant:** Dr. Salah Gontara
**Classe:** 4Info
**Année Universitaire:** 2024/2025

## Description du Projet

Ce projet de Travaux Pratiques (TP4) a pour but d'introduire les concepts et l'utilisation de gRPC (Google Remote Procedure Call). Il s'agit d'un framework RPC moderne, open source et haute performance qui peut s'exécuter dans n'importe quel environnement. Il permet de connecter des services de manière efficace, en utilisant Protocol Buffers (Protobuf) comme langage de définition d'interface et comme format d'échange de messages.

L'objectif principal est de mettre en place un service gRPC simple en Node.js, de définir sa structure de communication avec Protobuf, et de le tester.

## Objectifs Pédagogiques

*   Comprendre le rôle et les avantages de gRPC dans une architecture microservices.
*   Apprendre à définir des services et des messages en utilisant Protocol Buffers (.proto).
*   Implémenter un serveur gRPC en Node.js.
*   Tester un service gRPC en utilisant un client (comme Postman).
*   (Objectif étendu) Comprendre le concept d'un reverse proxy pour exposer des services gRPC.

## Outils Utilisés

*   **Node.js:** Environnement d'exécution JavaScript côté serveur.
*   **npm:** Gestionnaire de paquets pour Node.js.
*   **Protocol Buffers (protobuf):** Mécanisme extensible de sérialisation de données structurées.
*   **gRPC:** Framework RPC.
    *   `@grpc/grpc-js`: Bibliothèque gRPC pour Node.js.
    *   `@grpc/proto-loader`: Utilitaire pour charger dynamiquement les fichiers `.proto` en Node.js.
*   **Postman:** Outil de test d'API (avec support gRPC).

## Prérequis

Avant de commencer, assurez-vous d'avoir installé les outils suivants sur votre système :
1.  **Node.js et npm:** À télécharger depuis le site officiel de Node.js.
2.  **Le compilateur Protocol Buffers (`protoc`):** À installer depuis le site officiel de Protobuf et à ajouter au PATH de votre système. Sur Ubuntu, la commande `sudo snap install protobuf --classic` peut être utilisée.

## Étapes de Réalisation

### 1. Configuration de l'Environnement

*   Créez un répertoire pour le projet (par exemple, `grpc-tp`).
*   Naviguez dans ce répertoire via votre terminal.
*   Initialisez un nouveau projet Node.js avec la commande `npm init` (vous pouvez utiliser l'option `-y` pour accepter les valeurs par défaut).
*   Installez les dépendances gRPC nécessaires pour Node.js via npm : `@grpc/grpc-js` et `@grpc/proto-loader`.

### 2. Définition du Service avec Protocol Buffers

*   Créez un fichier avec l'extension `.proto` (par exemple, `hello.proto`).
*   Dans ce fichier, définissez la syntaxe `proto3`.
*   Déclarez un `package` pour votre service.
*   Définissez un `service` (par exemple, `Greeter`) avec une ou plusieurs méthodes RPC. Chaque méthode spécifiera son message de requête et son message de réponse.
*   Définissez les structures des messages (`message`) pour les requêtes (par exemple, `HelloRequest` avec un champ `name`) et les réponses (par exemple, `HelloReply` avec un champ `message`).

### 3. Implémentation du Serveur gRPC

*   Créez un fichier JavaScript pour le serveur (par exemple, `server.js`).
*   Importez les modules nécessaires : `grpc` (`@grpc/grpc-js`), `protoLoader` (`@grpc/proto-loader`), et `path`.
*   Chargez la définition du service à partir de votre fichier `.proto` en utilisant `protoLoader.loadSync()` et `grpc.loadPackageDefinition()`.
*   Implémentez la logique métier pour chaque méthode RPC définie dans votre service. Cette fonction recevra l'objet `call` (contenant la requête) et un `callback` pour renvoyer la réponse ou une erreur.
*   Créez une instance du serveur gRPC (`new grpc.Server()`).
*   Ajoutez votre service implémenté au serveur (`server.addService()`).
*   Liez le serveur à une adresse IP et un port (par exemple, `0.0.0.0:50051`) en utilisant `server.bindAsync()` avec des identifiants de serveur non sécurisés (`grpc.ServerCredentials.createInsecure()`).
*   Démarrez le serveur gRPC (`server.start()`) une fois la liaison réussie. Affichez un message de confirmation dans la console.

### 4. Démarrage du Serveur

*   Exécutez votre fichier serveur Node.js depuis le terminal (par exemple, `node server.js`).
*   Vérifiez que le message indiquant que le serveur a démarré s'affiche correctement.

### 5. Test du Service gRPC avec Postman

*   Ouvrez l'application Postman.
*   Créez une nouvelle requête de type "gRPC Request".
*   Entrez l'URL du serveur (par exemple, `localhost:50051`).
*   Importez votre fichier `.proto` dans Postman pour qu'il puisse comprendre la structure du service.
*   Sélectionnez le service et la méthode que vous souhaitez appeler (par exemple, `Greeter` et `SayHello`).
*   Remplissez le message de requête au format JSON (par exemple, `{"name": "MonNom"}`).
*   Envoyez la requête ("Invoke").
*   Vérifiez la réponse reçue du serveur.

## Conclusion

À la fin de ce TP, vous devriez avoir une compréhension fonctionnelle de la mise en place d'un service gRPC simple, de la définition de son contrat avec Protobuf, et de la manière de l'exécuter et de le tester.

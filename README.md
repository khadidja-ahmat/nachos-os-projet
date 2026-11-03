# Nachos : appels système, threads et mémoire paginée (C++)

Projet du cours de **Systèmes d'Exploitation** (M1 Informatique, Université de Bordeaux, 2025), réalisé en binôme.

[Nachos](https://en.wikipedia.org/wiki/Not_Another_Completely_Heuristic_Operating_System) est un mini système d'exploitation **simulé** (processeur MIPS émulé) écrit en C++. Le cours consiste à y ajouter, étape par étape, des briques d'un vrai système.

> Ce dépôt ne contient **pas** le code : il présente le travail réalisé. Le code de base de Nachos appartient à l'Université de Californie et à l'équipe enseignante, et les sujets du cours ne sont pas publics.

## Ce que j'ai réalisé

### Devoir 1 : entrées/sorties
- Pilote de console (`ConsoleDriver`) avec synchronisation entre le noyau et les interruptions du simulateur.
- Appels système `PutChar`, `GetChar`, `PutString`, `GetString`, `PutInt`, `GetInt`.
- Copie sécurisée de chaînes entre la mémoire du programme utilisateur (MIPS) et le noyau, y compris pour les chaînes longues.
- `printf` côté utilisateur (via `vsprintf`, sans appel système supplémentaire).

### Devoir 2 : multithreading
- Appels système `ThreadCreate` et `ThreadExit` : création de threads utilisateur propulsés par des threads noyau (`do_ThreadCreate`, `StartUserThread`, `do_ThreadExit`).
- Initialisation du contexte MIPS du nouveau thread (registres, pointeur de pile).
- Allocation dynamique des piles des threads avec un `BitMap` (`AllocateUserStack`).
- Verrous sur la console pour éviter les affichages mélangés entre threads.
- Compteur de threads par espace d'adressage et terminaison propre du processus.
- Programmes de test : `makethreads`, `twothreads_print`, `threadexit_test`, `manythreads`.

### Devoir 3 : pagination et processus
- Traduction d'adresses par table des pages ; chargement du programme via la table (`ReadAtVirtual`).
- `PageProvider` : allocation et libération des pages physiques.
- Appel système `ForkExec` : lancement de plusieurs processus.
- `Exit` : le simulateur ne s'arrête que quand le dernier processus se termine ; la fin d'un thread principal termine tous les threads de son processus.
- Mini-**shell** utilisateur : il affiche une invite `nachos>`, lit une commande et lance le programme correspondant avec `ForkExec` ; la commande `exit` quitte.
- Vérification avec **Valgrind** (pas de fuite mémoire).

## Compétences mises en œuvre

C++ · programmation système · appels système · threads et synchronisation (verrous) · gestion mémoire (pagination) · processus · débogage (gdb, Valgrind) · Git.


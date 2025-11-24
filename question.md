

Ahnou Mehdi  
BTS2

                        
   
                                                 Question TP

# **📊 1\. Sécurité et RGPD**

## **Q1.1 : Pourquoi est-il important de stocker les clés API dans un fichier `.env` et pas directement dans le code ?**

* Le code source peut être partagé, publié ou versionné (ex. GitHub).

* Une clé API dans le code pourrait être volée et utilisée par un tiers → risques financiers, juridiques, de sécurité.

* Le fichier `.env` est exclu du versioning (via `.gitignore`) et permet de séparer *configuration sensible* et *code*.  
   ➡️ **Protection des secrets**, bonne pratique DevOps/Sécurité.

---

## **Q1.2 : Quelles données personnelles sont collectées par notre agent ? Est-ce conforme au principe de minimisation du RGPD ?**

* L’agent collecte principalement : **la ville demandée**, éventuellement **le texte entré par l'utilisateur**.

* Pas de nom, email, IP (sauf éventuellement côté serveur), ni autre donnée inutile.  
   ➡️ Oui, c’est **conforme au principe de minimisation** : seules les données strictement nécessaires au fonctionnement sont utilisées.

---

## **Q1.3 : Que se passerait-il si on stockait l'historique des conversations ? Quelles obligations RGPD s'appliqueraient ?**

Si l’historique est enregistré, l’application devient un **traitement de données personnelles**.  
 Il faudrait alors :

* Définir une **finalité** précise (ex : améliorer le service).

* Informer l’utilisateur (transparence).

* Justifier une **base légale** (souvent : consentement).

* Permettre :

  * droit d’accès

  * droit de suppression

  * droit de rectification

* Définir une **durée de conservation limitée**.

* Assurer la **sécurité** (chiffrement, contrôle d’accès).

---

# **🛡️ 2\. Conception conforme CNIL**

## **Q2.1 : Citez 3 recommandations de la CNIL que nous avons appliquées dans ce TP.**

Exemples valables :

* Transparence sur l’utilisation d’un agent conversationnel.

* Minimisation des données collectées.

* Pas de conservation des conversations.

* Affichage clair du rôle du bot.

* Utilisation sécurisée d'une API avec clés protégées.

---

## **Q2.2 : Comment l’utilisateur est-il informé qu’il parle à un robot ? Pourquoi est-ce important ?**

* L’interface indique explicitement que la réponse provient d’un **agent** ou d’un **assistant automatisé**.

* Important car :

  * évite la confusion humain/IA (principe de transparence).

  * respecte les recommandations CNIL.

  * permet à l’utilisateur d’adapter son niveau de confiance.

  * prévention des risques de manipulation ou mauvaise interprétation.

---

## **Q2.3 : Proposez une amélioration pour ajouter une "supervision humaine" comme recommandé par la CNIL.**

Quelques options possibles :

* Ajouter un bouton **“Contacter un humain”** qui transfère la demande à un opérateur.

* Mettre en place une revue humaine des réponses problématiques (ex : escalade automatique si l’IA ne comprend pas).

* Ajouter un mode “validation humaine” où un agent humain peut vérifier certaines réponses sensibles.

---

# **🧠 3\. Technique**

## **Q3.1 : Expliquez le rôle de Mistral AI dans notre application.**

* Mistral est le **modèle de langage** utilisé pour :

  * comprendre les questions de l’utilisateur,

  * extraire des informations (ex : la ville),

  * formuler les réponses,

  * interpréter le contexte conversationnel.  
     ➡️ C’est le "cerveau" de l'agent conversationnel.

---

## **Q3.2 : Pourquoi utilise-t-on `response_format={"type": "json_object"}` dans la fonction `extraire_ville()` ?**

* Pour **forcer le modèle** à retourner une sortie JSON structurée.

* Cela évite les variations de texte naturelles d’un LLM.

* Permet d’obtenir **directement une valeur exploitable en Python** (ex : `{ "ville": "Paris" }`).  
   ➡️ Plus fiable, plus robuste, plus facile à traiter.

---

## **Q3.3 : Comment pourrait-on gérer plusieurs langues dans l’agent conversationnel ?**

Plusieurs approches possibles :

1. **Détection automatique de la langue**

   * Utiliser un modèle (ou un prompt) pour identifier la langue de la requête.

   * Répondre dans la même langue.

2. **Prompt multilingue**

   * Indiquer au modèle : *"Comprends et réponds dans la langue de l'utilisateur."*

3. **Modèles ou fichiers de localisation**

   * Préparer des textes d’interface dans plusieurs langues (i18n).

4. **Utilisation d’un modèle multilingue** (Mistral, GPT, Llama, etc.)

   * Qui comprend et génère plusieurs langues nativement.

                                             
---
editor_options: 
  markdown: 
    wrap: 72
---

# Guide d'annotation

Pour chaque rapport de patient fourni, l'objectif est d'extraire des
informations sur tous les médicaments qui sont connus pour être pris par
le patient ou liés à lui, différents attributs des médicaments et la
temporalité en relation ou non avec les médicaments..

L'ensemble de la tâche d'annotation sera centrée sur les médicaments
mais l'ensemble des concepts suivant doit être annoté ou corrigé (à
partir de la préannotation) dans le document :

-   Médicament ou Classe de médicament : **drug**, **ATC**

-   Dose : **dose** (en relation ou non avec un médicament)

-   Fréquence : **freq** (en relation ou non avec un médicament)

-   Durée : **duration** (en relation ou non avec un médicament)

-   Voie d'administration : **route** (en relation ou non avec un
    médicament)

-   Condition : **condition** (en relation ou non avec un médicament)

-   Date : **date** (en relation ou non avec un médicament)

Le deuxième objectif est d'extraire les relations entre ces annotations
et les médicaments, l'ensemble des relations suivantes nécessite d'être
annoté :

-   start : entre une **date** et un **drug** ou **ATC**

-   stop ente une **date** et **drug** ou **ATC**

-   duration_presc : entre une **duration** et **drug** ou **ATC**

-   duration_admin : entre une **duration** et **drug** ou **ATC** IV

-   refer_to : entre une **dose**, une **route**, une **freq** ou une
    **condition** et un **drug** ou **ATC**

Le dernier objectif est d'extraire les relations temporelle : arrivé à
replacer les entité temporelle les unes par rapport aux autres si elles
sont relatives. <!--# Vraimen t? peut-être utopique -->

Si une entité est disjointe, la relation : **same_ent** doit être
utilisé entre les deux parties de l'entité. Si un médicament est répété
plus loin dans le texte sans notion du nom ou de la classe, une relation
**coref** doit être utilisée.

Chaque médicaments ne peut avoir au maximum qu'une seule de ces lignes.
S'il est nécessaire de dupliquer le lignes, il est nécessaire d'annoter
deux médicaments différents même si ça correspond au même token. Voir
exemple [Exemple 1 :]

| A annoté               | Class d'annotation | Relation avec le médicaments | exemple                     |
|-----------------|-----------------|---------------------|-----------------|
| médicaments            | drugs/ATC          |                              | arimidex/corticoide         |
| Dose                   | dose               | refer_to                     | 1 G de doliprane            |
| Fréquence              | freq               | refer_to                     | 3 cp/jour                   |
| Voie d'administration  | route              | refer_to                     | en intraveineuse            |
| Durée d'administration | duration           | duration_admin               | 1L de serum phy pendant 5h  |
| Durée de prescription  | duration           | duration_presc               | arimidex pendant 5 ans      |
| Date de début          | DATE               | start                        | dès ce jour                 |
| Date de fin            | DATE               | stop                         | arrêt le 4 juin             |
| Date non spécifié      | DATE               | refer_to                     | il y a environ 3-4 semaines |

Si un médicament est modifier à une dates, il est nécessaire d'annoté
plusieurs fois le médicaments.

Événement : "event" : "start", "stop", "start-stop", "increase",
"decrease", "continue", "switch" Prescription : "drug_blob", "ordo_blob"

Les annotations doivent être faites même s'il y a des fautes
d'orthographe, sauf si ces fautes d'orthographe peuvent induire une
confusion.

### Exemple 1 :

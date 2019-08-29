class: center, middle

# Ansible

---
# Au menu

--
<ol>
    <li>Introduction</li>
    <ul>
      <li>Un outil de provisionning</li>
      <li>Pourquoi Ansible ?</li>
      <li>Comment ça marche ?</li>
    </ul>
    <br>
<!---
--
    <li>Vagrant</li>
    <ul>
        <li>Présentation de l'outil</li>
        <li>Création de notre terrain de jeu</li>
    </ul>
    <br> 
-->
--
    <li>Hosts, Groups et ligne de commande</li>
    <ul>
        <li>Création du fichier host</li>
        <li>Variabilisation des hosts et groupes</li>
        <li>Premières actions à la ligne de commande</li>
    </ul>
    <br>
--
    <li>Configurer Ansible</li>
    <ul>
        <li>Niveaux de conf</li>
        <li>confs principales</li>
    </ul>
    <br>
--
    <li>Playbooks et Tasks</li>
    <ul>
        <li>Création des Playbooks</li>
        <li>Agencement des tâches et pré-tâches</li>
    </ul>
    <br>
--
    <li>Roles</li>
    <ul>
        <li>Création des tâches</li>
        <li>Fichiers et templates</li>
        <li>Variables par défaut</li>
    </ul>
</ol>

---

# Introduction

* Ansible, un outil de provisionning

* Pourquoi Ansible ?

* Comment ça marche ?


---
# Ansible, un outil de provisionning

* Créé par Michael DeHaan (Cobbler) (v1.0 2012)

* Est aujourd’hui sous la responsabilité de RedHat (Octobre 2015)

* Open Source : les sources sont disponibles sur GitHub.

* Nom inspiré d'un outil de communication supraluminique dans le livre de SF Rocannon's World de Ursula K. Le Guin

* Agit sur des machines déjà existantes afin de les **configurer**

* Similaire à Puppet ou Chef par exemple -> _Config Management_

* Différent de Terraform -> _Orchestration Management_  
    (vont provisionner les serveurs eux-mêmes)

* !! Ansible peut faire de l'Orchestration, mais ce n'est pas son rôle premier (Notamment pour Docker)


---

# Pourquoi Ansible

* Idempotence de la plupart des modules sur la plupart des plateformes (Linux, Windows, Mac, BSD)

* Ne nécessite qu'une connexion ssh et Python sur la machine distante. Pas d'agent à installer partout. Limite les risques de sécurité.

* Pas besoin d'expérience de développement (même si ça aide...)

* Permet d'avoir très rapidement un aperçu de l'infrastructure via les playbooks

* Possible d'écrire ses propres modules (dans la plupart des langages de scripting: bash, perl, ruby...)


---

# Comment ça marche ?

* Génère un script python avec l'ensemble des commandes à effectuer

* Se connecte aux machines via SSH et dépose ce script dans les fichiers temporaires

* Exécute et monitore le déroulement du script


<!-- 
---
# Vagrant ?
-->

--- 

# Hosts, Groups et ligne de commande

* Le fichier inventaire

* Variabilisation des hosts et groups

* Premières actions à la ligne de commande


---

# Le fichier inventaire
## Référencer les machines

* Sert simplement à signaler à Ansible les machines sur lesquelles agir -> hosts.

* Existe deux formats: ini et yaml

* permet d'associer des variables à chaque host.

* permet de regrouper les hosts en groupe, en fonction de leurs affinités.
* Les groupes peuvent être regroupés en groupes.

* des variables peuvent aussi être appliquées au niveau du groupe

---
Exemple tiré de la documentation Ansible

```yml
all:
  hosts:
    mail.example.com:
  children:
    webservers:
      hosts:
        foo.example.com:
        bar.example.com:
    dbservers:
      hosts:
        one.example.com:
        two.example.com:
        three.example.com:
    east:
      hosts:
        foo.example.com:
        one.example.com:
        two.example.com:
    west:
      hosts:
        bar.example.com:
        three.example.com:
    prod:
      children:
        east:
    test:
      children:
        west:
```

---

# Variabilisation des hosts et groupes

* Directement dans le fichier d'inventaire

* Dans un répertoire dédié: host_vars ou group_vars

---

    <li>Playbooks et Tasks</li>
    <ul>
        <li>Création des Playbooks</li>
        <li>Agencement des tâches et pré-tâches</li>
    </ul>
    <br>

    ---
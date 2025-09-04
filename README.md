# Projet Ansible

Ce dépôt contient une configuration Ansible simple permettant de démarrer et arrêter des services/applications sur des hôtes définis dans un inventaire.

---

## Contenu

```
.
├── ansible.cfg         # Configuration Ansible
├── inventory.ini       # Inventaire des hôtes (groupes et IPs)
├── start.yml           # Playbook pour démarrer les services
└── stop.yml            # Playbook pour arrêter les services
```

---

## Prérequis

- **Ansible** installé (≥ 2.14 recommandé).
- Accès SSH fonctionnel aux hôtes de `inventory.ini`.
- Clés SSH configurées (de préférence sans mot de passe pour automatiser).

Vérifiez l’installation :
```bash
ansible --version
```

---

## Inventaire

Le fichier `inventory.ini` contient la liste des hôtes et leurs groupes. Exemple :

```ini
[serveurs]
192.168.1.10 ansible_user=ubuntu
192.168.1.11 ansible_user=ubuntu
```

Vous pouvez définir plusieurs groupes, par exemple `db`, `web`, etc.

Tester la connexion SSH :
```bash
ansible all -i inventory.ini -m ping
```

---

## Fichiers principaux

### 1) `ansible.cfg`
Fichier de configuration Ansible.

### 2) `start.yml`
Playbook qui exécute les tâches de démarrage (par ex. lancement de conteneurs, services, VM).

### 3) `stop.yml`
Playbook qui exécute les tâches d’arrêt.

---

## Exemple de workflow

1. **Vérifier les hôtes**
   ```bash
   ansible all -i inventory.ini -m ping
   ```

2. **Démarrer les services**
   ```bash
   ansible-playbook -i inventory.ini start.yml
   ```

3. **Arrêter les services**
   ```bash
   ansible-playbook -i inventory.ini stop.yml
   ```

---

## Débogage

- Ajouter `-vvv` à vos commandes pour plus de détails :
  ```bash
  ansible-playbook -i inventory.ini start.yml -vvv
  ```
- Vérifier la connectivité SSH et les permissions utilisateur.

## Ressources utiles

- [Documentation officielle Ansible](https://docs.ansible.com/)


## 1. Accès Initial & Ouverture de Session
- **Artefact analysé :** `Security.evtx`
- **Event ID :** `4624` (Ouverture de session réussie)
- **Horodatage (UTC) :** `27/03/2023 14:37:09`
- **Utilisateur :** `DESKTOP-887GK2L\CyberJunkie`
- **Type d'ouverture de session :** `2` (Connexion interactive locale)
- **Analyse :** Cet événement marque le début de l'activité de l'utilisateur sur le poste et sert de référence temporelle (*timeline*) pour le reste de l'investigation.
## 2. Altération des Règles du Pare-feu Windows
- **Artefact analysé :** `Microsoft-Windows-Windows Firewall With Advanced Security%4Firewall.evtx`
- **Event ID :** `2004` (Une règle a été ajoutée à la liste des exceptions du Pare-feu Windows)
- **Horodatage (UTC) :** `27/03/2023 14:44:43`
- **Nom de la règle :** `Metasploit C2 Bypass`
- **Direction :** `Outbound` (Sortante)
- **Action / Protocole :** Autoriser (`Allow`) sur `TCP`
- **Analyse :** L'utilisateur a créé une règle sortante explicite pour laisser passer un trafic de commande et contrôle (C2) Metasploit sans blocage du pare-feu local.
## 3. Modification de la Politique d'Audit Système
- **Artefact analysé :** `Security.evtx`
- **Event ID :** `4719` (La stratégie d'audit système a été modifiée)
- **Catégorie / Sous-catégorie :** `Object Access` / `Other Object Access Events`
- **Modification appliquée :** `Success Added`
- **Impact technique :** Cette sous-catégorie contrôle la journalisation des opérations liées aux tâches planifiées (*Scheduled Tasks*). L'activation de l'audit des succès permet désormais de tracer la création ou la modification de tâches planifiées dans le journal `Security.evtx`.
- ## 4. Persistance via Tâche Planifiée
- **Artefact analysé :** `Security.evtx`
- **Event ID :** `4698` (Une tâche planifiée a été créée)
- **Nom de la tâche :** `HTB-AUTOMATION`
- **Chemin du fichier exécuté :** `C:\Users\CyberJunkie\Desktop\Automation-HTB.ps1`
- **Arguments :** `-A cyberjunkie@hackthebox.eu`
- **Analyse :** L'utilisateur a mis en place une persistance quotidienne exécutant un script PowerShell depuis son Bureau avec une adresse e-mail en argument. Cela permet d'identifier le fichier à isoler/analyser et l'entrée à nettoyer lors de la remédiation.

# Sherlock : LogJammer (Hack The Box)

## Résumé de l'incident
Investigation des journaux d'événements Windows (`.evtx`) du poste `DESKTOP-887GK2L` suite à des soupçons d'actions malveillantes effectuées par l'utilisateur `CyberJunkie`.

## Chronologie des faits (Timeline)
| Heure (UTC) | Source / Event ID | Description |
| :--- | :--- | :--- |
| `27/03/2023 14:37:09` | `Security.evtx` (4624) | Connexion interactive locale réussie de `CyberJunkie` (Logon Type 2). |

| `27/03/2023 14:44:43` | `Firewall.evtx` (2004) | Ajout de la règle sortante (`Outbound`) nommée `Metasploit C2 Bypass`. |

| `27/03/2023` | `Security.evtx` (4719) | Modification de la politique d'audit : activation de `Success Added` sur `Other Object Access Events`. |

| `27/03/2023` | `Security.evtx` (4698) | Création de la tâche planifiée `HTB-AUTOMATION` exécutant `Automation-HTB.ps1` avec l'argument `-A cyberjunkie@hackthebox.eu`. |b

| `27/03/2023` | `Windows Defender.evtx` (1117) | Détection de `SharpHound-v1.1.0.zip` dans `Downloads` et mise en quarantaine (`Quarantine`) par Defender. |

| `27/03/2023 14:58:33` | `PowerShell%4Operational.evtx` (4103) | Exécution de `Get-FileHash -Algorithm md5 .\Desktop\Automation-HTB.ps1` par `CyberJunkie`. |

| `27/03/2023` | `System.evtx` (104) | Effacement du journal `Microsoft-Windows-Windows Firewall With Advanced Security/Firewall`. |

## Conclusion & Recommandations de Remédiation
1. **Confinement & Nettoyage :** Supprimer la règle de pare-feu sortante `Metasploit C2 Bypass` ainsi que la tâche planifiée `HTB-AUTOMATION`.
2. **Analyse de Malware :** Isoler le script `C:\Users\CyberJunkie\Desktop\Automation-HTB.ps1` et vérifier l'isolation effective de `SharpHound-v1.1.0.zip` en quarantaine.
3. **Sécurisation des Journaux :** Centraliser les journaux `.evtx` en temps réel vers un SIEM afin d'empêcher la perte de preuves lors d'un effacement local (Event ID `104` / `1102`).

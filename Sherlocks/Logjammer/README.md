# Sherlock : LogJammer (Hack The Box)

## Résumé de l'incident
Investigation des journaux d'événements Windows (`.evtx`) du poste `DESKTOP-887GK2L` suite à des soupçons d'actions malveillantes effectuées par l'utilisateur `CyberJunkie`.

## Chronologie des faits (Timeline)
| Heure (UTC) | Source / Event ID | Description |
| :--- | :--- | :--- |
| `27/03/2023 14:37:09` | `Security.evtx` (4624) | Connexion interactive locale réussie de `CyberJunkie` (Logon Type 2). |

| `27/03/2023 14:44:43` | `Firewall.evtx` (2004) | Ajout de la règle sortante (`Outbound`) nommée `Metasploit C2 Bypass`. |

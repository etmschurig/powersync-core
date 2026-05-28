# ETM PowerSync — Core

> Cœur open source du HEMS ETM PowerSync — gestion d'énergie locale (surplus solaire,
> délestage, API) bâtie sur [nymea.io](https://nymea.io).

ETM PowerSync est un **HEMS** (Home Energy Management System) qui coordonne photovoltaïque,
batterie, pompe à chaleur et borne de recharge sous une seule logique d'optimisation —
exécutée **en local**, sur votre matériel, sans dépendance cloud obligatoire.

Ce dépôt contient la couche ETM open source bâtie au-dessus de nymea.io, ainsi que le
connecteur GPL (`optimizer-plugin`) vers la logique d'optimisation. Cette logique métier
elle-même (`powersync-optimizer`) est propriétaire et n'est pas distribuée ici — voir
l'architecture ci-dessous.

## Architecture

```
nymea (plateforme IoT, GPL3)
└─ powersync-core / plugins (GPL3)        ← tout ce qui est lié à nymea
   └─ optimizer-plugin (GPL3)             ← connecteur nymea, relaie via socket Unix
        ⇅  socket Unix (IPC)              ← frontière de licence
      powersync-optimizer (propriétaire)  ← logique métier : arbitrage, Predict AI (non public)
```
## Installation

Via le dépôt APT signé ETM :

```bash
curl -fsSL https://repos.etm-powersync.fr/key.gpg | sudo gpg --dearmor -o /usr/share/keyrings/etm.gpg
echo "deb [signed-by=/usr/share/keyrings/etm.gpg] https://repos.etm-powersync.fr stable main" | sudo tee /etc/apt/sources.list.d/etm.list
sudo apt update && sudo apt install powersync-community
```

Voir la [documentation complète](https://docs.etm-powersync.fr) pour la configuration.

## Statut

Projet en développement actif. L'état réel de chaque fonction (Supporté / Partiel / Roadmap)
est indiqué dans la [documentation des fonctionnalités](https://docs.etm-powersync.fr).

## Licence

[GNU General Public License v3.0](LICENSE) — © ETM-Schurig.

## Liens

- Documentation : https://docs.etm-powersync.fr
- Site produit : https://etm-powersync.fr
- Plugins d'équipements : https://github.com/etmschurig/powersync-plugins

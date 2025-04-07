# 🗺️ API Distance IGN - Calculs d’Itinéraires et Routes Proches

Ce projet Python utilise les services de l’IGN (Institut national de l'information géographique et forestière) pour identifier les routes les plus proches d’un point géographique et calculer des itinéraires optimaux pour les piétons entre plusieurs points.

## 📌 Objectif

Fournir des outils permettant :
- D’extraire les routes les plus proches d’un point via un service WFS.
- De calculer un itinéraire piéton entre deux points à l’aide de l’API de calcul d’itinéraire IGN.
- D’explorer toutes les combinaisons d’itinéraires entre routes proches autour de deux points.

## ⚙️ Fonctionnalités

### 1. `trouver_routes_proches(point, bbox_size, url_base, couche, nombre_routes=5)`
Identifie les routes les plus proches d’un point géographique donné en interrogeant une couche géospatiale via WFS.

- 📥 Entrées : coordonnées du point, taille de la bbox, URL WFS, nom de la couche, nombre de routes à retourner.
- 📤 Sortie : `DataFrame` contenant les routes les plus proches, distances, coordonnées en WGS84.
- ⚠️ Gère les erreurs de requêtes.

### 2. `calculer_itineraire_et_distance(point_depart, point_arrivee)`
Calcule l’itinéraire piéton entre deux points géographiques à l’aide du service IGN.

- 📥 Entrées : latitude/longitude du départ et de l’arrivée.
- 📤 Sortie : tuple contenant les données JSON, la distance, et la géométrie (GeoJSON).
- ⚠️ Gère les erreurs réseau ou réponse invalide.

### 3. `obtenir_combinaisons_itineraires(point_depart, point_arrivee, bbox_size, url_base, couche, nombre_routes=5)`
Génère toutes les combinaisons possibles d’itinéraires entre les routes proches autour du point de départ et d’arrivée.

- 📥 Entrées : points de départ/arrivée, bbox, WFS URL et couche, nombre de routes proches.
- 📤 Sortie : `DataFrame` des itinéraires avec distances et géométries.
- 🔁 Utilise les deux fonctions précédentes.

## 🔧 Technologies

- Python 3
- `requests`, `geopandas`, `shapely`, `heapq`, `pandas`
- Services IGN : API Itinéraire + WFS (Web Feature Service)

## 🧪 Exécution & Tests

Tu peux tester les fonctions dans le notebook en changeant :
- Les coordonnées (`point_depart`, `point_arrivee`)
- Les paramètres de la couche et du service IGN

Assure-toi que :
- Les URLs IGN sont accessibles
- Le service WFS retourne bien des données (vérifier les permissions/couche)

## ❗ Limitations

- Optimisé pour les itinéraires piétons uniquement.
- Les performances peuvent être limitées si trop de combinaisons sont générées (grand `nombre_routes`).
- Dépendance forte à la disponibilité des services IGN.

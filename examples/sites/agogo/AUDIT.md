# Agogo Store: refonte de la page d'accueil

Source : capture d'écran de https://agogostore.net/ (octobre 2026) et catalogue réel
(MCP Agogo Store : 6 catégories, 12 produits actifs). Le site n'était pas joignable
depuis la session, donc aucun autre contenu n'a été lu.

## Diagnostic de la page actuelle

| # | Sévérité | Constat | Correction appliquée |
|---|----------|---------|----------------------|
| 1 | Critique | Bouton orange "Shop now" avec texte blanc, environ 3.0:1 (couleur estimée depuis la capture), sous le seuil AA de 4.5:1 | Orange d'action approfondi en #B83C0B (5.69:1). L'orange vif reste dans le logo uniquement |
| 2 | Critique | Trois widgets flottants (Ask Agogo AI, WhatsApp, bulle violette) recouvrent l'image du hero et se concurrencent | Retirés du premier écran. Une section "Not sure where to start?" intègre l'assistant IA (en tête) et WhatsApp (en second) |
| 3 | Majeur | Environ 400px de vide au-dessus du titre : le message principal commence à mi-écran | Hero resserré, titre en haut, preuve sociale juste sous les boutons |
| 4 | Majeur | Aucun produit visible au premier écran d'une boutique ; photo d'ambiance générique | Produit vedette (Beauty Glow, prix, note, lien) dans le hero |
| 5 | Majeur | Navigation : 2 catégories sur 6 (Beauty, Wellness) | Les 6 catégories réelles + New + Bestsellers, défilement horizontal sur mobile |
| 6 | Majeur | Deux boutons de même poids (Shop now, Explore collections) | Un seul bouton principal, l'action secondaire devient un lien |
| 7 | Mineur | "Shop all" orange isolé à droite de la nav, cloche de notifications sans valeur sur l'accueil | "Shop everything" dans la grille des catégories, cloche supprimée, bascule clair/sombre ajoutée |
| 8 | Mineur | Badge panier "31" qui déborde de l'icône | Compteur à taille fixe, annoncé aux lecteurs d'écran |

## Structure de la nouvelle page

1. En-tête : logo, recherche centrale, thème, compte, favoris, panier ; 6 catégories.
2. Hero : titre conservé ("Beauty that moves with you"), un bouton principal, produit vedette.
3. Catégories : Wellness en tuile principale, cinq tuiles secondaires, "Shop everything".
4. Bestsellers : 8 vrais produits, filtres fonctionnels, ajout au panier et favoris.
5. Rituels : matin, après-midi, soir avec les trois bundles du catalogue.
6. Aide : assistant IA avec validation et exemples, WhatsApp et suivi de commande.
7. Pied de page.

## À brancher côté production

- Les URL (`/category/...`, `/product/<slug>`, `/assistant`, `/whatsapp`) suivent les slugs
  du catalogue mais doivent être alignées sur les routes réelles.
- Les visuels produits sont des packshots SVG en attendant les vraies photos détourées.
- Les catégories Skincare, Makeup et Haircare n'ont aucun produit actif dans le catalogue :
  à approvisionner, ou à masquer de la nav tant qu'elles sont vides.

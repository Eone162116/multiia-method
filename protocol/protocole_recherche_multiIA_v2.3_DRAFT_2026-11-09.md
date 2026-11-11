# Protocole de recherche empirique assistée multi-IA — v2.3 DRAFT (proposition du 09/11/2026, non gelée)

**v1.0 formalisée le 28/07/2026 à partir du programme MaNGA n_g / ISF. v2.0 le même jour. v2.1 le 31/08/2026 après B2 et l'exécution initiale de C1–C3. v2.2 FINAL le 31/08/2026 après réconciliation F12 : C1–C3 régénérés par les scripts canoniques réellement exécutés, 195 MAPS hachés, manifeste exécutable validé sans erreur ; artefact prereg original non retrouvé et conservé comme exception permanente de provenance.**

**Statut : version finale opérationnelle avec exception de provenance documentée. Le verdict scientifique B2 reste fermé. Le paquet C1–C3 est reproductible et archivé (`EXECUTION_PASS_PREREG_MISSING`) ; le prereg original n'est pas vérifiable par hash et cette absence ne doit jamais être requalifiée en provenance complète. Domaine de validité : tout projet scientifique disposant d'un vérificateur exogène.**

> **Changement v2.1 → v2.2 FINAL.** L'audit post-exécution a découvert F12, puis la réconciliation a été menée jusqu'au bout : C3 a été rejoué sur la branche primaire `f_coh=0.3`, C1 a été rendu déterministe, C2 a été consolidé en script canonique intégrant les hotfixes réellement nécessaires, et l'ensemble C1–C3 a été régénéré. Le manifeste final a haché 16 artefacts sources, 16 copies archivées et les 195 MAPS, avec zéro erreur de validation. Le seul défaut résiduel est l'absence du prereg original attendu sous le préfixe SHA256 `2a64a52a…`; cette perte est conservée explicitement comme exception de provenance, sans reconstruction fictive. F11 et le renforcement de P9 sont conservés.

> **Changement v2.2 FINAL → v2.3 DRAFT (09/11/2026, proposition non gelée, soumise à l'approbation de l'auteur).** (a) Fusion de l'amendement du 29/07/2026, rédigé après le test de transférabilité sur les vitesses radiales, marqué « à fusionner » et jamais intégré : théorème central raffiné (vérificateur exact, exogène et **accessible**), principes P10 et P11, mode d'échec F14 (l'« F11 » de cet amendement, renommé car F11 désigne ici le pivot post-null), cas d'usage §7bis, items 16–17 de la checklist et ajout aux limites. (b) Ajout de F13 (vérificateur endogène ou benchmark circulaire), identifié le 31/08/2026 sur le premier benchmark CMS, après la v2.2. (c) Mise à jour de la note de provenance du prereg des contrôles (voir §5, « Mise à jour de provenance »). (d) Ajout de F15 et F16 (échecs de la vérification des références, audit du 09/11/2026) et de l'item 19 de la checklist. (e) 11/11/2026 : troisième occurrence de F16 ajoutée (références GWOSC).

---

## 0. Théorème central du protocole

> **La valeur d'un cycle de travail assisté par IA est entièrement déterminée par la qualité du vérificateur exogène disponible.**

Là où existe un vérificateur exact, bon marché et indépendant des modèles (données réelles, CrossRef/ADS, un mock passé par le code identique, une compilation, une mesure), le cycle multi-IA est un amplificateur de productivité. Là où le vérificateur est absent (théorie spéculative, esthétique conceptuelle), le même cycle devient un amplificateur de complaisance : les modèles convergent entre eux et produisent une cohérence interne qui **ressemble** à une validation sans en être une. Le premier acte de tout nouveau projet est donc d'identifier le vérificateur, pas la question.

**Corollaire (consensus LLM ≠ validation).** L'accord de N modèles sur un point n'a aucun poids probatoire. Il localise au mieux ce qui est plausible dans la littérature d'entraînement, c'est-à-dire précisément ce qu'un projet original cherche à dépasser.

> **Raffinement (v2.3, issu de l'amendement du 29/07/2026).** Le vérificateur doit être exact, exogène **et accessible**. Une vérité-terrain pristine adossée à des données non archivées proprement est un vérificateur défaillant. Le test de transférabilité sur les vitesses radiales l'a établi frontalement : la cible fantôme initiale, α Cen Bb, avait une vérité-terrain très probablement négative (le signal de 3,24 j provient presque certainement de la fonction de fenêtre des données ; Rajpaul et al. 2016), mais son jeu de données canonique n'était récupérable par aucune route automatique, et une reconstruction a échoué à une porte de fidélité fixée a priori (rms 12 contre 1,5 m/s, piège F9). La cible a dû pivoter vers HD 41248, dont le dépôt CDS obligatoire (Faria et al. 2020) fournissait les vitesses radiales, les indicateurs d'activité et une conclusion publiée (les variations s'expliquent par l'activité stellaire, sans preuve suffisante d'une planète, le modèle GP étant préféré par l'évidence bayésienne). Cette conclusion est une préférence de modèle, non une preuve d'absence. **Corollaire de sélection de cible : viser d'abord les cas à données déposées avec indicateurs, pas les cas iconiques.**

---

## 1. Architecture des rôles

Le workflow sépare quatre fonctions et les attribue à des agents distincts pour créer une friction adversariale structurelle :

**Synthèse / garde-fou / rédaction** — maintient l'état du projet, rédige, tient le registre des risques, refuse le poids institutionnel au spéculatif. C'est aussi le rôle qui exécute le code contre les données réelles quand l'environnement le permet.

**Calcul formel** — dérivations, vérifications algébriques, stabilité. Ses sorties sont des conjectures tant qu'elles ne sont pas recoupées.

**Arbitre externe** — relit les manuscrits et verdicts comme un referee. Ses audits sont traités comme des rapports de referee : triés, pas obéis (mode d'échec F7, « audit sur-calibré »).

**Critique adversariale** — cherche activement la faille, la lecture triviale, l'explication instrumentale. Son succès se mesure au nombre de résultats qu'il tue.

Règle de rotation : aucun agent ne valide sa propre production. Une dérivation du calculateur est auditée par l'arbitre ; une rédaction du synthétiseur est attaquée par le critique. **Aucune de ces quatre fonctions ne constitue le vérificateur** : elles génèrent et filtrent, la validation vient toujours de l'extérieur de la boucle.

---

## 2. Les onze principes

**P1 — Séparation génération/validation.** Les analogies séduisantes, intuitions infalsifiables et cadres spéculatifs appartiennent à la couche générative. Poids institutionnel nul (aucune tâche, aucune entrée de registre) tant qu'une structure falsifiable complète n'existe pas : observable X, prédiction Y, jeu de données Z, critère de rejet W.

**P2 — Vérification exogène obligatoire.** Toute référence bibliographique passe par CrossRef/ADS avant d'entrer dans un .bib. Tout résultat numérique est régénérable depuis les données brutes. Toute affirmation attribuée à une source est vérifiée contre la source, pas contre le souvenir qu'en a un modèle.

**P3 — Reproductibilité exécutable un-jeu-un-script-une-table (renforcé, v2.2).** Une valeur « gelée » qui ne peut pas être régénérée par le script canonique est disqualifiée, quelle que soit sa place dans le manuscrit. Le gel se fait par artefacts réellement exécutés : données/CSV d'entrée + script exact + ligne de commande + environnement minimal + hash des entrées et du code + table de sortie. **Le code canonique est le code qui a réellement tourné**, pas une version antérieure « équivalente » ni une version nettoyée après coup. Tout hotfix d'I/O ou de logique crée une nouvelle version à regeler. Avant dépôt, le paquet gelé est ré-exécuté ; la table publiée doit être régénérée selon une règle de reproduction fixée (égalité exacte quand déterministe, ou tolérance pré-spécifiée si une composante numérique ne peut pas être bitwise). Les bootstraps destinés à une table gelée utilisent un RNG explicitement seedé.

**P4 — Portes d'intégrité pré-enregistrées.** Tout portage, refactoring ou réimplémentation d'un pipeline passe une porte quantitative définie AVANT exécution (ex. : Spearman ≥ 0,995 et médiane |Δ| ≤ 0,02 contre le CSV gelé). Idem pour les décisions scientifiques : critères go/no-go écrits, datés et hachés avant de voir les résultats.

**P5 — Validation d'estimateur sur mocks à code identique.** Aucun estimateur n'est interprété avant d'avoir été passé sur (a) du bruit pur et (b) un signal nul structuré, **à travers le chemin de code strictement identique** à celui des données réelles. Un estimateur censuré (clipping, sélection de bins valides) est présumé coupable tant que le mock bruit-pur n'a pas montré ce qu'il fabrique tout seul.

**P6 — Test de dégénérescence joint, pas budget canal-par-canal.** Un budget de systématiques assemblé canal par canal peut être globalement faux même si chaque canal est correctement quantifié isolément, parce que le terme dominant peut être une interaction non énumérée. Le remède : construire un modèle avancé **sans signal intrinsèque**, le contraindre sur des observables autres que la statistique d'intérêt, et demander ce qu'il prédit pour elle. Si la prédiction reproduit l'observation, l'amplitude est dégénérée — quelle que soit la propreté du budget.

**P7 — Statistiques appariées.** Une statistique dont l'amplitude est saturée par les systématiques reste utilisable si on l'apparie à une seconde statistique répondant aux mêmes nuisances avec une sensibilité différente. L'objet informatif est alors la paire (exclusion par l'absurde : le réglage de nuisance qui explique l'une prédit une valeur exclue pour l'autre).

**P8 — La rétractation est un résultat.** Un claim retiré après validation sur mock, avec le cadre qui a forcé le retrait, est publié comme résultat méthodologique. Le versionnage rhétorique (incrémenter vX.Y sans nouvelle contrainte exogène) est un mode d'échec, pas un progrès.

**P9 — Règle d'arrêt pré-engagée (renforcé, v2.1).** Le pré-enregistrement d'un test doit fixer, avant exécution, non seulement les critères de survie/rejet mais aussi **ce qui se passe en cas de zone grise, et le fait qu'aucune statistique supplémentaire ne sera essayée quelle que soit l'issue**. Sans cette clause, une zone grise déclenche mécaniquement la recherche d'une N+1ᵉ sonde, qui est le moteur même du garden of forking paths (F6). La discipline consiste à honorer un seuil fixé d'avance même quand la donnée « frôle » : un excès positif dans toutes les configurations mais sous le seuil d'amplitude pré-engagé est une **non-détection**, pas une détection faible. Déplacer le poteau après avoir vu le ballon est la faute que P9 interdit.

Après qu'un critère de clôture a été satisfait, **les contrôles déjà gelés sont dus et passent avant toute nouvelle proposition de test**. Un test nouveau, même techniquement excellent, ne devient pas admissible parce qu'il est présenté comme « décisif », « plus robuste » ou « pré-enregistrable ». Toute étude ultérieure d'injection–récupération, de sensibilité ou de calibrabilité de l'estimateur est une **caractérisation méthodologique bornée** : son interprétation doit être écrite avant exécution de façon que ni une faible ni une forte sensibilité ne puisse réactiver le claim astrophysique fermé. Cette clause de non-résurrection vise F11.


**P10 — Calibration des seuils par cible (nouveau, v2.3).** Les seuils de décision (survie/rejet) d'une statistique dépendante du rapport signal/bruit ne se transfèrent pas d'une cible de référence à une autre : un seuil calibré sur une cible propre (S/N élevé) est trop exigeant sur une cible bruitée. Ils se calibrent **par cible**, par injection-récupération sur le bruit et l'échantillonnage propres de chaque cible. Normaliser en z-score par le nul de chaque cible ne suffit pas : la normalisation agit sur le dénominateur (dispersion du nul), pas sur le numérateur (force du signal), qui dépend du S/N. *Preuve dans le test RV : le seuil z_haut = 12,58 calibré sur le contrôle brillant (e_RV 0,39 m/s) déclassait à tort une injection identique dans une cible bruitée (e_RV 1,32 m/s) ; recalibré par cible, l'injection est correctement récupérée.*

**P11 — La statistique de décision doit épouser le mécanisme de nuisance (nouveau, v2.3).** En régime dominé par une nuisance structurée (activité stellaire, systématique cohérente), une statistique de « puissance résiduelle après nul » ne reproduit pas une rejection par comparaison de modèles, même quand le nul écrase la nuisance : il subsiste un résidu cohérent que la puissance lit comme signal, alors qu'une comparaison d'évidence bayésienne (modèle avec/sans la composante d'intérêt) le pénalise correctement. Le choix de la statistique n'est pas un détail d'implémentation tractable : c'est une décision de fond, à pré-enregistrer, et **tout surrogate tractable doit être validé comme suffisant sur le mécanisme visé avant d'être adopté**. *Preuve dans le test RV : après un nul GP écrasant la rotation d'un facteur 40, la puissance GLS résiduelle laissait le fantôme en zone grise (z = 5,5) là où Faria et al. 2020 préfèrent, par évidence bayésienne, le modèle d'activité à celui d'une planète.*

---

## 3. Cycle opérationnel

**Phase 0 — Cadrage.** Identifier le vérificateur exogène (théorème central). Formuler la question en structure X-Y-Z-W. Si W (critère de rejet) ne peut pas être écrit, le sujet reste en couche générative et le cycle s'arrête ici.

**Phase 1 — Gel.** Pipeline canonique + échantillon gelé + CSV de référence + porte d'intégrité. Documenter l'origine de chaque choix d'échantillon (F9).

**Phase 2 — Mesure fiducielle.** Une statistique, un script, une table. Aucune interprétation avant Phase 3.

**Phase 3 — Batterie de robustesse.** Stratifications (avec corrélations partielles contrôlant la structure d'échantillon — jamais de stratification brute interprétée seule), observations répétées pour l'erreur empirique par objet, mocks bruit-pur et signal-nul (P5), scan de sensibilité des choix analytiques.

**Phase 4 — Dégénérescence jointe (P6/P7).** Modèle nul contraint sur observables indépendantes ; identification d'une seconde sonde ; verdict : amplitude dégénérée / excès survivant / paire contraignante. **Cette phase est pré-enregistrée (P4) avec sa règle d'arrêt (P9) avant tout run.** Si le verdict ferme le claim, les contrôles accompagnants déjà gelés sont exécutés dans l'ordre prévu ; aucun nouveau contrôle ne s'intercale entre le verdict et leur exécution.

**Phase 5 — Verdict et registre.** Trois issues, toutes consignées : résultat survivant (→ manuscrit de détection), rétractation ou non-détection (→ manuscrit de méthode, P8), indéterminé sous critère de levée explicite. Chaque verdict entre dans la mémoire institutionnelle avec ses fichiers. Après clôture, une nouvelle étude ne peut être ajoutée au même claim que si son rôle est explicitement distinct (caractérisation, réplication, transfert) et si une clause de non-résurrection est gelée avant le run.

**Phase 6 — Intégrité éditoriale et reproductibilité exécutable.** Audit bibliographique complet contre ADS/CrossRef ; vérification claim-par-claim ; audit fichier-par-fichier du dépôt public (F10) ; **audit exécutable du paquet scientifique (F12)**. Pour chaque table publiée : enregistrer le script exact exécuté, sa ligne de commande, les hashes des entrées, les versions minimales de l'environnement, la sortie et son hash. Rejouer le script archivé dans un répertoire propre et vérifier qu'il régénère la table selon la règle P3. Un dépôt n'est pas déclaré propre parce que les noms sont corrects : il l'est seulement si le chemin archivé reproduit effectivement les nombres publiés. Toute divergence runtime/source est versionnée dans un CHANGELOG et réconciliée avant le gel final. DAS avec DOI de concept, jamais de version.

Le cycle est itératif : tout résultat de Phase 4 qui invalide une hypothèse de Phase 2 renvoie en Phase 2 avec un nouveau gel, jamais avec une retouche du gel existant. Une clôture sous P9 n'est pas un simple point de passage : elle change le statut du claim. Revenir dessus exige un nouveau projet explicitement distinct, pas une continuation implicite.

---

## 4. Mémoire institutionnelle

Deux registres, alimentés en continu et sans demander :
— **Gestionnaire de tâches** : verdicts scientifiques, tests en attente avec leurs critères pré-enregistrés, blocages. Une idée non adoptée ne crée pas de tâche ; un commentaire sur tâche existante vaut mieux qu'une tâche nouvelle.
— **Base documentaire** : états de manuscrits, décisions stratégiques, audits.

Règle de provenance : avant de demander à l'humain de confirmer un fait, une intention ou l'origine d'une décision, chercher d'abord dans l'historique des sessions. La recherche **localise** l'origine d'un fait ; elle ne le **valide** jamais (validation exogène, P2). Motif documenté : des éléments attribués à l'humain se sont révélés issus de sessions IA antérieures, y compris des références confabulées.

---

## 5. Catalogue des modes d'échec observés

**F1 — Confabulation de références avec leurs claims.** Références plausibles (auteur réel, revue réelle, volume inventé) générées en rédaction de Discussion, puis attribuées par tous à l'humain. Pire que la référence fausse : le claim attaché était lui aussi fabriqué. Contre-mesure : P2 + Phase 6 + règle de provenance.

**F2 — Artefact / dégénérescence observationnelle déguisé en signal (trois occurrences).** Un estimateur clippant les valeurs négatives, combiné à des erreurs croissant radialement, peut fabriquer un gradient positif sur du bruit pur ; un forward model incomplet peut en outre laisser croire qu'une correction partielle suffit. Occurrence 1 : échelle harmonique, gradient médian +1,5 à +1,9, excès « ×3,5 » cru pendant des semaines. Occurrence 2 : \(n_g\), où une baseline \(s_{in}=0\) produit \(n_g^{out}=+0,752\) contre \(+0,766\) observé ; les contrôles C1–C3 montrent que cette dégénérescence ne dépend pas finement de \(A\), sans démontrer une équivalence stricte galaxie-par-galaxie. Occurrence 3 (28/07) : l'estimateur log-log de la pente m≥3 produit **+1,82 sur du bruit pur** dans la géométrie réelle, tuant le « +1,50 » qui en était issu. Contre-mesure : P5 pour les estimateurs, P6 pour les dégénérescences jointes, et distinction explicite entre « amplitude reproduite » et « équivalence objet par objet ».

**F3 — Stratification en résolution sur-interprétée dans les deux sens.** Une première stratification brute en \(R_e/\mathrm{PSF}\) semblait prouver une origine instrumentale ; la corrélation partielle contrôlant redshift et masse l'avait réduite, montrant qu'une stratification brute peut être un confound d'échantillon. Le run C3 exécuté le 31/08 sur la branche **secondaire** \(f_{coh}=0.7\) a produit \(D_{obs}=+0.576\) et \(D_{mock}=+0.517\), tous deux à IC95 positif. **Ce nombre mock reste provisoire pour le paquet confirmatoire tant que la branche primaire f_coh=0.3 n'a pas été exécutée/réconciliée.** Leçon inchangée : une tendance en résolution ne reçoit aucune étiquette causale par défaut. Contre-mesure : Phase 3 pour les confounds + Phase 4 pour le forward model complet + P3/F12 pour vérifier que la branche publiée est bien celle pré-engagée.

**F4 — Budget de systématiques juste canal par canal, faux au total.** Le terme dominant peut être une interaction non énumérée. Dans le cas \(n_g\), le mock rotation-only donnait \(+0,11\), tandis qu'une baseline structurée \(s_{in}=0\) passée par le même opérateur observationnel produit une sortie de l'ordre de \(+0,75\). Le ratio ~6,8 est descriptif, **pas un budget additif** : \(n_g\) n'est pas supposé se décomposer en contributions linéaires. Contre-mesure : P6.

**F5 — Contamination géométrique d'une sonde « propre ».** La sonde harmonique de secours était elle-même contaminée par le warp ; un modèle tilted-ring en a absorbé un quart. Contre-mesure : toute sonde de repli subit la totalité du cycle, pas une version allégée.

**F6 — Jardin des embranchements.** Le passage successif d'une statistique à une autre après échec de la précédente rend la p-value finale ininterprétable si la séquence n'est ni pré-enregistrée ni divulguée. Séquence réelle du projet : n_g → s_harm(m≥2) → s₃(m≥3). Contre-mesure : P4 + P9 + divulgation complète de la séquence dans le manuscrit.

**F7 — Boucle d'auto-validation multi-IA.** Des audits croisés entre modèles ont produit des verdicts convergents recyclant le propre registre de risques du projet, présentés comme découvertes externes ; un audit externe sur-calibré a inversement classé « FATAL » des points déjà maîtrisés. Contre-mesure : théorème central + tri des audits comme rapports de referee.

**F8 — Hygiène de données.** Fichiers dupliqués dans le répertoire de travail gonflant N silencieusement. Contre-mesure : déduplication par identifiant unique en tête de tout pipeline, N vérifié contre l'échantillon gelé.

**F9 — Provenance perdue des choix d'échantillon.** L'origine de la sélection s'est perdue entre sessions, créant un point bloquant éditorial (convenance vs critère caché). Contre-mesure : Phase 1, documentation d'origine au moment du gel.

**F10 — Défaut d'intégrité de dépôt public (v2.0).** Un fichier hérité, mal nommé et mal décrit, a été publié dans une archive Zenodo avec DOI, décrivant comme « échantillon gelé » une sortie d'analyse superseded dont les statistiques contredisaient le résultat fiduciel. Public et indexé pendant six semaines. Contre-mesure : Phase 6 étendue à l'audit fichier-par-fichier de tout dépôt ; correction par version documentée (CHANGELOG, renommage explicite, jamais d'effacement).

**F11 — Pivot post-null déguisé en robustesse (nouveau, v2.1).** Après plusieurs tours où un arbitre externe avait correctement renforcé puis validé la clôture méthodologique, le même arbitre a proposé, un tour plus tard, un test d'injection–récupération entièrement nouveau et l'a qualifié de « décisif » et « plus important que C1–C3 ». Le test était méthodologiquement recevable en soi, mais orthogonal à la question déjà fermée par B2 : montrer qu'un gradient injecté est récupérable ne démontre pas que le signal observé exige ce gradient. Le danger venait du **timing et du rôle argumentatif**, pas de la qualité technique du test. Le track record de l'arbitre créait en outre une inertie d'autorité : la cohérence accumulée de la boucle ressemblait à une validation externe. Contre-mesure : P9 renforcé — exécuter d'abord les contrôles gelés ; toute étude ultérieure de sensibilité est bornée par une clause de non-résurrection et ne peut rouvrir le claim fermé.

**F12 — Code exécuté ≠ code gelé/haché (nouveau, v2.2).** Un résultat peut respecter ses seuils scientifiques tout en échouant à l'intégrité de provenance : le script effectivement exécuté diverge du script déclaré gelé, un hotfix runtime n'est pas archivé, une branche différente de celle pré-engagée est exécutée, ou une table contient des composantes stochastiques non reproductibles faute de seed explicite. Première occurrence documentée : paquet C1–C3 de \(n_g\). C2 avait nécessité un hotfix de déduplication ; les régressions secondaires, un nettoyage des sentinelles `drpall` ; C3 avait été exécuté initialement sur \(f_{coh}=0.7\) au lieu de la branche primaire \(f_{coh}=0.3\) ; C1 utilisait un bootstrap non explicitement seedé.

La réconciliation a ensuite été exécutée jusqu'au contrôle exécutable : C1 déterministe, C2 canonique, C3 primaire, 195 MAPS hachés, 16 artefacts sources et 16 copies archivées, zéro erreur de validation. Le statut final est `EXECUTION_PASS_PREREG_MISSING`, car l'artefact prereg original n'a pas été récupéré. **Distinct de F10** : F10 = mauvais fichier ou mauvaise description dans le dépôt ; F12 = le chemin exécutable archivé ne régénère pas les nombres ou sa provenance runtime est incomplète. Contre-mesure : P3 renforcé + Phase 6 exécutable + manifeste runtime + re-run propre avant dépôt + exception explicite lorsqu'un artefact historique manque.


**Mise à jour de provenance du prereg des contrôles (v2.3).** Le prereg original, déclaré introuvable à la v2.2 FINAL (31/08/2026, 17:04), a été retrouvé le même soir : les copies ont été créées à 18:24 et conservent leurs dates de modification d'origine (27/08/2026, 14:24 à 14:26), antérieures à la première sortie de C1 (31/08, 11:39). Son SHA256 complet, `2a64a52aa20fc92669681a182ad2f16325daf2c109f3e56886527e61bddc6104`, correspond au préfixe attendu `2a64a52a…` sur deux copies. L'archive finale compte 17 artefacts sources (les 16 de la v2.2 plus le prereg) et `STATUS = PASS`. L'exception permanente de provenance déclarée à la v2.2 est donc levée pour ce prereg ; les horodatages de fichiers soutiennent l'ordre prospectif sans le prouver, et la distinction avec F10 est inchangée. [À confirmer par l'auteur avant gel.]

**F13 — Vérificateur endogène ou benchmark circulaire (nouveau, v2.3).** Un benchmark dont la vérité nominale ou la règle d'admission des cas dépend du classifieur ou de la règle de décision qu'il est censé évaluer. Le premier benchmark CMS (31/08/2026) sélectionnait, avec le classifieur même de l'analyse, un cas positif donnant déjà SURVIVE, un cas nul rééchantillonné jusqu'à REJECT et un cas faible dosé pour donner GRAY : un 3/3 aurait mesuré l'auto-cohérence, non la transférabilité. Il a été arrêté avant analyse. Contre-mesure : le constructeur n'importe pas le noyau d'analyse, ne calcule pas la statistique de décision et ne rééchantillonne pas conditionnellement au verdict futur.

**F14 — Auto-diagnostic erroné appliqué sans test (nouveau, v2.3 ; « F11 » dans l'amendement du 29/07/2026).** Un diagnostic de faille (« le nul est trop serré, il faut marginaliser les hyperparamètres ») posé et appliqué sans le tester peut être faux et aggraver le problème. Dans le test RV, la marginalisation des hyperparamètres GP, prédite pour élargir le nul, l'a en fait **resserré** (le GP réajusté absorbe la structure propre de chaque mock), poussant le z du fantôme vers le haut au lieu du bas. Remède : tout correctif diagnostiqué est une hypothèse, testée en itération pré-enregistrée neuve, jamais appliquée comme évidente. C'est P4/P9 étendu au débogage méthodologique lui-même.


**F15 — Faux négatif du vérificateur par erreur d'agence (nouveau, v2.3).** Un DOI valide est déclaré irrésolvable parce qu'il a été interrogé auprès de la mauvaise agence d'enregistrement (par exemple un DOI DataCite interrogé chez CrossRef). Le 09/11/2026, le DOI du jeu de données GWOSC O4b (`10.7935/8emv-ag54`), déclaré irrésolvable par un audit antérieur, résolvait par trois voies indépendantes ; un assistant IA avait répété ce statut dans une tâche et une page d'état avant de le revérifier. Contre-mesure : déterminer d'abord l'agence (`doi.org/doiRA`), interroger cette agence, et confirmer par une seconde voie avant de déclarer un DOI cassé.

**F16 — Citation qui résout mais ne soutient pas son affirmation (nouveau, v2.3).** Le DOI existe, mais ses métadonnées diffèrent de la citation (titre, auteurs, année), ou l'affirmation attachée dépasse la conclusion de la source. Exemples du 09/11/2026 : l'entrée STScI/MAST des produits TESS (deux DOI qui résolvent mais désignent d'autres titres, auteurs et année, un troisième produit utilisé n'ayant aucun DOI) ; les verdicts de référence des fantômes RV, énoncés plus fort que Rajpaul et al. 2016 et Faria et al. 2020 (voir §7bis). Troisième occurrence le 11/11/2026 : les deux références GWOSC, que l'audit à l'origine de F15 n'avait vérifiées que pour la résolution, portaient « GWOSC » comme auteur et les titres des pages d'accueil, alors que DataCite enregistre les deux jeux de données sous les collaborations LIGO, KAGRA et Virgo avec d'autres titres ; l'article qui décrit la publication des données (arXiv:2605.27090) n'était pas cité. Contre-mesure : comparer champ par champ les métadonnées résolues à la citation, et l'affirmation à la conclusion de la source, pas seulement l'existence de la référence.

---

## 6. Gabarits réutilisables

### 6.1 Squelette de pré-enregistrement (P4/P9)

Rédiger, dater, hacher (SHA256) et consigner **avant tout contact avec les données** :

1. **Objet et motivation.** Pourquoi ce test ; quelle est la statistique vivante et son statut (brute ? mesurée par quel estimateur ?).
2. **Position dans la séquence.** Lister les statistiques déjà essayées et pourquoi celle-ci vient après (transparence F6).
3. **H₀ explicite.** Ce qu'un modèle nul reproduirait exactement.
4. **Statistique de décision** et son incertitude (bootstrap, N tirages).
5. **Pré-tests éliminatoires** bloquants : bruit pur (l'estimateur ne fabrique rien), correction de bruit re-dérivée pour les degrés de liberté du modèle, suffisance de l'échantillon, porte d'intégrité. Chacun avec son critère chiffré.
6. **Critères SURVIE / REJET / ZONE GRISE**, chiffrés, mutuellement exclusifs.
7. **Règle d'arrêt (P9)** : ce que déclenche la zone grise, l'engagement explicite qu'aucune statistique supplémentaire ne sera essayée, et l'ordre d'exécution des contrôles déjà gelés après le verdict.
8. **Contrôles accompagnants** : calibration, cohérence croisée, erreur empirique par objet, sensibilité aux choix. S'ils sont post-clôture, préciser qu'ils peuvent renforcer, affaiblir ou borner l'interprétation méthodologique sans réactiver le claim fermé.
9. **Divulgation** : ce que le manuscrit contiendra quelle que soit l'issue.
10. **Ce que le test ne protège pas** : biais amont, exhaustivité de la famille de mocks.
11. **Clause de non-résurrection si post-clôture** : si le test caractérise un estimateur après fermeture du claim, écrire avant le run pourquoi aucune branche du résultat ne pourra réactiver ce claim.

Toute révision post-gel est versionnée (addendum daté), justifiée, et divulguée.

### 6.2 Recette de validation d'estimateur (P5)

Avant d'interpréter tout estimateur sur données réelles :
- **E1 bruit pur** : champ = bruit apparié aux erreurs observées, aucune structure, code identique. Critère : |médiane| sous un seuil ET IC contenant 0 ; OU l'estimateur n'est défini que pour une fraction négligeable d'objets (auquel cas il ne fabrique par construction aucune pente).
- **E2 correction de biais re-dérivée** : toute correction analytique de bruit est vérifiée par Monte-Carlo dans la géométrie exacte, même chemin d'ajustement ; se méfier des facteurs 2 et des degrés de liberté consommés par le modèle.
- **Estimateur non censuré par défaut** : ajuster en espace linéaire plutôt qu'en log si le log impose d'écarter des valeurs (la censure est directionnelle). Remplacer la censure par un test d'identifiabilité sur l'amplitude (|A|/σ_A ≥ 2), qui ne porte pas sur le signe.
- **Estimateur de secours pré-spécifié** avec règle de bascule fondée sur un critère mesurable (ex. taux d'identifiabilité), fixée d'avance, indépendante du signe du résultat.

### 6.3 Matrice de décision de la dégénérescence (P6)

Construire un modèle nul sans signal intrinsèque, le contraindre sur des observables indépendantes, balayer sa famille de nuisance (amplitude × fraction cohérente). Lire Δ = réel − mock sur toute la grille :

| Observation sur la grille | Lecture |
|---|---|
| Δ ≤ 0 dans ≥ 1 config | l'amplitude est dégénérée → REJET |
| Δ > 0 partout, mais s'effondre vers 0 à la config conservatrice (mock entièrement cohérent) | dégénérée en pratique → non-détection |
| Δ > 0 partout, IC excluant 0 partout, amplitude ≥ seuil pré-engagé | excès survivant |
| entre les deux | ZONE GRISE → règle d'arrêt P9 |

La config conservatrice est celle où le mock est le plus proche d'une vraie structure astrophysique (cohérente), pas d'un bruit blanc. C'est elle qui décide, pas la config la plus favorable.

---

## 7. Cas d'usage complet : clôture m≥3 et arrêt du programme empirique (28/07/2026)

Déroulé qui a servi de première validation du protocole à lui-même.

**Contexte.** Quatre statistiques successives promettaient un signal : n_g (+0,766), s_harm(m≥2) (+2,6), s₃(m≥3) via log-log (+1,50). La théorie (ISF) était déjà écartée. Seul le +1,50 restait « vivant », mesuré la veille.

**Application.** (Phase 0) Vérificateur = les données MaNGA réelles + mocks à code identique. (P4/P9) Pré-enregistrement rédigé, haché (SHA256 `2a9062cb…`), horodaté avant tout run ; addendum v1.1 documentant trois corrections d'estimateur décidées avant les données réelles. (Porte d'intégrité) Médiane n_g recalculée = +0,7655 = valeur gelée : extraction fidèle. (E1) L'estimateur primaire non censuré ne fabrique rien sur bruit pur (1/195) ; le log-log clippé produit **+1,82 sur bruit pur** → le +1,50 est mort comme mesure log-log (F2, 3ᵉ occurrence). (Scan de dégénérescence) L'estimateur primaire donne Δs₃ > 0 dans les 20 configurations, mais l'amplitude minimale (+0,20) est sous le seuil pré-engagé (+0,30) et Δs₃ s'effondre à +0,22 avec IC contenant 0 à la config conservatrice (mock entièrement cohérent). Un champ radialement plat vu par l'instrument reproduit la pente.

**Verdict.** ZONE GRISE. Non-détection. La règle d'arrêt P9 interdit une cinquième statistique. Le programme empirique se clôt.

**Ce que le protocole a produit.** Pas de détection — mais pas de faux positif non plus, alors que quatre sondes successives y menaient. La sortie publiable est un papier de méthode : n_g montré dégénéré, trois rétractations avec leurs mocks, le cadre de forward-model degeneracy, le pré-enregistrement horodaté, une borne supérieure sur l'excès m≥3, et la recette de validation d'estimateur. **C'est la démonstration que le protocole fait ce pour quoi il existe : convertir un enthousiasme non fondé en résultat honnête.**

---

## 7bis. Cas d'usage de transférabilité (domaine RV, 28–29/07/2026)

*(Issu de l'amendement du 29/07/2026 ; chronologiquement antérieur au §8.)*

Première application à un domaine étranger au projet source, en mode réplication (checklist 15). **Dispositif.** Paire appariée à trois branches. Fantôme = HD 41248 (signal de 25,6 j attribué à la rotation ; conclusion publiée de Faria et al. 2020 : variations expliquées par l'activité stellaire, sans preuve suffisante d'une planète). Contrôle réel = HD 219134 b (transitant, vérité-terrain orthogonale par le transit). Contrôle synthétique = keplérienne injectée dans l'activité du fantôme. W : divergence vis-à-vis du verdict attendu sur au moins une branche ⇒ échec de transférabilité, publiable (P8 sur le protocole lui-même). **Déroulé.** Pré-enregistrement haché et addenda datés (pivot de cible, calibration des seuils) à chaque décision, avant les données ; portes d'intégrité passées (reproduction des signaux publiés depuis les jeux gelés) ; deux itérations pré-enregistrées. **Verdicts.** v1 (seuils transférés du contrôle, H0 à hyperparamètres fixes) : 1/3 (contrôle seul correct). v2 (seuils par cible, H0 marginalisé) : 2/3 (contrôle et injection corrects ; fantôme toujours en zone grise). Aucun seuil déplacé post hoc (P9 tenu). **Ce que le protocole a produit.** Pas la complétion 3/3, mais trois raffinements durables : P10, P11 et le démasquage par itération d'un auto-diagnostic faux (F14). La non-complétion à 2/3, avec chemin de résolution connu (statistique d'évidence), est le résultat de méthode ; la v3 (évidence par nested sampling) est spécifiée, non exécutée, et le test a été clos par décision humaine.

---

## 8. Deuxième cas : \(n_g\) — B2 fermé, C1–C3 réconciliés, exception de provenance prereg documentée (27–31/08/2026)

**Statut logique à distinguer.** Le verdict historique **B2 reste fermé** : le run principal a montré qu'une baseline ordinaire sans gradient intrinsèque positif peut atteindre le régime du signal observé. L'incident F12 ne l'a jamais rouvert. En revanche, la première déclaration « C1–C3 exécutés proprement et clôturés » était trop forte ; l'audit a détecté une déviation de branche C3 et une divergence entre code gelé et code réellement exécuté. Ces points ont depuis été réconciliés par rerun canonique.

**B2, résultat historique inchangé.** À \(A=1.144\), \(s_{in}=0,f_{coh}=0.3\) donne \(n_g^{out}=+0.752\) [IC95 ≈ +0.586,+0.923] contre \(+0.766\) observé ; \(f_{coh}=0.7\) donne +0.863. Plusieurs baselines \(s_{in}\le0\) franchissent le seuil B2. La conclusion reste une **non-séparabilité** de l'interprétation intrinsèque, pas un « instrument pur ».

**C1 — réconcilié et reproductible.** Le balayage en \(A\) a été régénéré avec bootstrap explicitement seedé. Les médianes sont identiques au run initial :
- \(A=1.0\) : +0.717 / +0.808 ;
- \(A=1.061\) : +0.732 / +0.819 ;
- \(A=1.144\) : +0.752 / +0.863.
Les deux critères C1 passent. Les IC95 sont désormais déterministes dans l'archive officielle.

**C2 — script canonique réconcilié.** Le rerun officiel intègre dans un seul artefact les hotfixes réellement nécessaires : quatre lignes dupliquées identiques sont collapsées explicitement, les sentinelles `drpall` sont nettoyées avant les régressions secondaires, et les RNG sont déterministes. Le rerun régénère :
- C2a primaire (\(f_{coh}=0.3\)) : \(\mathrm{median}(\Delta n_g)=+0.093970\), IC95 [−0.066478,+0.255219] ;
- C2b secondaire (\(f_{coh}=0.7\)) : +0.037175, IC95 [−0.202638,+0.149402].
Dans les deux cas : **offset médian non détecté, équivalence stricte ±0.10 non démontrée**, et critère d'insuffisance du forward model non déclenché. C2a reste compatible avec un excès apparié positif jusqu'à environ +0.25 au niveau de son IC95 ; le résultat ne doit donc jamais être résumé par « le mock reproduit chaque galaxie ».

**C3 — branche primaire réconciliée.** Le rerun officiel utilise \(f_{coh}=0.3\) comme branche primaire :
\[
D_{obs}=+0.576100,\qquad IC95=[+0.129771,+0.944107],
\]
\[
D_{mock,\,primary}=+0.539419,\qquad IC95=[+0.236584,+0.764644].
\]
La hiérarchie est donc établie côté observations et côté mock primaire. La branche secondaire \(f_{coh}=0.7\) confirme le même résultat avec \(D_{mock}=+0.517118\), IC95 [+0.260841,+0.790620]. Les différences \(D_{obs}-D_{mock}\) restent descriptives uniquement ; aucun test d'équivalence n'est introduit.

**Réconciliation exécutable P3/F12.** Le paquet final a été rejoué puis gelé. Le contrôle d'archive rapporte :
- statut `EXECUTION_PASS_PREREG_MISSING` ;
- 0 erreur de validation ;
- 16 artefacts sources hachés ;
- 16 copies d'archive hachées ;
- 195/195 MAPS identifiés et hachés ;
- scripts, entrées, sorties, logs et environnement consignés dans le manifeste final.

**Exception de provenance prereg.** L'artefact original `PREREG_baseline_L0_ng_v1.md`, attendu sous le préfixe SHA256 `2a64a52a…`, n'a pas été retrouvé après recherche locale par nom/hash et inspection de l'historique PowerShell. Il n'a pas été reconstruit ni remplacé par une copie ultérieure. La provenance complète du prereg original est donc **non vérifiable** et cette limite est permanente. Elle est distincte de la reproductibilité exécutable de C1–C3, désormais établie.

**Apport méthodologique F12.** Le protocole a capturé un défaut de sa propre application avant dépôt : une décision scientifique correcte ne garantit pas une archive correcte. F12 devient donc un mode d'échec institutionnel à part entière. Sa contre-mesure n'est pas une déclaration mais un re-run : le code archivé doit être celui qui a réellement tourné et doit régénérer les tables publiées. L'incident montre également qu'une provenance perdue ne doit jamais être « réparée » par reconstruction rétroactive.

**F11 reste inchangé.** Aucun C4 ni test d'injection–récupération n'a été utilisé pour résoudre F12. La correction a porté exclusivement sur l'exécution, la provenance et l'archive ; elle n'a pas déplacé la question scientifique après B2.

---

## 9. Checklist de transfert

1. Quel est le vérificateur exogène ? S'il n'existe pas : le projet reste génératif, pas de registre, pas de manuscrit.
2. La structure X-Y-Z-W est-elle écrite ? Le critère de rejet W est-il opposable ?
3. Le pipeline est-il gelé avec porte d'intégrité chiffrée avant toute variante ? Le hash correspond-il au **script réellement exécuté**, hotfixes inclus ?
4. L'origine de l'échantillon est-elle documentée le jour du gel ?
5. L'estimateur a-t-il tourné sur bruit pur et signal nul via le code identique (gabarit 6.2) ?
6. Chaque tendance de stratification a-t-elle sa corrélation partielle contre la structure d'échantillon ?
7. Existe-t-il un modèle nul contraint sur d'autres observables, balayé sur sa famille de nuisance (matrice 6.3), et lu à la config conservatrice ?
8. Existe-t-il une seconde sonde appariée ?
9. Le test est-il pré-enregistré avec sa règle d'arrêt P9 (gabarit 6.1), haché et horodaté avant les données ?
10. La séquence complète des sondes essayées est-elle consignée et destinée à divulgation ?
11. Chaque référence du .bib a-t-elle son bibcode vérifié ET son claim vérifié contre la source ? Chaque dépôt public est-il audité fichier par fichier (F10) ET rejoué comme paquet exécutable (F12) ?
12. Les verdicts sont-ils dans le registre avec fichiers et critères de levée ? Pour chaque table : script exact, commande, hashes d'entrées/sorties et environnement minimal sont-ils consignés ?
13. Après un verdict de clôture, tous les contrôles déjà gelés ont-ils été exécutés avant toute nouvelle proposition ? Toute caractérisation ultérieure possède-t-elle une clause de non-résurrection écrite avant le run ?
14. Le script archivé a-t-il été ré-exécuté dans un répertoire propre et a-t-il régénéré la table publiée selon la règle P3 ?
15. Mode « réplication » sur problème connu : W = valeur publiée ± incertitude ; bénéfice attendu = détecter les artefacts de la littérature elle-même (F2–F5 ne sont pas propres à un projet). Le protocole s'applique intégralement.
16. **Le vérificateur est-il accessible ?** Vérité-terrain propre ET données déposées en format lisible par machine, avec les observables de nuisance nécessaires (indicateurs d'activité pour un nul P6). Prioriser les cibles à dépôt propre sur les cibles iconiques.
17. **La statistique de décision épouse-t-elle le mécanisme de nuisance (P11), et ses seuils sont-ils calibrés par cible (P10) ?** Un surrogate tractable est-il validé comme suffisant sur le mécanisme visé avant adoption ?
18. **Le benchmark est-il construit sans aucun appel au classifieur évalué (F13) ?** Le constructeur importe-t-il le noyau d'analyse, calcule-t-il la statistique de décision ou rééchantillonne-t-il selon le verdict futur ?
19. **Les références sont-elles vérifiées contre la bonne agence et contre leur affirmation ?** Agence déterminée par `doi.org/doiRA`, confirmation par une seconde voie, comparaison champ par champ des métadonnées et de l'affirmation attachée à la conclusion de la source (F15, F16).

---

## 10. Limites du protocole

Il ne produit pas d'idées : la couche générative reste humaine + IA en mode libre, et c'est voulu. Il est coûteux : chaque résultat paie mocks, portes, sondes appariées et pré-enregistrements ; sur un problème à vérificateur trivial il est surdimensionné. Il ne protège pas contre un vérificateur lui-même biaisé (données d'archive à sélection amont : le biais traverse toutes les portes — cf. le confound de sélection résiduel du projet source, documenté mais non résolu). Enfin il dépend d'une discipline de registre que rien n'impose techniquement : le protocole tient tant que l'humain le tient.

La v2.1 ajoute une limite plus subtile : **l'autorité accumulée d'un arbitre utile peut elle-même devenir un risque**. Un modèle qui a eu raison cinq fois de suite n'acquiert aucun droit à déplacer la question au sixième tour. Le track record augmente la valeur de ses critiques futures comme hypothèses à examiner ; il n'augmente jamais leur poids probatoire. Le vérificateur exogène et les règles gelées restent au-dessus de l'arbitre.

Le 28/07 puis le 31/08 ont montré deux choses distinctes : le protocole peut tenir face à une zone grise et face à un pivot post-null séduisant ; mais il peut encore échouer sur la **provenance exécutable de ses propres artefacts**. F12 rappelle qu'une discipline de décision correcte ne dispense jamais d'une discipline d'archive correcte.


Le protocole ne garantit pas non plus qu'un surrogate tractable choisi pour le coût soit fidèle : il peut passer les portes d'intégrité (reproduire les signaux publiés) tout en échouant la décision (ne pas reproduire la rejection consensuelle), parce que intégrité ≠ décision. La parade est P11, mais elle déplace le coût vers la machinerie lourde (évidence), ce qui ramène à la tension de coût déjà décrite. *(Ajout v2.3, issu de l'amendement du 29/07/2026.)*

---

*v2.2 FINAL — le paquet C1–C3 a passé la réconciliation exécutable F12 avec zéro erreur et 195 MAPS hachés. Le prereg original reste introuvable : la version est donc finale avec exception permanente de provenance documentée, et non avec provenance prereg complète. La prochaine révision doit venir d'une application prospective à un domaine différent.*

*v2.3 DRAFT (09/11/2026) : fusion de l'amendement du 29/07, ajout de F13 et mise à jour de provenance. Proposition non gelée, soumise à l'approbation de l'auteur. La prochaine révision doit venir d'une application prospective à un domaine différent (HYDRO, wbt-gaia) ou de la première application où le vérificateur est absent.*

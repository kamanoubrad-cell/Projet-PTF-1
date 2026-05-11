# Portfolio Risk & Optimization Analysis

> Simulation et analyse du risque d'un portefeuille multi-actifs : VaR, Expected Shortfall, Ratio de Sharpe, Ratio de Sortino et Frontière Efficiente via simulation Monte Carlo.

---

## Contexte

Ce projet s'inscrit dans une démarche d'analyse quantitative du risque de portefeuille, proche des problématiques rencontrées en gestion des risques bancaires (reporting NPL, pilotage du coût du risque).

L'objectif est double :
- **Mesurer le risque** d'un portefeuille via des indicateurs standards (VaR, ES, Sortino)
- **Optimiser l'allocation** des actifs pour maximiser le rendement ajusté au risque (Sharpe)

---

## Composition du portefeuille

| Actif | Ticker | Pondération initiale | Secteur |
|---|---|---|---|
| Apple | AAPL | 15% | Tech US |
| Microsoft | MSFT | 10% | Tech US |
| Air Liquide | AI.PA | 15% | Industrie EU |
| Or | GC=F | 50% | Matière première |

> La diversification sectorielle (Tech / Industrie / Or) vise à réduire la corrélation entre les actifs et limiter le risque global du portefeuille.

---

## Méthodologie

### 1. Analyse des rendements
- Calcul des **rendements logarithmiques** journaliers
- Analyse de la **matrice de corrélation** entre actifs
- Visualisation de l'évolution des prix sur 2 ans (504 jours)

### 2. Mesures de risque
| Indicateur | Description |
|---|---|
| **VaR historique (99%)** | Perte maximale journalière au seuil de 99% de confiance |
| **Expected Shortfall (99%)** | Moyenne des pertes au-delà de la VaR |
| **Ratio de Sharpe** | Rendement excédentaire par unité de risque total |
| **Ratio de Sortino** | Rendement excédentaire par unité de risque **baissier** uniquement |

> Le Sortino est plus pertinent que le Sharpe car il ne pénalise pas la volatilité haussière.

### 3. Optimisation Monte Carlo
- **10 000 combinaisons** de pondérations simulées aléatoirement
- Calcul du Sharpe pour chaque combinaison
- Identification du **portefeuille optimal** (Sharpe maximum)
- Visualisation de la **Frontière Efficiente**

---

## 📈 Résultats

### Mesures de risque (portefeuille équipondéré)
| Indicateur | Valeur |
|---|---|
| VaR historique (99%) | ~2.43% |
| Expected Shortfall (99%) | ~2.89% |
| Ratio de Sharpe | ~2.04 |

### Ratios de Sortino par actif
| Actif | Sortino |
|---|---|
| MSFT | ~1.84 |
| AAPL | ~2.01 |
| AI.PA | ~0.97 |
| GC=F | ~2.43 |

> Un ratio de Sortino > 1 indique que le rendement compense largement le risque baissier de l'actif.

### Portefeuille optimal (Max Sharpe — Monte Carlo)
| Actif | Poids optimal |
|---|---|
| MSFT | ~1.4% |
| AAPL | ~8.8% |
| AI.PA | ~3.7% |
| GC=F | ~87.4% |

> La simulation Monte Carlo surpondère fortement l'Or sur la période analysée, reflétant sa faible corrélation avec les actifs tech et sa forte performance récente.

---

## Bases de donnée

```
Python 3.10+
├── pandas          # Manipulation des données
├── numpy           # Calculs matriciels (covariance, Monte Carlo)
├── yfinance        # Données de marché en temps réel
├── matplotlib      # Visualisations statiques
├── seaborn         # Heatmap de corrélation
└── plotly          # Frontière Efficiente interactive
```

---

## Installation & Lancement

### Prérequis
```bash
pip install pandas numpy yfinance matplotlib seaborn plotly
```

### Lancer le notebook
```bash
# Option 1 : Google Colab (recommandé)
# Ouvrir le fichier .ipynb directement dans Google Colab

# Option 2 : Jupyter en local
jupyter notebook portfolio_risk_analysis.ipynb
```
https://colab.research.google.com/drive/10RhZ-BWUYkv5uuuIPvV-AkKiF20RBZky#
---

## Structure du projet

```
 portfolio-risk-analysis
 ┣ portfolio_risk_analysis.ipynb   # Notebook principal
 ┣ README.md                       # Documentation
 ┗ requirements.txt                # Dépendances
```

---

## Améliorations prévues

- [ ] Ajouter la **VaR Monte Carlo** et **VaR paramétrique** pour comparer les 3 méthodes
- [ ] Intégrer un **backtesting** de la VaR (nombre de dépassements observés)
- [ ] Ajouter des **contraintes de poids** (ex : min 5%, max 40% par actif)
- [ ] Déployer une **interface Streamlit** interactive
- [ ] Étendre l'analyse à un portefeuille de **crédit bancaire** (NPL, coût du risque)

---

## Auteur

**Brad Aymeric Feltre Kamanou**  
Étudiant Master Data Management — IÉSEG School of Management  

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue)](https://linkedin.com/in/ton-profil)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black)](https://github.com/ton-profil)

---

## Licence

Ce projet est à but éducatif. Les données sont issues de Yahoo Finance via l'API `yfinance`.

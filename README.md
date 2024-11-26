# Activité Pratique : Créer un modèle prédictif avec Scikit-learn pour estimer les ventes de produits alimentaires

<div class="group/conversation-turn relative flex w-full min-w-0 flex-col agent-turn"><div class="flex-col gap-1 md:gap-3"><div class="flex max-w-full flex-col flex-grow"><div data-message-author-role="assistant" data-message-id="d6a8329f-9091-4008-a3e0-021350ebf5f2" dir="auto" class="min-h-8 text-message flex w-full flex-col items-end gap-2 whitespace-normal break-words [.text-message+&amp;]:mt-5" data-message-model-slug="gpt-4o-mini"><div class="flex w-full flex-col gap-1 empty:hidden first:pt-[3px]"><div class="markdown prose w-full break-words dark:prose-invert light"><h3><strong>Activité Pratique : Créer un modèle prédictif avec Scikit-learn pour estimer les ventes de produits alimentaires</strong></h3><p>L’objectif de cette activité est de créer un modèle prédictif simple utilisant <strong>Scikit-learn</strong> pour estimer les ventes de produits alimentaires en fonction de données historiques. Nous allons suivre les étapes suivantes :</p><ol><li><strong>Charger les données sur les ventes de produits alimentaires</strong>.</li><li><strong>Préparer les données pour la modélisation</strong>.</li><li><strong>Entraîner un modèle de régression</strong>.</li><li><strong>Évaluer les performances du modèle</strong>.</li></ol><p>Nous allons utiliser un exemple fictif de données, où nous avons des informations sur les ventes passées de produits alimentaires, telles que le prix, les promotions, les jours de la semaine, la saisonnalité, et les données météorologiques, pour prédire les ventes futures.</p><h3><strong>Étape 1 : Charger les données sur les ventes de produits alimentaires</strong></h3><p>Nous allons charger un jeu de données fictif contenant des informations sur les ventes de produits alimentaires. Le jeu de données contient des colonnes comme le <strong>prix</strong>, la <strong>promotion</strong>, les <strong>jours de la semaine</strong>, et la <strong>température</strong>.</p><p>Voici un exemple de structure de données :</p><table><thead><tr><th>Date</th><th>Produit</th><th>Prix</th><th>Promotion</th><th>Température</th><th>Jour de la semaine</th><th>Ventes</th></tr></thead><tbody><tr><td>2023-01-01</td><td>Yaourt</td><td>2.5</td><td>1</td><td>15</td><td>Lundi</td><td>200</td></tr><tr><td>2023-01-02</td><td>Biscuit</td><td>1.5</td><td>0</td><td>12</td><td>Mardi</td><td>150</td></tr><tr><td>2023-01-03</td><td>Sauce</td><td>3.0</td><td>1</td><td>20</td><td>Mercredi</td><td>250</td></tr><tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr></tbody></table><h4>Code pour charger les données :</h4><pre class="!overflow-visible"><div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary dark:bg-gray-950"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none">python</div><div class="sticky top-9 md:top-[5.75rem]"><div class="absolute bottom-0 right-2 flex h-9 items-center"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none py-1"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-sm"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copier le code</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre hljs language-python"><span class="hljs-keyword">import</span> pandas <span class="hljs-keyword">as</span> pd

<span class="hljs-comment"># Charger un jeu de données fictif depuis un fichier CSV</span>
df = pd.read_csv(<span class="hljs-string">"ventes_produits.csv"</span>)

<span class="hljs-comment"># Afficher les premières lignes du dataset pour vérifier son contenu</span>
<span class="hljs-built_in">print</span>(df.head())
</code></div></div></pre><p>Si vous avez un fichier <code>ventes_produits.csv</code>, vous pouvez le charger et l'examiner. Sinon, vous pouvez simuler un dataset comme suit :</p><pre class="!overflow-visible"><div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary dark:bg-gray-950"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none">python</div><div class="sticky top-9 md:top-[5.75rem]"><div class="absolute bottom-0 right-2 flex h-9 items-center"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none py-1"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-sm"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copier le code</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre hljs language-python"><span class="hljs-comment"># Exemple de jeu de données fictif</span>
data = {
    <span class="hljs-string">'Date'</span>: [<span class="hljs-string">'2023-01-01'</span>, <span class="hljs-string">'2023-01-02'</span>, <span class="hljs-string">'2023-01-03'</span>, <span class="hljs-string">'2023-01-04'</span>, <span class="hljs-string">'2023-01-05'</span>],
    <span class="hljs-string">'Produit'</span>: [<span class="hljs-string">'Yaourt'</span>, <span class="hljs-string">'Biscuit'</span>, <span class="hljs-string">'Sauce'</span>, <span class="hljs-string">'Yaourt'</span>, <span class="hljs-string">'Biscuit'</span>],
    <span class="hljs-string">'Prix'</span>: [<span class="hljs-number">2.5</span>, <span class="hljs-number">1.5</span>, <span class="hljs-number">3.0</span>, <span class="hljs-number">2.5</span>, <span class="hljs-number">1.5</span>],
    <span class="hljs-string">'Promotion'</span>: [<span class="hljs-number">1</span>, <span class="hljs-number">0</span>, <span class="hljs-number">1</span>, <span class="hljs-number">1</span>, <span class="hljs-number">0</span>],
    <span class="hljs-string">'Température'</span>: [<span class="hljs-number">15</span>, <span class="hljs-number">12</span>, <span class="hljs-number">20</span>, <span class="hljs-number">18</span>, <span class="hljs-number">10</span>],
    <span class="hljs-string">'Jour de la semaine'</span>: [<span class="hljs-string">'Lundi'</span>, <span class="hljs-string">'Mardi'</span>, <span class="hljs-string">'Mercredi'</span>, <span class="hljs-string">'Jeudi'</span>, <span class="hljs-string">'Vendredi'</span>],
    <span class="hljs-string">'Ventes'</span>: [<span class="hljs-number">200</span>, <span class="hljs-number">150</span>, <span class="hljs-number">250</span>, <span class="hljs-number">220</span>, <span class="hljs-number">180</span>]
}

df = pd.DataFrame(data)
<span class="hljs-built_in">print</span>(df.head())
</code></div></div></pre><h3><strong>Étape 2 : Préparer les données pour la modélisation</strong></h3><p>Avant de créer le modèle, nous devons préparer les données en <strong>nettoyant</strong>, <strong>transformant</strong>, et <strong>sélectionnant</strong> les colonnes pertinentes.</p><p>Les étapes suivantes sont nécessaires :</p><ul><li>Convertir les variables catégorielles comme <strong>Produit</strong> et <strong>Jour de la semaine</strong> en variables numériques à l'aide de la méthode <code>get_dummies</code> de <strong>Pandas</strong>.</li><li>Sélectionner les variables explicatives (features) et la variable cible (target) : ici, la cible est <code>Ventes</code>.</li><li>Séparer les données en <strong>ensemble d'entraînement</strong> et <strong>ensemble de test</strong>.</li></ul><h4>Préparation des données :</h4><pre class="!overflow-visible"><div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary dark:bg-gray-950"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none">python</div><div class="sticky top-9 md:top-[5.75rem]"><div class="absolute bottom-0 right-2 flex h-9 items-center"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none py-1"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-sm"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copier le code</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre hljs language-python"><span class="hljs-comment"># Convertir les variables catégorielles en variables numériques</span>
df = pd.get_dummies(df, columns=[<span class="hljs-string">'Produit'</span>, <span class="hljs-string">'Jour de la semaine'</span>], drop_first=<span class="hljs-literal">True</span>)

<span class="hljs-comment"># Sélectionner les variables explicatives et la variable cible</span>
X = df.drop([<span class="hljs-string">'Date'</span>, <span class="hljs-string">'Ventes'</span>], axis=<span class="hljs-number">1</span>)  <span class="hljs-comment"># Suppression de la date et de la cible</span>
y = df[<span class="hljs-string">'Ventes'</span>]  <span class="hljs-comment"># Variable cible (Ventes)</span>

<span class="hljs-comment"># Diviser les données en ensembles d'entraînement et de test (80% train, 20% test)</span>
<span class="hljs-keyword">from</span> sklearn.model_selection <span class="hljs-keyword">import</span> train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=<span class="hljs-number">0.2</span>, random_state=<span class="hljs-number">42</span>)

<span class="hljs-comment"># Afficher les premières lignes de X_train et y_train pour vérifier</span>
<span class="hljs-built_in">print</span>(X_train.head())
<span class="hljs-built_in">print</span>(y_train.head())
</code></div></div></pre><h3><strong>Étape 3 : Entraîner un modèle de régression</strong></h3><p>Nous allons utiliser une <strong>régression linéaire</strong> pour prédire les ventes en fonction des variables explicatives. Scikit-learn propose un modèle de <strong>Régression Linéaire</strong> que nous allons entraîner sur l'ensemble d'entraînement.</p><h4>Code pour entraîner le modèle :</h4><pre class="!overflow-visible"><div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary dark:bg-gray-950"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none">python</div><div class="sticky top-9 md:top-[5.75rem]"><div class="absolute bottom-0 right-2 flex h-9 items-center"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none py-1"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-sm"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copier le code</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre hljs language-python"><span class="hljs-keyword">from</span> sklearn.linear_model <span class="hljs-keyword">import</span> LinearRegression

<span class="hljs-comment"># Créer un modèle de régression linéaire</span>
model = LinearRegression()

<span class="hljs-comment"># Entraîner le modèle sur l'ensemble d'entraînement</span>
model.fit(X_train, y_train)

<span class="hljs-comment"># Afficher les coefficients du modèle (importance de chaque variable)</span>
<span class="hljs-built_in">print</span>(<span class="hljs-string">"Coefficients du modèle : "</span>, model.coef_)
<span class="hljs-built_in">print</span>(<span class="hljs-string">"Intercept du modèle : "</span>, model.intercept_)
</code></div></div></pre><h3><strong>Étape 4 : Évaluer les performances du modèle</strong></h3><p>Une fois le modèle entraîné, nous devons évaluer ses performances sur l'ensemble de test. Nous utiliserons des métriques telles que l’<strong>erreur quadratique moyenne (MSE)</strong> et la <strong>précision</strong> (ou <strong>R²</strong>) pour mesurer la qualité du modèle.</p><h4>Code pour évaluer les performances :</h4><pre class="!overflow-visible"><div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary dark:bg-gray-950"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none">python</div><div class="sticky top-9 md:top-[5.75rem]"><div class="absolute bottom-0 right-2 flex h-9 items-center"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none py-1"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-sm"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copier le code</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre hljs language-python"><span class="hljs-keyword">from</span> sklearn.metrics <span class="hljs-keyword">import</span> mean_squared_error, r2_score

<span class="hljs-comment"># Prédire les ventes sur l'ensemble de test</span>
y_pred = model.predict(X_test)

<span class="hljs-comment"># Calculer l'Erreur Quadratique Moyenne (MSE)</span>
mse = mean_squared_error(y_test, y_pred)

<span class="hljs-comment"># Calculer le coefficient de détermination R^2</span>
r2 = r2_score(y_test, y_pred)

<span class="hljs-comment"># Afficher les résultats</span>
<span class="hljs-built_in">print</span>(<span class="hljs-string">f"Erreur quadratique moyenne (MSE) : <span class="hljs-subst">{mse}</span>"</span>)
<span class="hljs-built_in">print</span>(<span class="hljs-string">f"R^2 : <span class="hljs-subst">{r2}</span>"</span>)
</code></div></div></pre><p>Le <strong>R²</strong> mesure la proportion de la variance des ventes qui peut être expliquée par le modèle. Plus la valeur de R² est proche de 1, mieux le modèle prédit les ventes.</p><h3><strong>Conclusion :</strong></h3><ul><li>Si le modèle a un <strong>mauvais R²</strong> (par exemple proche de 0), cela indique que le modèle ne capture pas bien la relation entre les variables et les ventes. Dans ce cas, nous pourrions envisager d’utiliser des <strong>modèles plus complexes</strong> comme les <strong>arbres de décision</strong>, la <strong>régression polynomiale</strong> ou même des modèles d'<strong>apprentissage profond</strong>.</li><li>Si le <strong>MSE est faible</strong> et le <strong>R² est élevé</strong>, le modèle est bien adapté pour prédire les ventes.</li></ul><h3><strong>Améliorations possibles :</strong></h3><ul><li>Ajouter plus de <strong>variables explicatives</strong> comme les campagnes publicitaires, les jours fériés, ou les tendances économiques pour améliorer la précision du modèle.</li><li>Tester <strong>d'autres algorithmes</strong> comme la <strong>régression des forêts aléatoires</strong> ou <strong>XGBoost</strong> pour améliorer les prédictions.</li></ul><hr><h3><strong>Exécution complète du code :</strong></h3><p>Voici le code complet pour cette activité :</p><pre class="!overflow-visible"><div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary dark:bg-gray-950"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none">python</div><div class="sticky top-9 md:top-[5.75rem]"><div class="absolute bottom-0 right-2 flex h-9 items-center"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none py-1"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-sm"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copier le code</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre hljs language-python"><span class="hljs-keyword">import</span> pandas <span class="hljs-keyword">as</span> pd
<span class="hljs-keyword">from</span> sklearn.model_selection <span class="hljs-keyword">import</span> train_test_split
<span class="hljs-keyword">from</span> sklearn.linear_model <span class="hljs-keyword">import</span> LinearRegression
<span class="hljs-keyword">from</span> sklearn.metrics <span class="hljs-keyword">import</span> mean_squared_error, r2_score

<span class="hljs-comment"># Exemple de données fictives</span>
data = {
    <span class="hljs-string">'Date'</span>: [<span class="hljs-string">'2023-01-01'</span>, <span class="hljs-string">'2023-01-02'</span>, <span class="hljs-string">'2023-01-03'</span>, <span class="hljs-string">'2023-01-04'</span>, <span class="hljs-string">'2023-01-05'</span>],
    <span class="hljs-string">'Produit'</span>: [<span class="hljs-string">'Yaourt'</span>, <span class="hljs-string">'Biscuit'</span>, <span class="hljs-string">'Sauce'</span>, <span class="hljs-string">'Yaourt'</span>, <span class="hljs-string">'Biscuit'</span>],
    <span class="hljs-string">'Prix'</span>: [<span class="hljs-number">2.5</span>, <span class="hljs-number">1.5</span>, <span class="hljs-number">3.0</span>, <span class="hljs-number">2.5</span>, <span class="hljs-number">1.5</span>],
    <span class="hljs-string">'Promotion'</span>: [<span class="hljs-number">1</span>, <span class="hljs-number">0</span>, <span class="hljs-number">1</span>, <span class="hljs-number">1</span>, <span class="hljs-number">0</span>],
    <span class="hljs-string">'Température'</span>: [<span class="hljs-number">15</span>, <span class="hljs-number">12</span>, <span class="hljs-number">20</span>, <span class="hljs-number">18</span>, <span class="hljs-number">10</span>],
    <span class="hljs-string">'Jour de la semaine'</span>: [<span class="hljs-string">'Lundi'</span>, <span class="hljs-string">'Mardi'</span>, <span class="hljs-string">'Mercredi'</span>, <span class="hljs-string">'Jeudi'</span>, <span class="hljs-string">'Vendredi'</span>],
    <span class="hljs-string">'Ventes'</span>: [<span class="hljs-number">200</span>, <span class="hljs-number">150</span>, <span class="hljs-number">250</span>, <span class="hljs-number">220</span>, <span class="hljs-number">180</span>]
}

<span class="hljs-comment"># Convertir en DataFrame</span>
df = pd.DataFrame(data)

<span class="hljs-comment"># Préparer les données</span>
df = pd.get_dummies(df, columns=[<span class="hljs-string">'Produit'</span>, <span class="hljs-string">'Jour de la semaine'</span>], drop_first=<span class="hljs-literal">True</span>)
X = df.drop([<span class="hljs-string">'Date'</span>, <span class="hljs-string">'Ventes'</span>], axis=<span class="hljs-number">1</span>)
y = df[<span class="hljs-string">'Ventes'</span>]
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=<span class="hljs-number">0.2</span>, random_state=<span class="hljs-number">42</span>)

<span class="hljs-comment"># Entraîner le modèle</span>
model = LinearRegression()
model.fit(X_train, y_train)

<span class="hljs-comment"># Prédire et évaluer</span>
y_pred = model.predict(X_test)
mse = mean_squared_error(y_test, y_pred)
r2 =
</code></div></div></pre></div></div></div></div><div class="mb-2 flex gap-3 empty:hidden -ml-2"><div class="items-center justify-start rounded-xl p-1 flex"><div class="flex items-center"><span class="" data-state="closed"><button class="rounded-lg text-token-text-secondary hover:bg-token-main-surface-secondary" aria-label="Copier" data-testid="copy-turn-action-button"><span class="flex h-[30px] w-[30px] items-center justify-center"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-md-heavy"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg></span></button></span><span class="hidden"></span><button class="cursor-pointer h-[30px] rounded-md px-1 text-token-text-secondary hover:bg-token-main-surface-secondary"><div class="flex items-center pb-0"><span class="overflow-hidden text-clip whitespace-nowrap text-sm" style="opacity: 0; padding-left: 0px; width: 0px; will-change: opacity;">Bon Travail</span></div></button></div></div></div><div class="pr-2 lg:pr-0"></div><div class="mt-3 w-full empty:hidden"><div class="text-center"></div></div></div><div class="absolute" style="top: -29.2031px; left: 0.5px; width: 696px; height: 24px;"><span class="" data-state="closed"><button class="btn relative btn-secondary btn-small shadow-lg"><div class="flex items-center justify-center"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-md"><path d="M7.5 13.25C7.98703 13.25 8.45082 13.1505 8.87217 12.9708C8.46129 14.0478 7.62459 15.5792 6.35846 15.76C5.81173 15.8382 5.43183 16.3447 5.50993 16.8914C5.58804 17.4382 6.09457 17.8181 6.6413 17.7399C9.19413 17.3753 10.7256 14.4711 11.169 12.1909C11.4118 10.942 11.3856 9.58095 10.8491 8.44726C10.2424 7.16517 8.92256 6.24402 7.48508 6.25001C5.55895 6.25805 4 7.82196 4 9.74998C4 11.683 5.567 13.25 7.5 13.25Z" fill="currentColor"></path><path d="M16.18 13.25C16.667 13.25 17.1308 13.1505 17.5522 12.9708C17.1413 14.0478 16.3046 15.5792 15.0385 15.76C14.4917 15.8382 14.1118 16.3447 14.1899 16.8914C14.268 17.4382 14.7746 17.8181 15.3213 17.7399C17.8741 17.3753 19.4056 14.4711 19.849 12.1909C20.0918 10.942 20.0656 9.58095 19.5291 8.44726C18.9224 7.16517 17.6026 6.24402 16.1651 6.25001C14.2389 6.25805 12.68 7.82196 12.68 9.74998C12.68 11.683 14.247 13.25 16.18 13.25Z" fill="currentColor"></path></svg></div></button></span></div></div>

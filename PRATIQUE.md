**Total : 100 points — Seuil de réussite : 50/100**  
**Durée estimée : ~1h00**  
**Documents autorisés : Aucun**

> Pour les trous de code (Q1) : répondez dans ce fichier en numérotant vos réponses.  
> Pour le code from scratch (Q2) : créez les fichiers PHP directement dans votre dossier.  
> Écrivez votre nom et prénom ci-dessous.

**Nom et prénom :** ___KEMO FRANC LOIC____________________

---

## Question 1 — Compléter du code PHP (40 points)

> **Contexte :** Un visiteur s'inscrit à un atelier en ligne. Le formulaire doit **conserver les données saisies** si le formulaire est renvoyé incomplet, et sauvegarder l'inscription dans un fichier texte.

Complétez les parties `/* 1 */` à `/* 12 */` dans le code ci-dessous.  
**Écrivez vos réponses numérotées dans la section "Vos réponses" plus bas.**

```php
<?php
$erreur = "";

// Traitement si le formulaire a été soumis
if(/* 1 */($_POST["envoyer"])) {

    // Vérification des champs obligatoires
    if(/* 2 */($_POST["prenom"]) || empty($_POST["email"])) {
        $erreur = "Veuillez remplir tous les champs obligatoires.";
    } else {
        // Nettoyage des données
        $prenom = /* 3 */("\\", "", $_POST["prenom"]);
        $email  = str_replace("\\", "", $_POST["email"]);
        $niveau = str_replace("\\", "", $_POST["niveau"]);

        // Récupération de la date du jour (format jj/mm/aaaa)
        $date = /* 4 */("d/n/Y");

        // Sauvegarde dans le fichier (ajout à la fin)
        $fichier = /* 5 */("inscrits.txt", /* 6 */);
        /* 7 */($fichier, $prenom . " | " . $email . " | " . $niveau . " | " . $date . "\n");
        /* 8 */($fichier);

        // Redirection vers la page de confirmation
        /* 9 */("Location: confirmation.php");
    }
}
?>

<form method="post" action="inscription.php">
  <fieldset>
    <legend>Inscription à l'atelier</legend>

    <?php if(!empty($erreur)) echo "<p style='color:red'>" . $erreur . "</p>"; ?>

    Prénom :
    <input type="text" name="prenom" size="40" value="
      <?php
        if(!/* 10 */($_POST["prenom"]))
          echo /* 11 */($_POST["prenom"]);
      ?>" />
    <br />

    Email :
    <input type="text" name="email" size="40" value="
      <?php
        if(!empty($_POST["email"]))
          echo htmlentities($_POST["email"]);
      ?>" />
    <br />

    Débutant :
    <input type="radio" name="niveau" value="débutant"
      <?php
        if(isset($_POST["niveau"]) && $_POST["niveau"] == "débutant")
          echo "checked=\"checked\"";
      ?> />

    Avancé :
    <input type="radio" name="niveau" value="avancé"
      <?php
        if(isset($_POST["niveau"]) && $_POST["niveau"] == "avancé")
          echo /* 12 */;
      ?> />
    <br />

    <input type="submit" name="envoyer" value="S'inscrire" />
    <input type="reset" value="Effacer" />
  </fieldset>
</form>
```

### ✏️ Vos réponses — Q1

Remplacez chaque `?` par votre réponse :

| N° | Votre réponse |
|---|---|
| 1 | isset |
| 2 | empty |
| 3 | str_replace |
| 4 | date|
| 5 | fopen |
| 6 | "a" |
| 7 | fwrite|
| 8 | fclose |
| 9 | header |
| 10 | empty|
| 11 | htmlentities |
| 12 | ? |

*(~3,5 pts par réponse correcte)*

---

## Question 2 — Écrire du code from scratch (60 points)

> **Contexte :** Vous développez une page d'administration pour consulter et rechercher parmi les inscrits sauvegardés dans `inscrits.txt`.  
> Chaque ligne du fichier a la structure : `prenom | email | niveau | date`

Écrivez **un seul fichier** `admin_inscrits.php` qui remplit les deux fonctions ci-dessous.

---

### Partie A — Affichage de la liste des inscrits *(30 pts)*

Le fichier doit :

1. Lire `inscrits.txt` avec `fread()` + `filesize()` pour compter le nombre total d'inscrits (nombre de `\n`) et l'afficher en haut de page *(5 pts)*
2. Si le fichier est vide ou inexistant, afficher : *"Aucun inscrit pour l'instant."* *(5 pts)*
3. Lire le fichier **ligne par ligne** avec `fgets()` *(5 pts)*
4. Pour chaque ligne, découper les champs avec `explode()` sur le séparateur `|` *(5 pts)*
5. Afficher les inscrits dans un **tableau HTML** avec les colonnes :
   **Prénom** | **Email** | **Niveau** | **Date d'inscription** *(10 pts)*

---

### Partie B — Recherche par mot-clé *(30 pts)*

Au-dessus du tableau, le fichier doit afficher un formulaire avec :
- Un champ texte *"Rechercher un inscrit (prénom ou email)"*
- Un bouton *"Rechercher"*

Comportement attendu :

1. Vérifier que le champ de recherche n'est pas vide *(5 pts)*
2. Si une recherche est soumise, relire `inscrits.txt` ligne par ligne et afficher **uniquement les lignes** contenant le mot recherché — insensible à la casse avec `stristr()` *(15 pts)*
3. Si aucun résultat : afficher *"Aucun inscrit ne correspond à votre recherche."* *(5 pts)*
4. Si aucune recherche n'est soumise : afficher la liste complète *(5 pts)*

Ajoutez un lien retour vers `inscription.php` en bas de page.

---

## 📊 Barème

| Question | Détail | Points |
|---|---|---|
| Q1 — Compléter du code | 12 trous (~3,5 pts chacun) | 40 |
| Q2 — From scratch | Partie A — Affichage liste | 30 |
| | Partie B — Recherche | 30 |
| **TOTAL** | | **100** |

---

> ⚠️ Seuil de réussite : **50/100 minimum**

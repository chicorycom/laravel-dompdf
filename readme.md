## DOMPDF Wrapper pour Laravel 5

### Pour Laravel 4.x, vérifiez le [0.4 branch](https://github.com/barryvdh/laravel-dompdf/tree/0.4)!

Exigez ce paquet dans votre composer.json et mettez à jour le compositeur. Cela va télécharger le paquet et les bibliothèques dompdf + font lib aussi.

    composer require Chicorycom/laravel-dompdf:dev-master

## Installation

### Laravel 5.x:

Après la mise à jour de composer, ajoutez le fournisseur de services au tableau des fournisseurs dans config/app.php

    Chicorycom\DomPDF\ServiceProvider::class,

Vous pouvez éventuellement utiliser la façade pour un code plus court. Ajoutez ceci à vos façades:

    'PDF' => Chicorycom\DomPDF\Facade::class,

### Lumen:

Après la mise à jour composer ajouter les lignes suivantes pour enregistrer dans le fournisseur `bootstrap/app.php`

  ```
  $app->register(\Barryvdh\DomPDF\ServiceProvider::class);
  ```
  
Pour modifier la configuration, copiez le fichier de configuration dans votre dossier de configuration et activez-le `bootstrap/app.php`:

  ```
  $app->configure('dompdf');
  ```
  
## En utilisant

Vous pouvez créer une nouvelle instance DOMPDF et charger une chaîne HTML, un fichier ou un nom de vue. Vous pouvez l'enregistrer dans un fichier, ou diffuser (afficher dans le navigateur) ou télécharger.

    $pdf = App::make('dompdf.wrapper');
    $pdf->loadHTML('<h1>Test</h1>');
    return $pdf->stream();

Ou utilisez la façade:

    $pdf = PDF::loadView('pdf.invoice', $data);
    return $pdf->download('invoice.pdf');

Vous pouvez enchaîner les méthodes:

    return PDF::loadFile(public_path().'/myfile.html')->save('/path-to/my_stored_file.pdf')->stream('download.pdf');

Vous pouvez modifier l'orientation et la taille du papier, et masquer ou afficher les erreurs (par défaut, les erreurs sont affichées lorsque le débogage est activé)

    PDF::loadHTML($html)->setPaper('a4', 'landscape')->setWarnings(false)->save('myfile.pdf')

Si vous avez besoin de la sortie sous forme de chaîne, vous pouvez obtenir le PDF rendu avec la fonction output (), vous pouvez donc l'enregistrer / l'éditer vous-même.

Utilisez `php artisan vendor: publish` pour créer un fichier de configuration situé à` config/dompdf.php` qui vous permettra de définir des configurations locales pour changer certains paramètres (papier par défaut, etc).
Vous pouvez également utiliser ConfigProvider pour définir certaines clés.

### Configuration
Les paramètres de configuration par défaut sont définis dans `config/dompdf.php`. Copiez ce fichier dans votre propre répertoire de configuration pour modifier les valeurs. Vous pouvez publier la configuration en utilisant cette commande:

    php artisan vendor:publish --provider="Barryvdh\DomPDF\ServiceProvider"

Vous pouvez toujours modifier les options de dompdf dans votre code avant de générer le pdf en utilisant cette commande:

    PDF::setOptions(['dpi' => 150, 'defaultFont' => 'sans-serif']);
    
Options disponibles et leurs valeurs par défaut:
* __rootDir__: "{app_directory}/vendor/dompdf/dompdf"
* __tempDir__: "/tmp" _(available in config/dompdf.php)_
* __fontDir__: "{app_directory}/storage/fonts/" _(disponible dans config/dompdf.php)_
* __fontCache__: "{app_directory}/storage/fonts/" _(disponible dans config/dompdf.php)_
* __chroot__: "{app_directory}" _(disponible dans config/dompdf.php)_
* __logOutputFile__: "/tmp/log.htm"
* __defaultMediaType__: "screen" _(disponible dans config/dompdf.php)_
* __defaultPaperSize__: "a4" _(disponible dans config/dompdf.php)_
* __defaultFont__: "serif" _(disponible dans config/dompdf.php)_
* __dpi__: 96 _(available in config/dompdf.php)_
* __fontHeightRatio__: 1.1 _(disponible dans config/dompdf.php)_
* __isPhpEnabled__: false _(disponible dans config/dompdf.php)_
* __isRemoteEnabled__: true _(disponible dans config/dompdf.php)_
* __isJavascriptEnabled__: true _(disponible dans config/dompdf.php)_
* __isHtml5ParserEnabled__: false _(disponible dans config/dompdf.php)_
* __isFontSubsettingEnabled__: false _(disponible dans config/dompdf.php)_
* __debugPng__: false
* __debugKeepTemp__: false
* __debugCss__: false
* __debugLayout__: false
* __debugLayoutLines__: true
* __debugLayoutBlocks__: true
* __debugLayoutInline__: true
* __debugLayoutPaddingBox__: true
* __pdfBackend__: "CPDF" _(disponible dans config/dompdf.php)_
* __pdflibLicense__: ""
* __adminUsername__: "user"
* __adminPassword__: "password"

### Tip: UTF-8 support
Dans vos modèles, définissez la méta-étiquette UTF-8:

    <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>

### Tip: Page breaks
Vous pouvez utiliser les propriétés CSS `page-break-before`/` page-break-after` pour créer une nouvelle page.

    <style>
    .page-break {
        page-break-after: always;
    }
    </style>
    <h1>Page 1</h1>
    <div class="page-break"></div>
    <h1>Page 2</h1>
    
### License

Ce Wrapper DOMPDF pour Laravel est un logiciel open-source sous licence [MIT license](http://opensource.org/licenses/MIT)
"# laravel-dompdf" 

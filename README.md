Skrupel-Erweiterung KI
======================

Version: 0.11.4 (Diese Version funktioniert ab Skrupel-Version 0.973!)

Autor: Wasserleiche

Email: Wasserleiche88@gmail.com


Installations-Anleitung für die Test-Version der Skrupel-KI
-----------------------------------------------------------

### 1. Entpacken

Die Skrupel-KI-Datei muss einfach in das Verzeichnis `skrupel/extend/ki` entpackt werden.

#### ... oder via Git

    $ cd DEIN_SKRUPEL_VERZEICHNIS/extend
    $ git clone https://github.com/skrupel/skrupel-extension-ki.git ki


### 2. Aktivieren

Danach muss im Admin-Menü von Skrupel die KI-Erweiterung aktiviert werden. Fertig!


### 3. Änderungen im Skrupel-Code

Damit bei deaktivierter KI auch wirklich die KI-Spieler nicht auswaehlbar sind, sollte in der Datei `admin/spiel_alpha.php` in Zeile 372 nach dem `}` folgendes eingefügt werden:

```php
elseif(is_file("../extend/ki/ki_basis/ki_basis.php")) {
    include_once("../extend/ki/ki_basis/ki_basis.php");
    $ki_daten = ki_basis::ermittleKIDaten();
    $continue = false;
    foreach($ki_daten as $ki) {
        $comp_nick = substr($nick, 0, strlen($ki['nick']));
        if($comp_nick == $ki['nick']) {
            $continue = true;
            break;
        }
    }
    if($continue) continue;
}
```

Skrupel-Erweiterung KI
======================

Version: 0.11.4
Autor: Wasserleiche
Email: Wasserleiche88@gmail.com


Installations-Anleitung fuer die Test-Version der Skrupel-Erweiterung KI
------------------------------------------------------------------------

- Diese Version funktioniert ab Skrupel-Version 0.973!

- Die Skrupel-KI-Datei muss einfach in das Verzeichnis `skrupel/extend/ki` entpackt werden. Danach muss im 
  Admin-Menü von Skrupel die KI-Erweiterung aktiviert werden. Fertig!

- Damit bei deaktivierter KI auch wirklich die KI-Spieler nicht auswaehlbar sind, sollte in der Datei 
  `admin/spiel_alpha.php` in Zeile 372 nach dem `}` folgendes eingefügt werden:

    ```
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
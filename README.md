
# Blink Update Process Github Integratie

Blink Thema Updater (Github Integratie)

## Beschrijving

In deze POC wordt het Blink Thema up to date gehouden via de plugin: [plugin-update-checker](https://github.com/YahnisElsts/plugin-update-checker) met Github integratie. Er wordt gekeken of de style.css in de root van het Thema gelijk is aan de laatste tag release versie in Github. 

Deze POC is vergelijkbaar met [Blink Updater Selfhosted](https://github.com/Myron1271/blink), echter wordt hier geen gebruik gemaakt van het handmatig uploaden van een .zip.

***Let op!**: deze installatie gaat ervan uit dat er al een Lokale Wordpress Environment is opgezet en dat het Thema al is toegevoegd.*

* Link voor het opzetten van WordPress: [Local WordPress Setup](https://jetpack.com/resources/wordpress-localhost/).

## Getting Started

### Dependencies

Hoewel de plugin-update-checker niet geïnstalleerd zal worden als Dependency is deze wel nodig voor dit project.

[plugin-update-checker](https://github.com/YahnisElsts/plugin-update-checker).

### Installatie

Voor deze POC moeten we de plugin-update-checker in de map **plugins** plaatsen en met een stukje code in **functions.php** van het Wordpress thema ervoor zorgen dat er gecontroleerd wordt op de nieuwste versies.

**Stappen:**

- Begin met het verkrijgen van de laatste versie van de [plugin-update-checker releases](https://github.com/YahnisElsts/plugin-update-checker/releases).
- Kopieer de uitgepakte .zip naar de plugins folder in Wordpress.
- Voor deze POC zal de volgende code in de functions.php van het Blink thema gezet worden, deze code hoeft niet per se in de functions.php, maar raad ik wel aan:

```
<?php
/**
 * Plugin Name: Blink Theme Updater
 * Description: Automatische GitHub-updates voor het Blink-theme.
 * Version: 1.0.0
 */

require plugin_dir_path(__FILE__) . 'plugin-update-checker/plugin-update-checker.php';
use YahnisElsts\PluginUpdateChecker\v5\PucFactory;

$updateChecker = PucFactory::buildUpdateChecker(
    'https://example.com/Github-Repository', // Link naar het git repository met het Blink Thema
    get_theme_root() . '/Blink', 'Blink' // Het pad naar het theme met de naam "Blink"
);

$updateChecker->setBranch('master'); // (of Main)

```

De installatie van de plugin is nu voltooid. Om het Wordpress thema gereed te maken voor toekomstige updates, moeten we het bestand **style.css** in de root van het thema aanpassen. Dit doen we door het volgende toe te voegen:

```
/*!  
Version: 1.0.0 // Moet gelijk zijn met de tag van de laatste release  
*/
```

De version in **style.css** zal vergeleken worden met de tag in de meeste recenste Github Release. Als deze lager is zal Wordpress aangegeven dat er een update beschikbaar is.

**Met dit is de installatie klaar.**

### Updates uitbrengen

Met de Github integratie kunnen eenvoudig aanpassingen naar het thema worden gepusht, waarna er een nieuwe release met een unieke tag kan worden aangemaakt.

Het is belangrijk dat bij elke nieuwe release het bestand **style.css** wordt bijgewerkt en dat het versienummer overeenkomt met de nieuwste tag. Als dit niet gebeurt, zal Wordpress blijven aangeven dat er een update beschikbaar is.

Als iemand een oudere versie van het thema gebruikt, verschijnt er in WordPress een melding met de mogelijkheid om het thema te updaten. Zie de afbeelding als voorbeeld:
<img width="1007" alt="Blink-ReadMe-Selfhosted" src="https://github.com/user-attachments/assets/489763db-cd51-44c7-b01d-2a24b8798113" />

## Auteurs

[Myron Seelen LinkedIn](https://www.linkedin.com/in/myron-seelen/)

## Versies

*Check releases tab voor version history:*
[Versies](https://github.com/Myron1271/blink-theme/releases).




# Folderstruktur


````
/assets
    /css-images        // bara css-bilder
    /javascripts       // endast egen-utvecklad js
    /fonts
    /sass
    /stylesheets
        screen.css
        print.css
/images                // alla bilder i "content"
/html                  // "sajten"
/prototypes            // här ligger alla prototyper för sajten
/styleguide            // dokumentation
/ui-live               // "/assets" exporterad från Live, read-only
/vendor                // 3:e-partskod, t.ex. jQuery 
````
Innehåll och användade av respektive folder förklaras nedan:

### /assets/css-images

Här läggs alla css-bilder. I praktiken bör dessa vara sprites så långt som möjligt.

### /assets/javascripts

Här läggs egenutvecklad javascript.

`REVIEW` Kanske ska javascript hellre ligga ihop med *Block*?

### /assets/fonts

Här läggs alla webbfonter.

### /assets/sass

Använd denna folderstruktur:

````
/sass
    /base                 // Reset och standard-styling, i princip inga klasser här
    /blocks               // Alla "legobitar", building blocks
    /modules              // Specifika vyer (men inte nödvändigtvis sidor)
                          //   "blocks" används inuti  
    /color                // "Grafisk profil"
    /hui                  // Happy User-specifikt, för visualisering av Color Palette
    /layout               // Grid och generella spacing-utilities
    /theme                // Används bara för en sajt som behöver *flera* tema
    _mixins.scss          // Alla mixins som används av flera scss-filer
    _utilities.scss       // Accessibility
    _variables.scss       // Sajt-variabler, inklusive färger
    screen.scss
    print.scss
````

* `/sass/base`  
Reset genom normalize.css och standard-styling. Syftet är ett snyggt och effektivt utgångsläge. I princip inga klasser här utan bara rena element. Princip: inga horisontella avstånd, margin endast i botten.
      
    `REVIEW` Ska jag lägga `inuit.css` här?

    ````
      /base 
        _form.scss
        _reset.scss // https://github.com/necolas/normalize.css/blob/master/normalize.css
        _spaces.scss
        _table.scss
        _typography.scss
    ````

* ``/sass/blocks (pluralis)``    
Blocks, eller *Modules* eller *objekt* som de ibland också benäms, är de små byggstenarna för designen. Det är delar som är relevanta att återanvända om och om igen. De används i princip genom att lägga till en klass till ett element.
  
    * Hur stor ska då ett block vara? Det beror på vilken typ av GUI som byggs. Till exempel: 
        * En contentdriven sajt har troligtvis ganska små byggstenar som återanvänds gång på gång på samma vy och emellan vyer, ett exempel på detta är listningar, kommentarsfunktioner. 
  
    * **Viktig princip:** Lägg alla *layoutalternativ*, block *states* och *media queries* i block-filen. Namnge eventuella javascript med samma namn som block. Det ska vara enkelt att flytta ett komplett block mellan projekt.  
`REVIEW` ska javascript ligga **i** Block eller ska de ligga i `/javascripts`?

    ````
    // Dessa block kan anses vara standard:
    /blocks
      _alerts.scss
      _backgrounds.scss
      _borders.scss
      _buttons.scss        // Kompletta knappar, inklusive mixins
      _forms.scss          // "Branding", override av /base/_form.scss
      _icons.scss
      _lists.scss
      _media.scss          // Nicole:s media-objekt
      _navigation.scss
      _sprites.scss
      _tables.scss
      _typograhy.scss      // "Branding", override av /base/_typography.scss
    
      // I vissa projekt kan det vara befogat att lägg till denna uppdelning:
      _article.scss
        .content-main
        .content-secondary
        .content-tertiary
      _footer.scss
      _header.scss
      _navs.scss
        #nav-main
         #nav-sec
      _sidebar.scss
    ````

* ``/sass/modules (pluralis)``    
Modules är "stora" sammanhållande vyer:

    * En webbapplikation som har komplexa vyer som bara används en gång, exempel en modul för tidredovisning; hela denna modul bilda en module, `_timesheet.scss`. En modul använder sig av de mindre byggstenarna i blocks som till exemepel `_buttons.scss`, `_lists.scss` etcetera.
    * En viktig kontrollfråga är: "Om jag vill återanvända denna modul i ett annat projekt, är det enkelt att bara kopiera markup och css? Kan jag enkelt se beroenden till blocks för att kopiera dem också?"

    ````
    // Dessa moduler finns troligen med:
    /modules
      _footer.scss
      _header.scss
      _login.scss
    ````

* `/sass/color`    
  Här skapas alla färger som kommer att användas i projektet. Logiken är denna
    1. Ange grundfärgerna från den grafiska profilen i `_color-settings.scss`
    2. I `_color-function-scale-color.scss` används så kallade *color funktions* från SASS för att skapa olika nyanser av grundfärgerna.
    3. När vi nu har alla färgerna, skapar vi en presentation av dess i `color-demo-table.scss`; och sätter samman en css-fil genom `color-demo-page.scss`.
    4. I html-sidan `color-palette.html` visas slutresultatet.

    ````
    _color-demo-table.scss            // Styles för att visa färgpaletten
    _color-function-scale-color.scss  // SASS color function för att rendera toner
    _color-settings.scss              // Färgerna som ska användas, från Grafisk Profil
    color-demo-page.scss
    color-palette.html                // Färgpaletten
    ````
    
* `/sass/layout`    
I Layout finns det grid-system som sajten använder. I Layout ska sådant som avgör positionering och placering ligga. Använd `l-`som prefix för klasserna.

    ````
    _grid.scss // Troligtvis är Susy det gridsystem som är att föredra
    _layout-utilities.scss
      - clearfix here?
      - floats
      - aligns
    ````
    
* `/sass/theme`    
Används bara för en sajt som använder sig av flera tema. Då ligger de `blocks` som ska skrivas över här. I huvudsak är det bara ändringar i fonter och färger som är aktuella att ändra.

* `/sass/`    

    ```` 
    _mixins.scss          // Alla mixins som används av flera scss-filer
      - animations          
      - backgrounds     
      - borders         
      - shadows         
      - transitions     
    ````

    ````
    _utilities.scss       // Accessibility
      - visual-impared
      - screen-reader
    ````

    ````
    _variables.scss       // Sajt-variabler, inklusive färger
    ````













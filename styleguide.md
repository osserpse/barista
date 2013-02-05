# Styleguide

## Layout i koden

* Använd ``UTF-8`` som encoding, lägg detta överst i SASS/CSS-filen: ``@charset "UTF-8";``
* Använd *Unix line endings* (I Windows-datorer behöver en inställning för detta göras.)
* Definitioner:

    ````
    [selector]{
      [property]:[value];
      [<-Declaration ->];
    }
    ````

* Använd två mellanslag för indrag.
* Använd ett mellanslag runt ``{`` , före ``}`` och efter kolon ``:``.
* Använd hex för färger, om möjligt även kortformen ``#000``. 
* Använd alltid ett mellanslag efter ``, ``
* Avsluta alla deklarationer med ``;``, se till att radan avslutas där (inga mellanslag).
* Den första ``{`` ska vara på samma rad som selektorn; den avslutande ``}`` ska vara på egen rad i kant med selektorn. Detta för att det ska vara enkelt att göra manipulationer på radnivå.
* Gör indrag med två mellanslag för varje selektorer som är barn. Inga blankrader mellan dessa selektorer. Detta för att tydliggöra hierarkin.
* Skriv deklarationer i bokstavsordning. Lägg SASS-includes sist.
* Gör en blankrad mellan nya selektorer.

Exempel på bra kodlayout:

     // Bra exempel
    .styleguide { 
      background: rgba(0, 0, 0, .5);
      border: 1px solid #cc0;
      color: #000;
      @include foobar
    }
      .styleguide p {
        color: #333;
      }
        .styleguide p a {
          color: #666;
        }

    .foobar {
      color: #999;
    }

## Selektorer

* Undvik att använda ID. Dels kan dessa inte återanvändas och dels ger de en onödigt tung [specificitet](http://www.w3.org/TR/CSS2/cascade.html#specificity).
* Försök att hålla alla selektorer "jämntunga". I praktiken är innebär det att bara använda en klass (En OOCSS-princip).
* Gör alla namn "framtunga" för att tydliggöra vad som hör ihop.
* Namngivning av klasser är inspirerad av BEM (Block Element Modifier) och Nicolas Gallagher:
    * ``.block`` är byggstenen, eller "legobiten"".
    * ``.block--modifier`` *Modifier* är en variant eller state av ``.block``.  
    * ``.block__element`` *Element* är delarna som bygger upp ett ``.block``.

    ````
    .block {}
    .block-long-name {} // flera ord skiljs med bindestreck
    .block-long-name--modifier {}
    .block__sub-block {}
    .block__sub-block--modifier {}
    ````
* För SASS-variabler används ``snake_case`` konsekvent.

    ````
    $single: foo;
    $double_word: bar;
    ````
### Javascript-hooks

* Skilj strikt mellan selektorer för styling och selektorer använda av javascript. 
* Lägg **aldrig** styling på en selektor för js-hooks.
* Använd **aldrig** js-hooks på en selektor för styling.
* Namnge en js-hook med ``.js-`` som *name space*, till exempel ``.js-toggle``

    ````
    .js-action-name
    .js-component-type
    ````
### States

    ````
    .is-state-type
    ````


## Kommentarer

(Här utgår vi från att vi använder SASS som preprocessor, byt till rätt kommentarstecken om annat används)

* Max 80 tecken brett.
* **Filhuvud**. *Notera att filnamnet på rad 2 har kommentarstecken som gör att det kommer att skrivas ut i CSS-filen. Detta för att underlätta debug.*

    ````
    // ============================================================================
    /* FILNAMN I VERSALER */
    //
    // @project      Projektets namne
    // @author       Anders Andersson, Firma
    // @version      Version, kan vara ett namn eller versionnummer
    // ============================================================================
    ````
* **Grupperingar**. 
    
    ````
    // NAMN PÅ GRUPPERING I VERSALER
    // ----------------------------------------------------------------------------
    
    .block {
      // property
    }
    
    // Sub-gruppering i gemener, ingen blankrad under
    .block {
      // property
    }
    ````
    
* Använd ``TODO`` för att visa på funktionalitet som bör/ska läggas till senare.
* Använd ``FIXME`` för kod som är trasig och **måste** fixas.
* Använd ``OPTIMIZE`` för att peka på kod som är ineffektiv, både ur prestanda men också ur underhållsperspektiv.
* Använd ``HACK`` för kod som verkligen är hack eller som borde kunna göras bättre.
* Använd ``REVIEW`` för delar som bör genomgå en "code review"; antingen för att bättre följa praxis eller för att säkerställa att den fungerar som det är tänkt.

    
## Verktyg och best practices

* [CSS Lint](http://csslint.net/)
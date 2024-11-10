# Individuele eindopdracht

## Introductie
In de flowcharts hieronder wordt de werking van het programma van een zaagmachine beschreven.  De flowcharts zijn opgedeeld in de 2 hoofd taken die samen het volledige proces van het zagen regelen. Daarnaast zijn er ook een aantal functieblokken die in deze taken aangeroepen worden.

1. Taak 1: Zagen Materiaal  
  Deze taak regelt het zagen van het materiaal.

2. Taak 2: In- en Uitvoer van Materiaal  
Deze taak regelt het invoeren van het materiaal. Verder wordt de initialisatie gecontroleerd en eventueel uitgevoerd. Ook wordt vervolgens de uitvoer van het materiaal geregeld. 

3. Functie: Initialiseren Machine
Deze functie gaat over het in de juiste positie zetten van de machine aan het begin van de operatie. Als de machine wordt ingeschakeld, wordt eerst gecontroleerd of de juiste startpositie is bereikt. Zo niet dan wordt de invoer op de juiste positie gezet.

4. functie: Simulatie in- en uitvoer
Deze functie staat niet in een flowchart, maar zit wel in het programma. Dit is gedaan, omdat dit normaal niet in een zaagmachine zit. Dit stukje code is gemaakt om de visualisatie van het programma duidelijker te maken.


## Taak 1: Zagen Materiaal

```plantuml
@startuml Zagen

start
if (Systeem is ingeschakeld?) then (Ja)
  
    if (Aanvoer in positie en zaag gestart?) then (Nee)
        :Toon status: "Voer eerst een lengte in";
    else
        :Start zaagmotor;
        repeat
            :Toon status: "Zaag actief";
        repeat while (Eindaanslag zaag bereikt?) is (Nee) not (Ja)
            :Stop zaagmotor;
            :Set zagen voltooid;
       
    endif

else (Nee)
    :Schakel zaagmotor uit;
endif
stop

@enduml
```


## Taak 2 in en uitvoer van materiaal.
```plantuml
@startuml In- en uitvoer

start
if (Systeem is ingeschakeld?) then (Ja)
  repeat
  :Initialisatie bezig;
  repeat while (Initialisatie voltooid?) is (Nee) not (Ja)
    
  :Toon status: "Voer de zaaglengte in";
  :Start aanvoer;

      repeat
    :Taak in- en uitvoer bezig;
    repeat while (Zaaglengte bereikt aanvoerpositie en aanvoer gereed?) is (Nee) not (Ja)
      :Set aanvoer in positie;
      :Stop aanvoer;
      :Toon status: "Aanvoer in positie, druk op: 'Start zagen'";
    
     repeat
            :Taak zagen bezig;
        repeat while (Zagen klaar?) is (Nee) not (Ja)
            :Start uitvoer;
    
    :Sensor uitvoer is hoog;
    :Stop uitvoer; 
  else 
  :Stop aanvoermotor;
  :Stop uitvoermotor;
  
  endif

stop
@enduml
```


## Functie initialiseren van de zaagmachine.
```plantuml
@startuml Initialiseren

start

if (Controleer of de initialisatie nog niet voltooid is) then (Nee)

  if (Positie groter is dan 0 en initialisatie nog niet voltooid) then (Ja)
      :Stel status in op "Machine initialiseren";
  else
    :Set initialisatie voltooid;
    stop
  endif

    :Start invoermotor;
  repeat
   :Invoer nog bezig;
  repeat while (Huidige positie is gelijk aan 0) is (Nee) not (Ja)
        :Set initialisatie als voltooid;

else
stop
endif
stop

@enduml


```
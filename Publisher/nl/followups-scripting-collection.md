# Followups: collection variabele

Een collectie is een subset van een [database](./followups-scripting-database) en kan ook gebruikt worden 
in een datascript. Om een collectie object op te vragen kun je de documentatie
hierover vinden bij [het account object](./followups-scripting-copernica)

## Beschikbare eigenschappen

* **ID**: ID van de collectie (Read only)
* **name**: Naam van de collectie (Read and write)
* **created**: Tijdstip waarop de collectie is aangemaakt (Read only)
* **data**: Zie de documentatie over [de data variabele](./followups-scripting-data)
* **subprofiles** Een array met [subprofielen](./followups-scripting-data) in deze collectie. 
Het ID van een subprofiel kan als key gebruikt worden om een subprofiel object 
uit de array op te vragen (zie voorbeeld).

## Voorbeeld

Met het volgende voorbeeld in javascript kun je een subprofiel uit een 
collectie opvragen.

    <script> 
    
    var subProfileID = 54840;
    var someSubProfile = collection.subprofiles[subProfileID];
    
    </script>

## Meer informatie
* [Het data-script object](./followups-scripting)
* [Het data object](./followups-scripting-data)
* [Database variabele](./followups-scripting-database)
# Security vereisten

## Diagram: Dataflow

![Untitled](https://user-images.githubusercontent.com/48216176/187092215-71bd5630-74c3-4ae0-9f38-92a8526d9f6c.png)


## Toegangs regels:

als <rol> kan ik <een actie uitvoeren>

Admin:

- Als admin kan ik een gebruiker aanmaken
- Als admin kan ik een gebruiker bijwerken (deze functionalitiet is nog niet uitgewerkt in het programma)
- Als admin kan ik een gebruiker verwijderen

Root:

- als root gebruiker kan ik de logbestanden controleren

Gebruiker:

- als gebruiker kan ik uitloggen

Registrator:

- Als registrator kan ik een gebruiker registreren
- Als registrator kan ik een gebruiker herladen

Cashier:

- Als cashier kan ik een product verkopen aan een gebruiker
- Als cashier kan ik de statestieken van de verkoop bekijken

Loaner:

- Als loaner kan ik items uitlenen.

Bij de toegangs regels heb ik elke rol apart beschreven. Dit beteken dat een gebruiker van het systeem meerdere rollen kan hebben. 

## STRIDE analyse:

| Threat | Property violated | Threat | Voorbeeld in programma | oplossing |
| --- | --- | --- | --- | --- |
| Spoofing | Authenticity | Een aanvaller kan een rol aan nemen of zich voordoen als een rol dat niet voor hem bedoelt is.  | bij het creëren van een gebruiker of bij het inloggen. | Authentication of het gebruik van authenticatie software (Oauth of twee staps verificatie. Dit gebeurd aan het hand van rollen in ons programma |
| Tampering | Integrity | Een aanvaller kan data of code modificeren. | het verkopen van producten of uitlenen van een item | Encryptie van data. Er is geen encryptie in het programma |
| Repudiation | Non-repudiability | een aanvaller kan acties laten uitvoeren en dan laten uitblijken dat dit niet gebeurd is. | Bij het creëren van gebruikers of bij het verkoop van producten | Logging. In het programma worden transacties en ongewenste acties gelogd |
| Information disclosure | Confidentiality | Een aanvaller die aan informatie geraakt waarvoor hij niet geautoriseerd is. | Bekijken van de sales of de statestiek van de sales | Encryption and permissions. In het programma word er gewerkt met rollen/permissions. |
| Denial of service | Availability | Een aanvaller kan het programma offline halen door een denial of service attack | Bij het gebruik van het programma als het online of ergens draait op een server. | load balancers or more availability. Op dit moment is hier geen oplossing voor in het programma |
| Elevation of privilege | Authorization | een aanvaller kan aan de juiste autorisatie geraken. zonder hier correct voor geautoriseerd te zijn | Bij het creëren van een user. of bij het bijwerken van een user. | Autorisatie en het gebruik van rollen toepassen. Dit word in ons programma toegepast. |

 

## **Classificatie security risico's:**

Threats: 

- Spoofing
    - Impact: High
    - likehood: High
    - risk assessment: Critical. Als de aanvaller zich kan voor doen als admin heeft hij toegang tot heel te systeem. Buiten de log files
- Tampering:
    - impact: High
    - likehood: medium
    - risk assessment: high. Als de aanvaller gegevens kan aanpassen kan dit een ramp zijn voor het systeem. Bv aanpassingen van de prijzen of de balance van users aanpassen.
- Repudiation
    - impact: high
    - likehood: low
    - risk assessment Low. Als een aanvaller acties zou uitvoeren dat niet mag. Dan kunnen deze snel worden gevonden via het log systeem.
- information disclosure
    - impact: High
    - likehood: Low
    - risk assessment: Medium. Als een aanvaller alleen de gegevens kan bekijken van bijvoorbeeld de inlog zou dit een groot probleem. Daarom bij het creëren van de users worden de passwoorden met md5 en sha versleutelt. Dit beschermd de inlog gegevens. De waarschijnlijkheid is echter ook klein omdat de gegevens worden opgeslagen in een externe databank.
- Denial of service
    - impact: High
    - likehood: low
    - risk assessment: medium Als een aanvaller het systeem zou kunnen neerhalen met een dos aanval zou dit een groot probleem veroorzaken. Dit zou betekend het het systeem niet werkt?
- Elevation of privilege
    - impact: High
    - likehood: low
    - risk assessment: medium. Deze threat staat verbonden met de spoofing threat. Als een gebruiker zich kan voordoen of aan een admin account kan geraken dan kan hij zichzelf alle rollen geven. Hij moet hier voor wel eerst een account kunnen spoofen. Waardoor dat de likelihood daalt.

## aanbevelingen:

Spoofing threat: 

De huidige manier om authenticity te verzekeren is niet genoeg. De simple inlog voldoet niet meer aan de huidige industrie standaarden. Als aanpak raden we aan op om dit probleem aan te pakken. Onze aanbeveling zijn het installeren van authenticatie software zoals Oauth of multi-factor authentication zoals 2-step verification van google.

Tampering threat:

In het programma is er niks dat zich bezich houd met de tampering threat. Alle data wordt opgeslagen en door gestuurd in plaintext. Dit maakt het zeker handing voor een aanvaller om hier een kijkje in te nemen of een verandering hier op te doen. Als is de likelihood laag omdat de data op een externe database wordt opgeslagen. Als aanpak raden we aan om dit probleem aan te pakken. Dit kan door simpele encryptie toe te passen.

Repudiation threat.

In het programma wordt er logging toegepast. Dit zorgt er voor dat als er ongewenste actie worden uitgevoerd, we deze snel kunnen vinden en terug rechtzetten. Als aanpak raden we aan om dit te aanvaarden. De likelihood is klein en als er een probleem zou zijn. Zouden we dit snel terug vinden.

Information disclosure threat.

In het programma worden permissions of rollen toegepast om information disclosure tegen te gaan. Dit is één van de verschillende manier om deze threat tegen te gaan. Als aanpak raden we aan om nog meer dan de inlog gegevens te encrypteren. Dit zou zowel de information disclosure als repudiation threat aanpakken.

Denial of service threat. 

In het programma is er niks dat een dos aanval zou tegen gaan. Dit programma is gemaakt om lokaal te draaien en dus is de likelihood laag dat er een dos aanval zou zijn. Als aanpak raden we om dit te accepteren.

Elevation of privilege threat. 

In het programma wordt er gebruik gemaakt van rollen/permissions om deze threat tegen te gaan. Deze threat hangt wel samen met de spoofing threat. Als spoofing succesvol is dan kan de aanvaller ook zichzelf verschillende rollen geven. Als aanpak raden we aan om dit te accepteren. Het werken met rollen is genoeg om deze threat tegen te gaan.
 
 # security evaluatie

## De gebruikte test tools:

- DAST
    - owasp ZAP: werd toegepast om de meest voorkomende Owasp vulnerabilities te controleren.
 
    ![Untitled](https://user-images.githubusercontent.com/48216176/187092324-1ef56250-36cd-46f8-a631-3769030a17f3.png)

- SAST
    - semgrep: heeft geen findings gevonden. Werd toegepast om de source code te testen op potentiele vulnerabilities.
 
    ![Untitled 1](https://user-images.githubusercontent.com/48216176/187092334-1e0d6390-6ec6-4945-ba33-136c65e2a60d.png)

    
    
    - sonarQube: faalde om te runnen
    
    ![Untitled 2](https://user-images.githubusercontent.com/48216176/187092371-5275fad6-e27c-45f2-8bff-b5a4d5cc4a86.png)
    ![Untitled 3](https://user-images.githubusercontent.com/48216176/187092378-688c5e71-2f44-4940-901e-1094572220cf.png)

    
    - snyke werkte niet zonder composer (composer werd niet gebruikt in dit php project)

- SCA: Werd toegepast om vulnerabilities in de open source code te vinden.
    - dependabot: vond geen fouten want er wordt geen gebruik gemaakt van NPM dependancies
    
    ## De evaluatie
    
    **Bij de opdracht security werden volgende bevindingen gedaan:**
    
    - Spoofing:
        - threat: critical
        - oplossing: het installeren van authenticatie software zoals Oauth of multi-factor authentication zoals 2-step verification van google.
    - Tampering
        - threat: high
        - oplossing: Meer encryption toepassen
    - Repudiation
        - threat: low
        - oplossing: Het gebruik van logging. Dit wordt al toegepast in het programma
    - Information disclosure
        - threat:  medium
        - oplossing: Inlog gegevens encypteren. Het wachtwoord word geëncrypteerd bij het maken van een user
    - Denial of Service
        - threat: medium
        - oplossing: In de vereisten word aan geraken om dit zo te laten. Moest er toch een tijd komen dat dit programma om het web zou draaien raden we aan om een om een tussen programma te installeren dat helpt met mitigation en load balancing (bv. cloudflair)
    - Elevation of Privilege
        - threat: medium
        - oplossing: Er word gebruik gemaakt van rollen is het programma. Dit zou een goed genoeg verdediging moeten zijn tegen elevation of privilege.
        
    
    **Bij de evaluatie van ivm wachtwoorden werden volgende bevindingen gedaan:**
    
    - Bij het registeren van de gebruiker
        - is er geen limiet op de grootte van het wachtwoord.
        - er werd niet gechecket of een nieuw wachtwoord voorkomt in een databreach
    - Bij het aanmelden.
        - kan de gebruiker zijn of haar wachtwoord rechtsreek kopieren uit een wachtwoord manager.
    - toepassing verdediging van bruteforce or credential stuffing attacks
        - Er is momenteel geen verdediging tegen brute force attacks
    
    Mogelijk oplossing hier voor.
    
    - limieten zetten voor de grote van de wachtwoorden
    - het gebruik van multi factor authentication voor bruteforce attack
    - het gebruik van een cooldown timer voor bruteforce attacks
    
    **Bij de evaluaties van het afdwingen de toegangs regels werden volgende bevindingen gedaan:** 
    
    De toegangs regels worden in het programma correct afgedwongen. Als is er wel een threat met spoofing. Dit is een gemakkelijke manier om de huidige toegangs regels te omzeilen. Hiervoor zou best een authentication software voor gebruikt worden.
    
    **Bij de evaluatie ivm HTTPS werden volgende bevindingen gedaan.** 
    
    HTTPS wordt niet toegepast omdat dit programma bedoelt is om te draaien om het privé netwerk van Erasmus hogeschool Brussel. Zoals je kan zien bij de Owasp analyse zijn de headers niet correct
    
    **Bij de evaluatie ivm beveiliging tegen typische web vulnerabilities:**
    
    - Er wordt geen gebruik gemaakt van CSRF tokens om CSRF attacks tegen te gaan.
    - Er wordt geen gebruik gemaakt van cookies, alleen sessions.
    - Er wordt geen gebruik gemaakt van escaping en output encoding om XSS tegen te gaan.
    - Er wordt geen gebruikt gemaakt van CSP.
 
 

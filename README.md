
# Sichere Proragmming: Android Application Secure Design/Secure Coding


## **1 – Einführung**

Entwicklung einer sicheren Android-Applikation mit Fokus auf Secure Design und Secure Coding, einschließlich der Implementierung von Sicherheitsmechanismen wie Android Keystore, SSL/TLS-Verschlüsselung, Schutz vor SQL-Injektionen sowie Durchführung von Code-Reviews und Sicherheitstests zur frühzeitigen Erkennung und Behebung von Schwachstellen


**Wichtigste Vorteile:**

- Änderungen rückgängig machen
- Zusammenarbeit erleichtern
- Branching & Merging (für paralleles Arbeiten)

Studiengang Angewandte Informatik
Fakultät Angewandte Informatik

Projektarbeit

Kurs: Sichere Programmierung
Android Applikation – Sicheres Design / Sichere Login-Kodierung


vorgelet von: 
Aboudou Koffitse (00774763)=>Backend und Frontend
Chege Faith (00718759)     => Frontend
Suzana Stankovic (00725310)=> Frontend

---

#### Jury:

Dozent/in: Michael Heigl
Tag der Einreichung: 22. Januar 2020

---
Inhaltsverzeichnis
Abbildungsverzeichnis	III
1. Motivation	1
2. Benötigte Software	2
3. Sicheres Design	2
3.1 Grundlegende Kenntnisse	2
3.2 Anwendung von sicherem Design	3
5. Sichere Codierung – Login	5
5.2 Passwortanzeige	6
5.2-1 Passwortmaskierung	6
5.2-2 Passwortanzeige im Klartext	7
5.3 Bildschirmaufnahme deaktivieren	7
5.4 Fehlermeldungen	8
6. Firebase	8
6.1 Gültigkeit der Login-Daten	9
5. Fazit	11
6. Literaturverzeichnis	13

 
Abbildungsverzeichnis
Abbildung 1: Backup Erlaubnis	4
Abbildung 2: Regulärer Ausdruck zur E-Mail-Verifizierung	6
Abbildung 3: maskiertes Passwort	6
Abbildung 4: Firebase Implementierung	9
Abbildung 5: Firebase Instanziierung	9
Abbildung 6: Autentication	10
Abbildung 7: Realtime Database	10


1. Motivation

In der heutigen Zeit werden Smartphones immer wichtiger. Laut einer Studie, welche am 15. Januar 2020 in der Frankfurter Allgemeinen erschienen ist, verbringen Nutzer 3,7 Stunden täglich am Smartphone (vgl. FAZ, 2020). Bei Jugendlichen liegt diese Zahl sogar bei mehr als fünf Stunden. (vgl. PZ-news, 2019). Die meiste Zeit davon wird in sozialen Netzwerken verbracht Über diese sozialen Netzwerke teilen Benutzer viele persönliche Informationen. Doch, um überhaupt in der Lage zu sein, „Social Media“ zu benutzen, muss man zuvor ein Benutzerkonto erstellen. 
Bei der Registrierung werden die Nutzungsdaten kaum durchgelesen, sie werden einfach akzeptiert, ohne groß darüber nachzudenken. Doch Sicherheit sollte vor allem in der Technik eine große Rolle spielen. Persönliche Daten werden online gestellt und wie man weiß, was einmal im Internet ist, ist für immer im Internet. Die meisten Nutzer sind sich einer möglichen Unsicherheit entweder nicht bewusst oder es ihnen egal, was mit ihren Daten passiert. Sie haben volles Vertrauen in die Entwickler, dass sie die Programme, die sie verwenden sicher machen. 
Aus den vorangestellten Gründen haben wir es uns zur Aufgabe gemacht eine sichere Applikation zu entwickeln. Unser fertiges Produkt ist eine App, welche Einnahmen und Ausgaben miteinander verrechnet und den aktuellen Geldbestand berechnet und anzeigt. Wir sind uns der Sicherheit beziehungsweise, der Unsicherheit bewusst gewesen und haben uns stets Gedanken zur dieser gemacht. Viele Funktionen sind bewusst unsicher programmiert worden, um Probleme aufzuzeigen. 
Diese Arbeit setzt sich mit der Entwicklung dieser Applikation auseinander. Dabei wird zunächst die verwendete Software aufgelistet. Gefolgt von der genauen Beleuchtung der Aspekte des sicheren Designs und der sicheren Codierung beim Login. Der letzte Gesichtspunkt der Arbeit ist die Datenspeicherung mit der, von uns gewählten Datenbank, Firebase.  

2. Benötigte Software

Wir haben mit der Installation von Android Studio begonnen. Danach haben wir einen Emulator installiert, mit dem wir das Ergebnis der Anwendung nach der Kompilierung sehen können. Als Betriebssystem wurde Windows 10 verwendet. Daran wurden neben der Installation einiger Pakete und Programme keine weiteren Änderungen unternommen. Jetzt konnten wir mit der Implementierung beginnen. Diese wurde in drei Teile geteilt. Der erste war das Erstellen unseres Projektes mit dem Namen „NewApp“. Im zweiten Schritt haben wir uns der Konfiguration aller gewünschten Abhängigkeiten gewidmet. Zu guter Letzt kam das Initialisieren und Testen der fertigen Applikation. 

3. Sicheres Design

3.1 Grundlegende Kenntnisse

Zunächst sollte die Begrifflichkeit geklärt werden. Diese könnte, durch die Wortwahl, zu eventuellen Missverständnissen führen. Sicheres Design bezieht sich hierbei nicht auf das Aussehen des Codes oder der Applikation, wie es das Wort Design zu vermuten lässt. Unter sicherem Design ist eine sichere Denkweise zu verstehen. 
Ein Entwicklungsprozess wird häufig in vier Phasen unterteilt. In der ersten Phase, der sogenannten Spezifikations-Phase, werden alle Anforderungen und Voraussetzungen an das fertige Produkt gestellt. Die zweite Phase setzt sich mit dem Entwurf und der Implementierung auseinander. Hier wird das vorher spezifizierte ausprogrammiert. Die dritte Phase ist die Validierungsphase. Die letzte Phase bildet die Evolution. (vgl. Sandhaus, G. ,S.13). Wo genau wird hier sicheres Design angewendet? Ganz einfach. In allen Phasen der Entwicklung. Das Entwicklungsteam muss sich, zu jedem Zeitpunkt der Gefahren und Unsicherheiten bewusst sein und diese versuchen zu beseitigen. In jeder Phase können neue Gefahren festgestellt werden. Dabei ist wichtig zu wissen, dass Software schnell änderbar ist. Deswegen ist es umso wichtiger, dass man von Anfang an „sicher denkt“. Denn spätere Änderungen am Code können zu neuen Sicherheitslücken führen. 

3.2 Anwendung von sicherem Design 

Da wir uns an diese Voraussetzungen gehalten haben, können wir bei unserem Projekt von einer Applikation mit sicherem Design reden. Zunächst haben wir uns mit dem Thema Hacking auseinandergesetzt. Wir haben uns Gedanken darüber gemacht, auf welche Art und Weise unsere Software missbraucht werden kann. Dabei sind unter anderem die Aspekte sichere Kennworteingabe und Datenspeicherung aufgekommen. Wie bereits zuvor erwähnt gehen die Aspekte sicheres Design und sichere Codierung miteinander ein. Aus diesem Grund wurde hier eine klare Abgrenzung gesetzt und die beiden Thematiken werden genauer im Kapitel „Sichere Codierung - Login“ betrachtet. 
Des Weiteren haben wir uns mit der Kompatibilität auseinandergesetzt. Unter diesem Begriff steckt die Anzeige der Daten auf verschiedenen Geräten. Einerseits könnte so ein Unterschied zwischen Geräten mit verschiedenen Bildschirmgrößen, wie Tablets, Handys und Computern, herrschen. Um die Applikation auf verschiedenen Geräten verwenden zu können, muss diese Anzeige angepasst werden. Ein weiterer Unterschied liegt zwischen den Betriebssystemen. Eine App sollte sowohl auf einem Android als auch auf einem IOS Gerät auf die gleiche Art und Weise laufen.  
Zuletzt haben wir uns dem Aspekt der Berechtigungen, auf Englisch auch Permissions genannt, gewidmet. Es handelt sich um eine Android App, deswegen sollten wir zunächst die verschiedenen Funktionen betrachten. Vorangehend sollte klar gemacht werden, dass es eine Unterscheidung zwischen Funktionen, die das Smartphone und die App ausführen, gibt. Funktionen des Gerätes sind das Verwalten der Telefonnummer, Medien, wie beispielsweise Fotos oder Videos, oder Informationen zu Sensoren, wie z.B. den Standort. Funktionen einer Applikation hingegen können Kontakte, social Media Daten oder der Internetverlauf sein (vgl. Sawada et al., 2019, S. 20). Einige App-Funktionen brauchen wiederrum Zugriff auf die des Gerätes, um ihre eigenen Funktionen richtig ausführen zu können. Eine Navigations-App zum Beispiel braucht Zugriff auf den Standort des Gerätes, welcher vom Smartphone selber erfasst wird. Eine Große Sicherheitslücke bieten Backups. Wenn sich ein Hacker Zugriff auf ein Gerät macht, kann er durch diese mehr Daten erhalten, als er ohne Backup hätte finden können. 
  
Abbildung 1: Backup Erlaubnis
Abbildung 1 zeigt die Datei „AndroidManifest.xml“. Hier werden diese Permissions vergeben. Dabei sollte die Funktion des Backups ausgeschaltet werden. Wir haben den Wert hier auf True gelassen, um darauf aufmerksam zu machen, dass hier eine Sicherheitslücke besteht. 
Es sollte außerdem erwähnt werden, dass Android so konzipiert wurde, dass die meisten Entwickler in der Lage sein werden ihre Anwendungen mit den Standardeinstellungen zu erstellen und nicht mit schwierigen Entscheidungen der Sicherheit konfrontiert werden. Android verfügt nämlich über eine Reihe von Sicherheitsfunktionen, welche in das Betriebssystem integriert sind und die Häufigkeit von Sicherheitsproblemen reduzieren. 
[ Einige dieser Funktionen werden im Folgenden genauer erläutert. Die erste ist die Android-Anwendungs-Sandbox, welche Code-Ausführungen für jede Anwendung isoliert. Die zweite ist das Android-Applikations-Framework, welches gängige Sicherheitsfunktionen, wie Kryptografie, Berechtigungen und Inter-Process-Communication, implementiert. Drittens gibt es bestimmte Technologien, wie ASLR oder NX, die Risiken im Zusammenhang mit häufigen Fehlern bei der Speicherverwaltung minimieren sollen. Zuletzt gibt es auch ein verschlüsseltes Dateisystem, das aktiviert werden kann, um Daten auf einem gestohlenen oder verloren gegangenem Android-Gerät, zu schützen. ]
Mit diesen und vielen weiteren Sicherheitspraktiken sollten Android-App-Entwickler vertraut sein, um in ihre Anwendungen nicht vermeidbare Sicherheitslücken einzubauen. 

4. Gestaltung der Benutzeroberfläche

Die Benutzeroberfläche wurde sehr einfach gehalten. Sie zeigt ein Login Label mit zwei Text-Elementen für die Eingabe einer E-Mail und eines Passwortes. Das Layout enthält auch eine Schaltfläche, welche die Anmelde-Sequenz auslöst. Die Eingabefelder wurden dabei, unter Berücksichtigung der Input-Typen programmiert. Bei der E-Mail-Eingabe werden auch nur E-Mails akzeptiert. Außerdem haben wir uns an der Android-Bibliothek Material Design Components, kurz MDC, orientiert. Sie wurde von einem Team bei Google entwickelt. Diese bietet Entwicklern anhand eines zuverlässigen Entwicklungs-Workflows, Android-Applikationen implementieren zu können. Von dieser Bibliothek haben wir uns von einer Taste Gebrauch gemacht. Diese hat sich bei der Implementierung des Buttons und der Texteingaben als sehr nützlich erwiesen (vgl. introidx, 2020). 
 
5. Sichere Codierung – Login

Unter Login ist die richtige Eingabe von Daten zu verstehen. Diese Daten müssen zuvor registriert sein um, bei jedem Login-Versuch auf Richtigkeit geprüft werden zu können. Ist der Login erfolgreich, hat man Zugriff auf das dahinter befindliche Konto. Zum Login werden meistens ein Benutzername und das dazugehörige Passwort verlangt. 

5.1 E-Mail-Verifizierung

Zunächst wurde der Aspekt der E-Mail-Verifizierung erarbeitet. Die E-Mail wird für den Login benötigt. Diese Funktionalität wurde mit Hilfe von Regulären Ausdrücken, auch regular expressions, oder RegEx, genannt, erzielt. Regular Expressions überprüfen, ob eine Eingabe das richtige Format, welches für das Eingabefeld benötigt wird, hat. Von RegEx haben wir in der Vorlesung gehört und von dieser Funktionalität Gebrauch gemacht, um zu prüfen ob die eingegebene E-Mail korrekt ist. 
Dabei haben wir uns keine eigene RegEx erarbeitet, sondern eine von vielen aus dem Internet hergenommen. 
 
Abbildung 2: Regulärer Ausdruck zur E-Mail-Verifizierung
Abbildung 2 zeigt diese regular expression. Die erste Zeile erlaubt dem Benutzer die Eingabe von Klein- oder Großbuchstaben, Zahlen, Bindestrichen, Unterstrichen und Punkten. Das nächste ist das @-Symbol, welches in jeder E-Mail-Adresse enthalten sein muss. Der zweite Teil akzeptiert nur Kleinbuchstaben. Hier soll die Domain eingegeben werden.
Dabei haben wir uns keine eigene RegEx geschrieben, sondern eine von vielen aus dem Internet hergenommen. 
Es handelt sich hierbei nicht um eine vollständig korrekte RegEx zur Überprüfung von E-Mails. Es kann eine freiwählbare Domain angegeben werden. Die E-Mail-Adresse wird nicht auf vollständige Richtigkeit geprüft. 

5.2 Passwortanzeige

5.2-1 Passwortmaskierung 

Da das Passwort der wichtigste Teil des Logins ist, sollte dieses nicht zu sehen sein. Deshalb gibt es die Funktion der Passwortmaskierung. Hierbei werden die eingegebenen Zeichen lediglich als Sternchen angezeigt. Man kann also nur die Länge des Passworts erkennen, ohne zu wissen, was sich dahinter verbirgt. Diese Lösung gibt es schon sehr lange im Bankwesen, wo die vier-stellige Bank-PIN maskiert ist, damit andere Personen diese nicht sehen können und sich unbefugten Zutritt auf das Konto eines anderen gewähren.
 
Abbildung 3: maskiertes Passwort

Die obere Abbildung zeigt das maskierte Passwort an. Dieses ist nicht lesbar, wir wissen nur, dass es sich um eine Zeichefolge von sechs Zeichen handelt. Diese Funktionalität wurde durch Benutzung eines EditText-Elements erreicht. Der Parameter, der das Passwort speichert, ist vom Typ EditText. Dadurch ist man in der Lage, das Passwort verschlüsselt anzuzeigen.

5.2-2 Passwortanzeige im Klartext

Anders als beim Rechner, erfolgt die Passworteingabe am Smartphone nicht über eine physische Tastatur, sondern über den Touchscreen. Das Fehlen der Tasten führt des Öfteren zur Eingabe eines falschen Buchstaben, was eine richtige Passworteingabe erschwert. Das stellt jedoch kein großes Problem dar, solange es keine Richtlinien gibt, wie z.B. die Sperrung des Kontos nach fünf fehlerhaften Passworteingaben. Obwohl es diese Hürden zu überwinden gibt, nutzen die meisten Verbraucher soziale Netzwerke auf ihren Smartphones und wählen daher ein einfaches Passwort. Um den Benutzern die Möglichkeit zu geben, das eingegebene Passwort vor dem Absenden, noch einmal zu überprüfen, gibt es die Funktion, das Passwort im Klartext anzeigen zu lassen. Wenn diese Funktionalität gegeben ist, muss ein automatischer Abbruch dieser Anzeige implementiert sein. Beispiele hierzu sind, die Anzeige nur während der Berührung einer bestimmten Taste oder eine vordefinierte Dauer der Klartextanzeige. Hinzufügend sollte dem Benutzer auch eine Meldung angezeigt werden, welche vor einer Klartextanzeige warnt und erklärt, dass diese Funktion ein bestimmtes Risiko mit sich bringt (vgl. Sawada et al., 2019, S. 320). Denn hierbei handelt es sich um eine unsichere Funktion, die anderen Personen einen Blick auf das Passwort erlaubt und wurde nur aus Präsentationszwecken in unserer Applikation implementiert.

5.3 Bildschirmaufnahme deaktivieren 

Ein Risiko der Klartextanzeige kommt mit dem Erzeugen einer Bildschirmaufnahme, auch Screenshot genannt, einher. Android hat mehrere Möglichkeiten implementiert, einen Screenshot zu erstellen. Die erste Möglichkeit ist das gemeinsame Drücken der Ein/Aus-Taste und der Leiser-Taste. Eine andere Möglichkeit ist, das Wischen mit dem Handrücken, von links nach rechts, über den Bildschirm des Smartphones. Das Auslösen einer Bildschirmaufnahme kann deshalb auch versehentlich geschehen. Wird eine Aufnahme getätigt, während das Passwort eingegeben wird, wird dieses Foto in der Galerie, in einer Cloud oder sogar auf einem externen Speichermedium gespeichert. Von dort aus kann ein potenzieller Angreifer eventuellen Zugriff auf die Login-Daten bekommen. Diese Aufnahme könnte unter anderem auch während eines Backups gespeichert werden und durch einen Hacker-Angriff in die falschen Hände kommen. Deswegen ist es wichtig die Screenshot-Funktion in der Entwicklungsphase der Applikation auszuschalten.

5.4 Fehlermeldungen

Werden die Login-Daten falsch eingegeben, muss die Applikation eine Fehlermeldung anzeigen. Dabei ist wichtig zu beachten, dass dem Benutzer nicht gesagt wird, welche Eingabe fehlerhaft war. Ein negatives Beispiel hierbei lautet: „Falsches Passwort“. Ein Angreifer weiß nun genau, welches Feld fehlerbehaftet ist und könnte sich durch mehrmaliges ausprobieren verschiedener, möglicher Passwörter Zugriff auf das Benutzerkonto verschaffen. Deswegen wird nach der Eingabe falscher Login-Daten in unsere Anwendung folgende Fehlermeldung angezeigt: „Passwort oder E-Mail nicht korrekt“. Jetzt weiß der Angreifer nicht, welches Feld eine falsche Eingabe beinhaltet. Ein möglicher Zugriff ist hierbei nicht unmöglich, wird jedoch erschwert. 
6. Firebase
Da es sich bei unserer Anwendung um eine sichere Applikation handelt, muss die Datenverwaltung ebenfalls gesichert sein. Da wir in diesem Bereich zu wenig Erfahrung haben, haben wir uns gegen das Aufsetzen eines eigenen Servers und für die Datenbank Firebase entschieden. Die Database wurde von Experten, auf dem Gebiet der Sicherheit, entwickelt. Diese Voraussetzung muss jedoch nicht unbedingt für eine tatsächlich sichere Ausarbeitung sprechen. Firebase ist eine Backend-Lösung von Google, welche auf der Google Cloud basiert. Mit Firebase kann man Daten von IOS, Android oder Web Applikationen speichern. Für kleine Projekte, wie das unsere, reicht selbst die kostenlose Version, welche einfache und sichere Konfigurationen mit sich bringt. Um Firebase benutzen zu können, benötigt man lediglich ein Google-Konto. 
Ein weiterer Aspekt, der für die Benutzung von Firebase gesprochen hat, war die einfache Implementierung in unser Projekt. Um unsere Anwendung und die Datenbank miteinander benutzen zu können, mussten wir die App in der Firebase registrieren und wiederum in unserer Anwendung die vorgefertigte Firebase-Konfigurationsdatei hinzufügen. 
 
Abbildung 4: Firebase Implementierung

Diese befindet sich in der Datei „build.gradle“ und wird in Abbildung 3 gezeigt. Firebase bringt viele Bibliotheken mit sich und um diese und ihre Funktionen benutzen zu können muss man lediglich eine Instanz der Datenbank in den Code implementieren. Eine beispielhafte Instanziierung ist in Abbildung 4 zu sehen.
 
Abbildung 5: Firebase Instanziierung

6.1 Gültigkeit der Login-Daten

Die Login-Daten können über Firebase ganz einfach verwaltet werden. 
 
Abbildung 6: Autentication
Abbildung 5 zeigt alle Nutzer, die sich in die Applikation eingeloggt haben. Hierbei sieht man eine weitere Sicherheitsfunktion von Firebase. Die Nutzer-UID ist ein verschlüsselter Wert, welcher mit Hilfe einer Hashfunktion erstellt wurde. Jeder Benutzer bekommt seinen eigenen Wert, welcher nach erfolgreicher Registrierung für diesen erstellt wird. 
In der Registerkarte „Authentication“ gibt es auch andere Funktionen, wie die Sign-in Methode. Hier kann das Entwicklerteam entscheiden, auf welche Arten sich der Benutzer bei seiner App registrieren kann. Wir haben uns lediglich für eine Registrierung über E-Mail oder ein Google-Konto entschieden, da uns diese Aspekte am sichersten vorkamen. Andere Möglichkeiten sind der Login über Facebook oder Twitter. Sogar eine anonyme Registrierung ist möglich.
Die Firebase-Funktion „Realtime Database“ zeigt alle gespeicherten Daten an. Es werden selbst Daten, die in Echtzeit erstellt werden innerhalb von wenigen Millisekunden, dargestellt. ¬¬
 
Abbildung 7: Realtime Database

In Abbildung 6 ist zu sehen, welche Daten eingegeben wurden. Auch hier wird mit Hashwerten gearbeitet. Aus dieser Darstellung sind keine wichtigen Daten zu erkennen. Alle verschlüsselten Daten hätten auch anders dargestellt werden können. Wenn wir bei der Implementierung die Möglichkeit der Vergabe einer eigenen Identifizierung gegeben hätten, wäre diese hier angezeigt. Da dies nicht der Fall war, erstellt Firebase einen gehashten Wert. Selbst wenn sich jemand unbefugten Zugriff auf die Firebase machen sollte, wird diesem die Datenbeschaffung erschwert.
Unter der Realtime Database-Funktion können auch Regeln aufgestellt werden. Diese Regeln verwalten die Schreib- und Lesezugriffe auf die Daten. Google hat hier eine Testfunktion direkt in die Firebase integriert, mit der es möglich ist die Zugriffsfunktionen zu testen. 
Es gibt noch viele andere Funktionen, die von Firebase zur Verfügung gestellt werden. Für die Datenverwaltung unserer Applikation reichen die genannten jedoch aus, deswegen werden wir auch nicht weiter auf die Funktionalitäten von Firebase eingehen.
Erweiterte Nachforschungen, was Firebase angeht, wurden leider erst im Nachhinein vorgenommen. Dabei sind wir auch einige Artikel gestoßen, die besagen, das Firebase nicht sicher ist (vgl. tweakPC, 2019). Dadurch, dass wir unsere Datenverwaltung an Firebase ausgelegt haben, gibt es keine Datenerfassung unsererseits. Dieser Aspekt steht im Konflikt mit sicherer Programmierung. Und wie sich herausgestellt hat, lagen wir mit unseren Befürchtungen richtig, dass Firebase nicht so sicher ist, wie sie denn Anschein macht.
Wegen der vorher angeführten Aspekte, gibt es bestimmt bessere Arten der sicheren Datenverarbeitung, wir wollten jedoch nicht zu viel Zeit in die weitere Suche oder eigene Implementierung dieser Funktion setzen und mit der Codierung unserer Applikation beginnen. Deshalb sind wir bei Firebase geblieben.  

5. Fazit

Wir haben sehr viel Zeit in die Ausarbeitung dieses Projektes investiert und hätten uns deshalb ein besseres Ergebnis gewünscht. Der zuvor aufgeführte Aspekt der Kompatibilität wurde nicht weiter realisiert als die Benutzung auf einem Android Smartphone. Eine weitere Funktion, dessen Realisierung leider nicht mehr erreicht wurde, war das Zurücksetzen des vergebenen Passwortes.
Dies verringert jedoch nicht den Lerneffekt und die Erfahrung, die wir aus der Erarbeitung des Projektes gewinnen konnten. Wir haben einen guten Einblick in Android Programmierung machen können. Als angehende Informatik-Studenten wird uns sichere Programmierung weiterhin begleiten. Bei unseren Recherchen waren wir sehr erstaunt, wie aktuell dieses Thema ist. Sichere Programmierung ist in vielen Bereichen vertreten und bietet verschiedenste Möglichkeiten. 
Abschließen wollen wir unsere Arbeit mit einem Dank an unseren Professor, der uns einen tollen Einblick in die sichere Programmierung vermittelt hat. Wir sind uns bewusst geworden, wie unsicher wir in der heutigen, digitalisierten Welt sind und auf wie viele Aspekte man bei der Erstellung einer sicheren Anwendung achten muss. Wir werden uns auch weiterhin mit der Thematik der sicheren Programmierung auseinandersetzen.  


6. Literaturverzeichnis

1. Introduction — Android Application Secure Design/Secure Coding Guidebook 2019-12-01 documentation (2019). Online verfügbar unter https://www.jssec.org/dl/android_securecoding_en/1_introduction.html, zuletzt aktualisiert am 19.12.2019, zuletzt geprüft am 19.01.2021​

2. https://www.geeksforgeeks.org/how-to-use-material-text-input-layout-in-android/​

3. Build your first app &nbsp;|&nbsp; Android Developers https://developer.android.com/training/basics/firstapp​

4. Secure your app &nbsp;|&nbsp; Android Developers https://developer.android.com/games/develop/safetynet?hl=en​

5. IDS03-J. Do not log unsanitized user input - SEI CERT Oracle Coding Standard for Java - Confluence (2021). ​

Online verfügbar unter https://wiki.sei.cmu.edu/confluence/display/java/IDS03-​

J.+Do+not+log+unsanitized+user+input, zuletzt aktualisiert am 19.01.2021, zuletzt geprüft am 19.01.2021.​

6. Android Secure Coding Standard - Android - Confluence (2021). Online verfügbar unter          
https://wiki.sei.cmu.edu/confluence/display/android/Android+Secure+Coding+Standard, zuletzt aktualisiert am ​

20.01.2021, zuletzt geprüft am 20.01.2021.​

​

7.    http://www.peterloos.de/index.php/android/m-menu-apps-with-cloud-interface/95-a-androidanothertodoapp​

8.   Firebase Logo: https://upload.wikimedia.org/wikipedia/commons/b/bd/Firebase_Logo.png​

9.   http://www.tutorialsface.com/2015/10/android-validating-email-edittext-sample-example-methods-tutorial/​

10.  https://www.tutorialspoint.com/how-to-check-email-address-validation-in-android-on-edit-text​

11. https://www.tutorialspoint.com/how-to-check-email-address-validation-in-android-on-edit-text


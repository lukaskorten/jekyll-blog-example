---
author: korten
---
In diesem Blog-Eintrag möchte ich dir zeigen, wie du in wenigen Schritten eine einfache „Hallo Welt“ Webanwendung mit Spring-Boot 2 und Wicket 8 aufsetzen kannst.

## Spring Boot
Für den Anfang brauchen wir eine saubere Spring-Boot-Anwendung. Die einfachste Möglichkeit ein Projekt mit Spring-Boot aufzusetzen ist die Nutzung der Website Spring-Initializr.

![Spring-Initializr](/assets/images/spring-initializr-screenshot.png)

Hier kannst du dir eine neue Spring-Boot-Anwendung mit wenigen Klicks zusammenstellen und als Zip-Datei herunterladen. Im oberen Bereich der Website gibst du über die entsprechenden Auswahllisten an, dass es sich hierbei um ein Gradle-Projekt mit Java und Spring-Boot in der Version 2.1.0 handelt. Unter Project-Metadata müssen die Bezeichner für die Group und das Artifact festgelegt werden, die zusammengesetzt standardmäßig das Default-Package deiner neuen Anwendung bilden. Über das Feld Dependencies können optional Abhängigkeiten zu verschiedenen Spring-Boot-Startern angegeben werden. Da wir uns zunächst auf die Erstellung einer einfachen Webanwendung beschränken wollen, reicht hier der Starter Web aus.  Mit dem Klick auf die Schaltfläche „Generate Project“ lädst du das frisch erstellte Projekt herunter.

Entpacke die heruntergeladene Zip-Datei in ein neues Verzeichnis deiner Wahl. Die Spring-Boot-Application kann jetzt schon gestartet werden. Rufe dazu im Projektverzeichnis die Eingabeaufforderung auf und führe den folgenden Befehl aus:

```bash
D:\code-snacks\wicket-helloworld>gradlew bootrun
```

In wenigen Sekunden fährt der eingebettete Tomcat hoch und kann danach über `http://localhost:8080` erreicht werden.

## Projekt in IntelliJ importieren
Bevor du dich den Abhängigkeiten widmest, empfiehlt es sich das Projekt in eine Entwicklungsumgebung, wie z.B. IntelliJ (du kannst natürlich auch jede andere Entwicklungsumgebung nutzen), zu importieren. Wenn du den Quellcode in IntelliJ als Gradle-Projekt importierst, erhälst du unter anderem den Komfort, dass die Abhängigkeiten direkt aufgelöst und automatisch aus dem entsprechenden Repository heruntergeladen werden. Selbstverständlich kannst du das Auflösen von Abhängigkeiten auch manuell über die Eingabeaufforderung anstoßen (gradlew buildDependencies), was z.B. implizit stattfindet, wenn du die Anwendung mit dem Befehl gradlew bootRun laufen lässt.

## Wicket einbinden
Als Nächstes binden wir das Webframework Wicket in der Version 8.1.0 ein. Dazu muss der dependencies-Block in der frisch generierten build.gradle-Datei, die sich im Root-Verzeichnis des Projekts befindet, wie folgt angepasst werden:

```groovy
dependencies {
    implementation(
            'org.springframework.boot:spring-boot-starter-web',
            'org.apache.wicket:wicket-core:8.2.0'
    )
    testImplementation('org.springframework.boot:spring-boot-starter-test')
}
```

## HomePage implementieren
Nun brauchen wir eine Seite, auf der wir die Begrüßung „Hallo Welt“ ausgeben wollen. Lege also eine neue Java-Klasse mit dem Namen „HomePage“ (Sie soll auch als Einstiegspunkt unserer Anwendung dienen) im Default-Package an. Im gleichen Package, jedoch unter Resources, erstellst du eine HTML-Datei, die ebenfalls HomePage heißt. Dein src-Verzeichnis sollte nun wie in der folgenden Abbildung dargestellt aussehen:

```bash
├── src
│   ├── main
│   │   ├── java

```

Die exemplarische Implementierung der Klasse HomePage und das dafür benötigte Markup in der HomePage.html ist in den folgenden zwei Listings dargestellt:

```java
package de.korten.codesnacks.wickethelloworld;
 
import org.apache.wicket.markup.html.WebPage;
import org.apache.wicket.markup.html.basic.Label;
import org.apache.wicket.model.Model;
 
public class HomePage extends WebPage {
 
    public HomePage() {
        add(new Label("greeting", Model.of("Hallo Welt!")));
    }
}
```

```html
<!doctype html>
<html lang="de" xmlns:wicket="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Hallo Welt</title>
</head>
<body>
```

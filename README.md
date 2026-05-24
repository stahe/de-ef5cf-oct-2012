# Migration von NHibernate zu Entity Framework 5 (Oktober 2012)

Dieses Dokument beschreibt eine **flexible und skalierbare ASP.NET-Anwendungsarchitektur**
und zeigt, wie das ORM **NHibernate** durch **Entity Framework 5** ersetzt werden kann,
ohne die Anwendungsebene zu ändern.

🌐 Die zugehörige Website ist unter folgender Adresse erreichbar: https://stahe.github.io/de-ef5cf-oct-2012/

---

## Hintergrund

**Entity Framework** ist ein ORM (Object Relational Mapper), das ursprünglich von Microsoft entwickelt wurde
und im Juli 2012 als Open Source veröffentlicht wurde.

In einem Kurs zu ASP.NET basiert dieses Dokument auf einer mehrschichtigen Architektur,
die es ermöglicht, Technologien (ORM, DBMS) zu aktualisieren, ohne die Anwendung zu beeinträchtigen.

---

## Allgemeine Architektur

Das folgende Diagramm zeigt die in der Anwendung verwendeten Architekturen:

![ASP.NET-Architektur mit NHibernate und Spring.NET](https://stahe.github.io/ef5cf-oct-2012/images/10000000000007D200000183315F4E40.png)

![ASP.NET-Architektur mit Entity Framework 5 und Spring.NET](https://stahe.github.io/ef5cf-oct-2012/images/10000000000007D7000001825B1CF7DD.png)

### Beschreibung der Schichten

- **ASP.NET-Anwendung**  
  Präsentationsschicht und Geschäftslogik.

- **DAO (Data Access Objects)**  
  Von der Anwendung verwendete Schnittstelle für den Datenzugriff.

- **ORM (NHibernate / Entity Framework)**  
  Zuständig für die SQL-Generierung und die Kommunikation mit ADO.NET.

- **ADO.NET**  
  Konnektor zum DBMS.

- **DBMS**  
  Datenbankmanagementsystem.

- **Spring.NET**  
  Gewährleistet die Integration der Schichten und die Abhängigkeitsinjektion.

---

## Warum ein ORM verwenden?

Die direkte Verbindung der DAO-Schicht mit ADO.NET macht die Anwendung vom DBMS abhängig:

- Unterschiede bei den Datentypen;
- proprietäres SQL;
- DBMS-spezifische Bibliotheken.

Mit einem ORM kommt ein Wechsel des DBMS im Wesentlichen einer **Änderung der Konfiguration** des ORM gleich.
Die DAO-Schicht bleibt unverändert.

---

## Rolle von Spring.NET

Spring.NET ermöglicht:
- die Erstellung dieser Ebene aus einer Konfigurationsdatei;
- das Ersetzen einer DAO-Implementierung durch eine andere **ohne Änderung des Codes**,
  vorausgesetzt, die Schnittstelle bleibt unverändert.

---

## Zweck dieses Dokuments

In der Praxis zu zeigen, dass die Architektur:

- **resilient gegenüber Änderungen im DBMS** ist;
- **resilient gegenüber Änderungen im ORM** ist;
- **den Austausch von NHibernate durch Entity Framework 5** ermöglicht,
  ohne die ASP.NET-Anwendungsschicht zu ändern.

---

## Verfolgter Ansatz

Die Migration erfolgt in mehreren Schritten:

1. Erkundung von **Entity Framework 5** mit verschiedenen DBMS;
2. Erstellung einer neuen Datenzugriffsebene (**DAO2**);
3. Anbindung der bestehenden ASP.NET-Anwendung an diese neue DAO-Ebene.

---

## Zielgruppe
- ASP.NET-Entwickler;
- Studierende und Dozenten der Softwarearchitektur;
- Alle, die sich für entkoppelte und skalierbare Architekturen interessieren;
---
## Lizenz und Nutzung;
Lehrdokument für den Unterricht und zur Demonstration;
von skalierbaren Anwendungsarchitekturen.

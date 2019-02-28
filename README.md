# 2019-02-steuern

## Vorbemerkungen

SRF Data legt Wert darauf, dass die Datenvorprozessierung und -Analyse nachvollzogen und überprüft werden kann. SRF Data glaubt an das Prinzip offener Daten, aber auch offener und nachvollziehbarer Methoden. Zum anderen soll es Dritten ermöglicht werden, auf dieser Vorarbeit aufzubauen und damit weitere Auswertungen oder Applikationen zu generieren.  

Die Endprodukte des vorliegenden Scripts, neben der vorliegenden explorativen Analyse, sind (Datenbeschreibung siehe unten):

* `cities.csv`: Ausgabenstruktur der Mitglieder des Schweizer Städteverbands
* `cantons.csv`: Ausgabenstruktur der Kantone
* `municipalities_by_canton.csv`: Ausgabenstruktur der Gemeinden pro Kanton
* `cantons_and_municipalities.csv`: Ausgabenstruktur der Kantone und all ihrer Gemeinden
* `federation.csv`: Ausgabenstruktur des Bundes
* `deltas.csv`: Abweichungen der Ausgaben von Schweizer Klein-, Mittel- und Grossstädte vom Durchschnitt

### R-Script & Daten

Die Vorprozessierung und Analyse wurde im Statistikprogramm R vorgenommen. Das zugrunde liegende Script sowie die prozessierten Daten können unter [diesem Link](https://srfdata.github.io/2019-02-steuern/rscript.zip) heruntergeladen werden. Durch Ausführen von `main.Rmd` kann der hier beschriebene Prozess nachvollzogen und der für den Artikel verwendete Datensatz generiert werden. Dabei werden Daten aus dem Ordner `input` eingelesen und Ergebnisse in den Ordner `output` geschrieben. 

SRF Data verwendet das [rddj-template](https://github.com/grssnbchr/rddj-template) von Timo Grossenbacher als Grundlage für seine R-Scripts.  Entstehen bei der Ausführung dieses Scripts Probleme, kann es helfen, die Anleitung von [rddj-template](https://github.com/grssnbchr/rddj-template) zu studieren. 


### GitHub

Der Code für die vorliegende Datenprozessierung ist auf [https://github.com/srfdata/2019-02-steuern](https://github.com/srfdata/2019-02-steuern) zur freien Verwendung verfügbar. 


### Lizenz

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons Lizenzvertrag" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Dataset" property="dct:title" rel="dct:type">2019-02-steuern</span> von <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/srfdata/2019-02-steuern" property="cc:attributionName" rel="cc:attributionURL">SRF Data</a> ist lizenziert unter einer <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Namensnennung - Weitergabe unter gleichen Bedingungen 4.0 International Lizenz</a>.

### Weitere Projekte

Code & Daten von [SRF Data](http://srf.ch/data) sind unter [http://srfdata.github.io](http://srfdata.github.io) verfügbar.

### Haftungsausschluss

Die veröffentlichten Informationen sind sorgfältig zusammengestellt, erheben aber keinen Anspruch auf Aktualität, Vollständigkeit oder Richtigkeit. Es wird keine Haftung übernommen für Schäden, die  durch die Verwendung dieses Scripts oder der daraus gezogenen Informationen entstehen. Dies gilt ebenfalls für Inhalte Dritter, die über dieses Angebot zugänglich sind.

### Datenbeschreibung 

#### `cities.csv`, `cantons.csv`, `cantons_and_municipalities.csv`, `federation.csv`, `municipalities_by_canton.csv`

| Attribut | Typ | Beschreibung |
|-------|------|-----------------------------------------------------------------------------|
| name | String | Name der Körperschaft (Kantonskürzel, Gemeindename) |
| id | String | Identifikationsnummer des Ausgabenbereichs (Vorsicht: 01 und 1 sind nicht dasselbe) |
| category | String | Name des Ausgabenbereichs |
| is_main | Boolean | Angabe: Ist diese Kategorie eine Hauptkategorie oder nicht |
| share | Numeric | Anteil dieses Ausgabenpunkts an den Gesamtausgaben als Dezimalzahl |
| bfs_id | Numeric | BFS ID der Gemeinde (nur in cities.csv) |

#### `deltas.csv`

| Attribut | Typ | Beschreibung |
|-------|------|-----------------------------------------------------------------------------|
| name | String | Name der Körperschaft (Kantonskürzel, Gemeindename) |
| id | String | Identifikationsnummer des Ausgabenbereichs (Vorsicht: 01 und 1 sind nicht dasselbe) |
| category | String | Name des Ausgabenbereichs |
| amount | Numeric | Angabe: Ist diese Kategorie eine Hauptkategorie oder nicht |
| type | Factor | Einteilung in drei Gruppen: Kleinstadt, Mittelstadt, Grossstadt |
| share | Numeric | Anteil dieses Ausgabenbereichs an den Gesamtausgaben als Dezimalzahl |
| average | Numeric | Durchschnittlicher Anteil dieses Bereichs über alle Gemeinden in dieser Gruppe |
| delta | Numeric | Abweichung dieser Stadt bzw. dieses Bereichs vom obigen Durchschnitt |


### Originalquelle

#### Steuerbelastung pro Person

&rarr; `input/SB-NP-alle-Gden_2017.xlsx`

Die Eidgenössische Steuerverwaltung ESTV veröffentlicht für jedes Jahr eine [Tabelle mit der Steuerbelastung](https://www.estv.admin.ch/estv/de/home/allgemein/steuerstatistiken/fachinformationen/steuerbelastungen/steuerbelastung.html#529360841) verschiedener Personen-Modelle für jede Gemeinde der Schweiz. Aufgrund dieser Prozentwerte berechnen wir für eineN Website-BenutzerIn, wie viele Franken Steuern er/sie insgesamt zu bezahlen hat.

Darin enthalten ist auch die Steuerbelastung durch die Direkte Bundessteuer. Diese ist schweizweit gleich für alle natürlichen Personen.


#### Steuerbelastung pro Einkommensgruppe

&rarr; `input/NP_2015_mitnull.xlsx`

Die dazugehörigen Tabellen der ESTV können auf [deren Website](https://www.estv.admin.ch/estv/de/home/allgemein/steuerstatistiken/fachinformationen/steuerstatistiken/direkte-bundessteuer.html#990744579) heruntergeladen werden. Kapitel: Statistische Kennzahlen > Natürliche Personen > Mit einer Belastung durch die direkte Bundessteuer. Sie liegen erst für bis und mit 2015 vor.


#### Effektive Steuerbelastung (nicht selbst berechnet)

&rarr; `input/Progression_Export_SRF.xlsx`

Von Kurt Schmidheiny haben wir die genannte Tabelle erhalten, um die Grafik in dem Working Paper [Effective Tax Rates and Effective Progressivity in aFiscally Decentralized Country](https://www.econstor.eu/bitstream/10419/130464/1/cesifo1_wp5834.pdf) Seite 18 nachzubilden. Sie zeigt, dass Reiche (Einkommen über 3 Mio CHF / Jahr) systeamtisch ihren Wohnsitz in Tiefsteuergemeinden verlegen und dass deshalb schweizweit gesehen, das Steuersystem nicht mehr unbedingt progressiv ist.


#### Steuerfüsse

&rarr; `input/steuerfuesse.csv`

Um zu eruieren, wie gross der Kantons- bzw. Gemeinde-Anteil an der Steuerbelastung ist, verwenden wir die Tabelle [Steuerfüsse der natürlichen Personen](http://www.estv2.admin.ch/steuerfuss/my_select_alle.php), die Teil des Steuerrechners der ESTV ist. Wenn die Gemeinde darin z.B. einen Steuerfuss besitzt von *119* und der Kanton einen Steuerfuss von **100**, so beträgt der Anteil der Gemeinde **100 / (100 + 119) = 45.6%** und der Anteil des Kantons entsprechend **54.4%**.

Da der Kanton jedoch **17%** der Direkten Bundessteuer behalten darf, da er für die Erhebung der Steuern der natürlichen Personen verantwortlich ist, addieren wir 17% der direkten Bundessteuer zum Kantonsanteil dazu.

##### Sonderall Wallis

&rarr; `input/tarifs/VS_bareme_Hilfstabellen/…`

In Wallis ist leider alles etwas komplizierter. Der Kanton und jede Gemeinde haben nicht einfach einen Steuerfuss, sondern einen Multiplikations-Faktor und einen Index. Der Index gibt an, nach welcher Progression die Steuern erhoben werden. Das führt dazu, dass je nach Höhe des Einkommens unterschiedlich viel Geld an die Gemeinde bzw. an den Kanton fliessen. Beide Werte werden anschliessend wird der definierte Wert mit dem Faktor multipliziert. Der Kanton hat im Moment einen Index von 160%.

Von der [Website des Kantons Wallis](https://www.vs.ch/de/web/scc/hilfstabellen-kanton-gemeinde) können wir die Tabellen als Textfiles herunterladen, in denen steht, mit wie viel Einkommen man bei welcher Indexierung wie viel Steuern bezahlt. Die Werte gelten «von 2008 bis heute» bzw. die Gemeindesteuer Tabellen gelten von «2012 bis 2017».

Der Ordner `tarifs` enthält ausserdem noch PDFs zu der Ausgestaltung der Steuern in allen Kantonen. Diese PDFs werden in der Analyse nicht verwendet, aber können ev. von Hilfe sein, um kantonale Besonderheiten nachzuvollziehen.

#### Ausgaben nach funktionaler Gliederung

&rarr; Tabellen im Ordner `input/zip_d_2016`

Die ESTV publiziert ausserdem für den Bund, alle Kantone und alle Städte im Schweizerischen Städteverband (über 150 Gemeinden) eine [detaillierte Berichterstattung über deren Finanzen](https://www.efv.admin.ch/efv/de/home/themen/finanzstatistik/berichterstattung.html). Darin befinden sich bei allen Ebenen die beiden Tabellenblätter **ord_ausgaben_funk** und **ord_einnahmen_funk**. Dies ist die sogenannte «funktionale Gliederung». Sie besteht aus 10 Haupt und ca. 70 Unterkategorien. Wir haben uns entschieden, mit dieser Einteilung zu arbeiten, da sie mit für Laien leicht verständlichen Kategorien arbeitet. Es ist nicht immer einfach, die Kosten des Staates in diese Kategorien zu unterteilen. Wir sind uns bewusst, dass nicht jede Gemeinde / jeder Kanton die funktionale Gliederung genau gleich vornimmt. Sie ist jedoch die zuverlässigste und vollständigste Sammlung der föderalen Schweizer Staatsfinanzen.

Haben in einem Punkt die Einnahmen die Ausgaben überstiegen (für den Staat also ein Plus resultierte), haben wir dieses Plus nicht beachtet und die Einnahmen durch null ersetzt, da wir ja nur an den Ausgaben interessiert waren.

Die Abkürzungen bedeuten folgendes:

- **fs_bund**: Zahlen des Bundes (inkl. Vergangenheit)
- **fs_staat**: Summierte Zahlen Gemeinden plus Kantone plus Bund (inkl. Vergangenheit)
- **fs_ktn**:	Zahlen der Kantone (inkl. Vergangenheit)
- **fs_ktn_gdn**: Summierte Zahlen Gemeinde plus Kanton (inkl. Vergangenheit)
- **fs_gdn**: Zahlen der Gemeinden

Im Ordner zu den Gemeinden gibt es einerseits summierte Zahlen aller Gemeinden in einem Kanton (inkl. Vergangenheit). Dazu kommt jedoch eine weitere Tabelle mit allen Kantonshauptorten bzw. allen Städten im Städteverband. (ohne Vergangenheit)


##### Städte im Städteverband

&rarr; Tabellen im Ordner `input/stdt_vgl`

Da wir mit den Zahlen der Städte Analysen machen, haben wir vom [ESTV](mailto:finstat@admin.ch) zusätzlich die Zahlen der Jahre 2010-16 erhalten.


#### Einwohnerzahlen

&rarr; `px-x-0102020000_201.csv`

Wir exportieren alle Gemeinden und alle Kantone und die Schweiz von allen verfügbaren Jahren als CSV aus STATPOP: [Bilanz der Ständigen Wohnbevölkerung](https://www.pxweb.bfs.admin.ch/pxweb/de/px-x-0102020000_201/px-x-0102020000_201/px-x-0102020000_201.px). (Speichern unter «Textdatei, kommagetrennt (ohne Kopfzeilen)»)

Das BFS gibt folgendes zu bedenken: «Die Daten weisen den Gemeindestand per 31. Dezember des letzten produzierten Jahres aus. Zu beachten ist, dass die nicht mehr bestehenden Thurgauer Gemeinden 4505 Neukirch an der Thur, 4670 Illighausen und 4695 Scherzingen immer noch ausgewiesen werden, da eine rückwirkende Verteilung der Wohnbevölkerung für die Jahre vor 1994 nicht möglich war.»

Wir arbeiten für die Berichterstattung mit dem neusten verfügbaren Stand der Daten. Dies hat Vor- und Nachteile. Zum Beispiel sind im Jahr 2017 16 kleinere Gemeinden zur Gemeinde Bellinzona [fusioniert](https://de.wikipedia.org/wiki/Bellinzona#Geschichte). Diese kleineren Gemeinden können nicht mehr gefunden werden vom Benutzer, bzw. Bellinzona kann gefunden werden, war aber zum Zeitpunkt der Datensammlung 2010-16 noch kleiner als heute. 

Alles in allem ist es aber durchaus sinnvoll, dass wir mit dem neusten Stand der Gemeinden arbeiten, auch wenn die Zahlen zu den Ausgaben wie erwähnt von 2010 bis 2016 gehen. Fusionen betreffen, mit Ausnahme von Illnau-Effretikon, Wil, Glarus und Bellinzona vor allem kleinere Gemeinden, zu denen wir ohnehin keine Gemeindespezifischen Zahlen haben.

#### Gemeindenamen auf italienisch und französisch

&rarr; `be-b-00.04-agv-01.xls`

Namen für Gemeinden auf Italienisch und Französisch entnehmen wir dem [Amtlichen Gemeindeverzeichnis der Schweiz](https://www.bfs.admin.ch/bfsstatic/dam/assets/256599/master). Die Zuordnungen zu Gemeindenummern (BFS ID) wurde von Hand gemacht und in Tabelle `input/gemeindenamen_de_fr_it.csv` gespeichert.

Den Inhalt der Tabellen kann auch in diesem [öffentlichen Google Spreadsheet](https://docs.google.com/spreadsheets/d/1yr5QnebpmyH-2cJRD9bv66SnSJRFKxDk2lyU6ycZhI0/) betrachtet werden.


#### Raumgliederung

&rarr; `input/Raumgliederungen.xlsx`
&rarr; `klein_mittel_grossstadt.csv`

Die Einteilung der Städte in die Gruppen klein, mittel und gross haben wir der Raumgliederung des BFS entnommen (Gemeindetypologie 1980-2000, 22 Typen). Die Tabelle haben wir aus der [Applikation der Schweizer Gemeinden](https://www.agvchapp.bfs.admin.ch/de/typologies/query) des BFS exportiert.


#### BIP

&rarr; `input/je-d-04.02.01.08.xlsx`

In der einen Grafik im Skript (nicht jedoch in der öffentlichen Berichterstattung) haben wir das Brutto-Inlandsprodukt als Vergleich dazugezogen. Die Werte haben wir beim [Bundesamt für Statistik](https://www.bfs.admin.ch/bfs/de/home/statistiken/kataloge-datenbanken/tabellen.assetdetail.6067512.html) heruntergeladen.


#### Funktionale Gliederung

Um besser nachvollziehen zu können, was sich hinter den Begriffen der funktionalen Gliederung verbirgt, haben wir drei Word-Dokumente (de, fr, it) zu Rate gezogen, die von der Konferenz der kantonalen Finanzdirektorinnen und -direktoren stammen:

- `input/funktionale_gliederung/srs-cspcp_kontenrahmen_und_funktionale_gliederung_hrm2_v10_2017_12_14_aend_3.docx`
- `input/funktionale_gliederung/srs-cspcp_piano_contabile_ed_articolazione_funzionale_mpca2_v10_2017_12_14_modif_3.docx`
- `input/funktionale_gliederung/srs-cspcp_plan_comptable_et_classification_fonctionnelle_mch2_v10_2017_12_14_modif_1.docx`

Und deren Inhalt bezüglich der funktionalen Gliederung manuell in diese sechs Tabellen extrahiert:

- `input/funktionale_gliederung/unterkategorien_de.csv`
- `input/funktionale_gliederung/unterkategorien_texte_de.csv`
- `input/funktionale_gliederung/unterkategorien_fr.csv`
- `input/funktionale_gliederung/unterkategorien_texte_fr.csv`
- `input/funktionale_gliederung/unterkategorien_it.csv`
- `input/funktionale_gliederung/unterkategorien_texte_it.csv`

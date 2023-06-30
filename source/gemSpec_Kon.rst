=====================================
gemSpec_Kon
=====================================

.. note:: 
    Dieses Dokument dient als experimentelles Proof-of-Concept.
    Die hier bereitgestellten Informationen und Anforderungen stellen lediglich Testdaten dar und sind weder normativ noch rechtlich bindend.
    Die offiziellen normativen Dokumente der TI sind auf dem Fachportal der gematik verfügbar: https://fachportal.gematik.de

*...*

Systemüberblick
---------------

Der Konnektor ist ein Produkttyp der TI gemäß [gemKPT_Arch_TIP#5.3.9].
Er bietet seine Basisdienste sowohl intern den in ihm laufenden Fachmodulen an, als
auch externen Clientsystemen über die Konnektoraußenschnittstellen.
Im lokalen Netz der Einsatzumgebung kommuniziert das Clientsystem mit dem
Konnektor über dessen LAN-seitiges Ethernet-Interface. Alleinig der Konnektor
kommuniziert mit den in lokalen Netzen angeschlossenen Kartenterminals und Karten.
Auch die Kommunikation mit den zentralen Diensten der TI-Plattform und
fachanwendungsspezifischen Diensten erfolgt ausschließlich über den Konnektor über
dessen WAN-seitiges Ethernet-Interface.
Abbildung PIC_KON_116 stellt die Schnittstellen im Umfeld des Konnektors dar.

*...*

Übergreifende Festlegungen
--------------------------

Für die folgenden Inhalte bitte die Hinweise in Kapitel 1.5.3 „Erläuterungen zur
Spezifikation des Außenverhaltens" sowie Kapitel 1.5.4 Erläuterungen zur
Dokumentenstruktur und „Dokumentenmechanismen“ beachten.
In diesem Kapitel werden die Aspekte des Konnektors behandelt, die
Funktionsmerkmalübergreifend geregelt werden müssen.
Die Managementschnittelle/Administrationsoberfläche des Konnektors wird dabei nicht
als übergreifender Aspekt, sondern als eigenes Funktionsmerkmal gewertet. Die
Festlegungen hierzu finden sich entsprechend in Kapitel 4.3.

Allgemeine übergreifende Festlegungen
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Dokumentformate
~~~~~~~~~~~~~~~

Mit dem Aufruf einer Operation, die Dokumente verarbeitet, muss durch den Aufrufer
festgelegt werden können, um welches Dokumentenformat es sich handelt, damit die
unterschiedlichen Formate zur Verarbeitung und etwaigen Anzeige unterschieden werden
können. Die nicht-XML-Formate werden dabei nach MIME-Typ-Klassen unterschieden:

* „PDF/A” für MIME-Typ „application/pdf-a” gemäß [ISO 19005],
* „Text” für MIME-Typ „text/plain”,
* „TIFF“ für MIME-Typ „image/tiff” gemäß [TIFF6]
* „Binär“ für alle übrigen MIME-Typen.

Folgende Bezeichner werden verwendet:
Alle_DocFormate: XML, PDF/A, Text, TIFF, Binär
nonQES_DocFormate: XML, PDF/A, Text, TIFF, Binär
QES_DocFormate: XML, PDF/A, Text, TIFF
Für nonQES_DocFormate wird, trotz Gleichheit zu Alle_DocFormate, ein eigener
Referenzbezeichner verwendet, da sich diese Liste noch ändern könnte. TIFF wird durch
[gemKPT_Arch_TIP] nicht für die nonQES verlangt. Die Unterstützung dieses Formats für
nonQES bedeutet jedoch keinen Mehraufwand, da die Routinen durch QES bereits
implementiert sind und nachgenutzt werden können.


.. req::  TIP1-A_4500-02 - Dokumentgrößen von 25 MB
    :id: A_XYZ
    :status: open

    Der Konnektor MUSS für alle Außenschnittstellen, in denen ein Dokument verarbeitet
    wird, Dokumente mit einer Größe <= 25 MB (26.214.400 Byte) unterstützen. Der
    Konnektor DARF NICHT Dokumente mit einer Größe > 25 MB (26.214.400 Byte)
    unterstützen.[<=]

*...*

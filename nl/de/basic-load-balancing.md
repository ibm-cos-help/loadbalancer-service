---

copyright:
  years: 2017
lastupdated: "2017-08-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Basislastausgleich
Vom IBM Bluemix-Service für die Lastausgleichsfunktion wird der Datenverkehr auf mehrere Serverinstanzen (Bare-Metal-Server und virtuelle Server) verteilt, die sich lokal in demselben Rechenzentrum befinden.  

## Öffentliche Lastausgleichsfunktion 
Der Instanz des Service für die Lastausgleichsfunktion wird ein öffentlicher und vollständig qualifizierter Domänenname zugewiesen. Sie können diesen Domänennamen für den Zugriff auf die Anwendungen verwenden, die hinter dem Service für die Lastausgleichsfunktion gehostet werden. Die Back-End-Recheninstanzen, auf denen die Anwendung gehostet wird, müssen sich in einem privaten Netz in einer IBM Cloud befinden.  

**HINWEIS:** Es wird empfohlen, Back-End-Server ausschließlich privat bereitzustellen, sofern nicht eine direkte öffentliche Verbindung erforderlich ist. Dies sorgt für eine bessere Sicherheit und Ihre öffentliche IP-Adresse wird beibehalten. Die Anwendungen, die auf diesen Back-End-Servern gehostet werden, sind mithilfe der Lastausgleichsfunktion weiterhin über das öffentliche Netz verfügbar.   

## Ports bzw. Protokolle von Front-End- und Back-End-Anwendungen
Sie können bis zu zehn Ports (bzw. Protokolle) für Front-End-Anwendungen definieren und diese den entsprechenden Ports (bzw. Protokollen) auf den Back-End-Anwendungsservern zuordnen. Der vollständig qualifizierte Domänenname, der der Serviceinstanz für den Lastausgleich zugewiesen ist, und die Ports der Front-End-Anwendung sind öffentlich zugänglich. An diesen Ports werden die eingehenden Benutzeranforderungen empfangen.  

Die Back-End-Ports sind dagegen nur intern bekannt. Diese Back-End-Ports können mit den Front-End-Ports identisch sein, können aber auch abweichen. Beispiel: Die Lastausgleichsfunktion kann so konfiguriert sein, dass von ihr eingehender Web- bzw. HTTP-Datenverkehr an Front-End-Port 80 empfangen wird, die Back-End-Server sind jedoch am angepassten Port 81 empfangsbereit.  

Unterstützte Front-End-Ports bzw. -Protokolle sind HTTP, HTTPS und TCP. Unterstützte Back-End-Ports bzw. -Protokolle sind HTTP und TCP. Eingehender HTTPS-Datenverkehr muss an der Lastausgleichsfunktion terminiert werden, damit eine ungeschützte HTTP-Kommunikation mit dem Back-End-Server möglich ist.  

**HINWEISE:**

* Während der Erstkonfiguration können Sie nur maximal zwei Front-End-Ports definieren. Sobald eine Lastausgleichsfunktion erstellt ist, können Sie die Portkonfiguration bearbeiten, um zusätzliche Ports hinzuzufügen; das Maximum liegt bei 10 Ports. 
* Alle zehn Front-End-Ports müssen denselben Back-End-Serverinstanzen zugeordnet sein. 
* Die maximale Anzahl an Serverinstanzen, die sich hinter einer Lastausgleichsfunktion befinden können, beträgt 50. 
* Der Portbereich von 56.500 bis 56.520 für Verwaltungszwecke reserviert und kann nicht für virtuelle Front-End-Ports verwendet werden.  

## Lastausgleichsmethoden
Zum Verteilen des Datenverkehrs auf die Back-End-Anwendungsserver stehen die drei folgenden Lastausgleichsmethoden zur Verfügung: 

* **Round Robin:** 'Round Robin' ist die Standardmethode für den Lastausgleich. Bei Verwendung dieser Methode leitet die Lastausgleichsfunktion eingehende Clientverbindungen im Umlaufverfahren an die Back-End-Server weiter. Dies hat zur Folge, dass allen Back-End-Servern ungefähr dieselbe Anzahl an Clientverbindungen zugewiesen wird. 

* **Weighted Round Robin:** Bei Verwendung dieser Methode werden an die Back-End-Server die Anteile der eingehenden Clientverbindungen weitergeleitet, die der Gewichtung dieser Server entsprechen. Jedem Server wird eine Standardgewichtung von 50 zugewiesen, die auf einen Wert zwischen 0 und 100 geändert werden kann.  

	Beispiel: Es gibt die drei Anwendungsserver A, B und C, deren Gewichtung jeweils auf 60, 60 und 30 angepasst wurde; die Server A und B erhalten in diesem Fall dieselbe Anzahl an Verbindungen, während Server C die Hälfte der Verbindungen eines dieser Server erhält.  

	**HINWEISE:** 

	* Wenn für die Gewichtung eines Servers der Wert '0' eingestellt wird, hat dies zur Folge, dass keine neuen Verbindungen an diesen Server weitergeleitet werden, der vorhandene Datenverkehr fließt jedoch weiter, so lange er aktiv ist. Durch die Einstellung von '0' kann ein Server sanft heruntergefahren werden und als Ziel für die Services entfernt werden.  
	* Werte für die Gewichtung der Server können nur bei Verwendung der Methode 'Weighted Round Robin' angewendet werden. Sie werden bei Verwendung der Lastausgleichsmethoden 'Round Robin' und 'Least Connections' ignoriert.  

* **Least Connections:** Bei Verwendung dieser Methode erhält die Serverinstanz, von der zu einem bestimmten Zeitpunkt die wenigsten Verbindungen verarbeitet werden, die nächste Clientverbindung.  

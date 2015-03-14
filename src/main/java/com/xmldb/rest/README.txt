[BaseX 7.5]

Postoji nekoliko startup opcija u kojima BaseX moze da radi, nama od interesa su sledeca dva: 
	1. Kao standalone server baze podataka
	2. Kao web aplikacija deploy-ovana u okviru kontejnera

Ukoliko pre pokretanja primera iz paketa "com.xmldb.rest" BaseX75.war nije deploy-ovan (ne trci na localhost:8080/BaseX75), aplikacija ce pokrenuti 
lokalno standalone instancu BaseX servera. U tom slucaju treba podesiti ${rest.url} parametar "basex.properties" fajla na sledecu adresu 
"http://localhost:8984/rest/". U tom slucaju ce interna organizacija baze podataka biti cuvana negde u lokalu - tacna putanja bice ispisana u startup logu. 
Ovakav nacin pokretanja BaseX-a, medjutim, nije preporucljiv osim za test svrhe. 

Druga opcija je pokretanje BaseX-a sa kontejnerom (Tomcat, Jetty, TomEE, ...). U tom slucaju pre pokretanja primera neophodno je promeniti ${rest.url} 
na "http://localhost:8080/BaseX75/rest/", jer prilikom pokretanja primera nece biti pokrenuta nova instanca BaseX servera, vec ce konekcija biti uspostavljena 
ka vec postojecoj, na koju ukazuje ${rest.url}. U ovakvom rezimu rada lokaciju na kojoj ce biti cuvana interna organizacija BaseX baze podataka moze biti 
konfigurisana konteksnim parametrom web.xml fajla (BaseX75.war/WEB-INF/web.xml) na sledeci nacin:

	<context-param>
		<param-name>org.basex.dbpath</param-name>
		<param-value>WEB-INF/data</param-value>
	</context-param>
	
Putanja na kojoj ce u ovom slucaju biti fajlovi cuvani je relativna u odnosu na kontekst deploy-ovane aplikacije. 
Npr ${tomee.dir}/webapps/BaseX75/WEB-INF/data. 

Takodje je moguce zadati i apsolutnu putanju kao <param-value>, za parametar org.basex.dbpath na sledeci nacin:

	<context-param>
		<param-name>org.basex.dbpath</param-name>
		<param-value>D:/Development/data</param-value>
	</context-param>
	
Ostali konfigurabilni parametri koji ovde nisu spomenuti mogu se naci u BaseX-ovoj dokumentaciji na sledecoj adresi:

http://docs.basex.org/wiki/Options

--
Igor Cverdelj-Fogarasi
	


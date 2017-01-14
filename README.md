## Aprire un nodo openNET.io

Aprire un nodo è facile! La prima volta ci vorranno almeno 45 minuti se non di più, ma piano piano vedrai che diventerà davvero facile e sarai in grado anche tu di configurare un nuovo nodo in meno di un quarto d'ora. Se hai bisogno di aiuto scrivici a [help@opennet.io](mailto:help@opennet.io)! Vuoi un router già configurato per ogni necessità? Acquistalo da noi visitando il nostro store [opening soon!] o scrivendoci a [store@opennet.io](mailto:store@opennet.io). In ogni caso... benvenuto! :)

### 1. Trova un buon router da acquistare se già non ne hai uno

[In costruzione]

### 2. Installa openWRT

[In costruzione]

### 3. Trasforma il tuo router in un nodo mesh openNET.io

Scegli qui il tipo di dispositivo che stai configurando:

[Router standard "da tavolo" con più porte di rete [da due in su]](#router-standard)

[Router Ubiquiti AirMax o altro dispositivo con una sola porta di rete [wan e lan sulla stessa porta]](#router-ubiquiti)

[Non sei sicuro o hai un altro router?](#altri-router)

### 3.1 Router standard

Note: These instructions will (probably) work for most Atheros-based routers. Mediatek routers WILL NOT be able to support multiple SSID types. If your router uses a Mediatek chipset you must choose between the "Master" SSID type OR the "Ad hoc" SSID type (used by the mesh network itself).

3.1.0. Se hai seguito gli step precedenti, dovresti avere il tuo computer già collegato ad una porta lan del router [o _alla_ porta lan nel caso il tuo router ne avesse una sola].

3.1.1. Se non lo avessi già fatto, apri la pagina di amministrazione di openWRT del tuo router: [http://192.168.1.1](http://192.168.1.1). Se non dovessi vedere la pagina raffigurata nell'immagine qui sotto, apri invece la pagina [http://192.168.1.1/cgi-bin/luci](http://192.168.1.1/cgi-bin/luci).

<img src="https://static.wixstatic.com/media/d29986_7f72f1229e9747b583f8567e1b5172db~mv2.png/v1/fill/w_976,h_513,al_c,lg_1/d29986_7f72f1229e9747b583f8567e1b5172db~mv2.png" alt="" class="inline"/>

3.1.2. **Non** click "change password now" even though it looks like you're supposed to. Senza inserire alcuna password, clicka semplicemente "login".

3.1.3. Now click "change password now" and set your own password. Mind that you don't hit the enter key to submit the password as it won't save it. You need to click "Save and Apply" at the bottom of the page.

<img src="https://static.wixstatic.com/media/d29986_36fa8200deb54270be1f5a20a40fcc74~mv2.png/v1/fill/w_976,h_525,al_c,lg_1/d29986_36fa8200deb54270be1f5a20a40fcc74~mv2.png" alt="" class="inline"/>

3.1.4. Log back in. From here on out we will configure 8 general sections. They are:

+ System
+ Interfaces
+ WiFi
+ DHCP and DNS
+ Firewall
+ Packages and Command Line configurations
+ OLSR

The first 5 of these sections are found in the top-most dropdown menus in the router's interface:

<img src="https://static.wixstatic.com/media/d29986_a728f3094b8a4d73a93917a5e7b8a8e8~mv2.png/v1/fill/w_596,h_400,al_c,lg_1/d29986_a728f3094b8a4d73a93917a5e7b8a8e8~mv2.png" alt="" class="inline"/>

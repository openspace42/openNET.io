## Aprire un nodo openNET.io

Aprire un nodo è facile! La prima volta ci vorranno almeno 45 minuti se non di più, ma piano piano vedrai che diventerà davvero facile e sarai in grado anche tu di configurare un nuovo nodo in meno di un quarto d'ora. Se hai bisogno di aiuto scrivici a [help@opennet.io](mailto:help@opennet.io)! Vuoi un router già configurato per ogni necessità? Acquistalo da noi visitando il nostro store [opening soon!] o scrivendoci a [store@opennet.io](mailto:store@opennet.io). In ogni caso... benvenuto! :)

Hai due router da dedicare al progetto? Ancora meglio! Ripeti la procedura per entrambi i tuoi dispositivi facendo attenzione alle note sotto i vari step dove indichiamo "router 1" e "router 2" [in assenza delle quali va fatto su entrambi] e sarai operativo con tutti i tuoi dispositivi fin da subito! Hai più di due router? Fantastico! Dividili in gruppi di due ciascuno e segui le istruzioni come sopra e posizionali in luoghi fisicamente distinti per ampliare al massimo la copertura dei tuoi nuovi nodi openNET.io!

Le nostre istruzioni sono frutto di oltre un anno di ricerca nell'ambito delle reti mesh, da sempre ispirata e fondata sull'eccellente lavoro e dei nostri amici di [Commotion wireless](https://commotionwireless.net/), [Meta Mesh](http://www.metamesh.org/) [da cui abbiamo tratto gran parte di questo howto], e [Ninux](http://ninux.org/). Non saremmo mai arrivati dove siamo oggi non fosse stato per loro. Grazie davvero da tutto il team openNET.io!

### 1A. Trova un buon router da acquistare se già non ne hai uno

[In costruzione]

### 1B. Verifica la compatibilità del tuo router se lo hai già

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

3.1.00. Se hai seguito gli step precedenti, dovresti avere il tuo computer già collegato ad una porta lan del router [o _alla_ porta lan nel caso il tuo router ne avesse una sola].

3.1.01. Se non lo avessi già fatto, apri la pagina di amministrazione di openWRT del tuo router: [http://192.168.1.1](http://192.168.1.1). Se non dovessi vedere la pagina raffigurata nell'immagine qui sotto, apri invece la pagina [http://192.168.1.1/cgi-bin/luci](http://192.168.1.1/cgi-bin/luci).


<img src="https://static.wixstatic.com/media/d29986_7f72f1229e9747b583f8567e1b5172db~mv2.png/v1/fill/w_976,h_513,al_c,lg_1/d29986_7f72f1229e9747b583f8567e1b5172db~mv2.png" alt="" class="inline"/>


3.1.02. **Non** click "change password now" even though it looks like you're supposed to. Senza inserire alcuna password, clicka semplicemente "login".

3.1.03. Now click "change password now" and set your own password. Mind that you don't hit the enter key to submit the password as it won't save it. You need to click "Save and Apply" at the bottom of the page.


<img src="https://static.wixstatic.com/media/d29986_36fa8200deb54270be1f5a20a40fcc74~mv2.png/v1/fill/w_976,h_525,al_c,lg_1/d29986_36fa8200deb54270be1f5a20a40fcc74~mv2.png" alt="" class="inline"/>


3.1.04. Log back in. From here on out we will configure 8 general sections. They are:

+ System
+ Interfaces
+ WiFi
+ DHCP and DNS
+ Firewall
+ Packages and Command Line configurations
+ OLSR

The first 5 of these sections are found in the top-most dropdown menus in the router's interface:


<img src="https://static.wixstatic.com/media/d29986_a728f3094b8a4d73a93917a5e7b8a8e8~mv2.png/v1/fill/w_596,h_400,al_c,lg_1/d29986_a728f3094b8a4d73a93917a5e7b8a8e8~mv2.png" alt="" class="inline"/>


3.1.05. Se ancora non lo hai fatto decidi il tuo nickname da usare all'interno del progetto e abbrevialo in 4 lettere [ad es. Nikksno > NKSN]. Identifica il tuo dispositivo nella [lista dei dispositivi noti](#) per trovare il suo codice di 4 lettere. Se non fosse già listato scrivici a [help@opennet.io](mailto:help@opennet.io) così che possiamo stabilirne uno insieme.

3.1.06. Now go to System > System > Tab "Impostazioni Generali". Make the following changes.

Hostname:  Scrivi in questo campo il nome del tuo router nel seguente formato:

**OPNT-USRN-DVCC-DVCS**

dove **USRN** sta per l'abbreviazione del tuo nickname che hai deciso nello step precedente, **DVCC** sta per il codice del tuo router che hai trovato nello step precedente, e **DVCS** sta per il numero progressivo dei tuoi router dello stesso **DVCC** [ad es **URM2-0001** se è il primo tuo router della serie **URM2**, **URM2-0002** se è il tuo secondo **URM2**, e così via...]. Il mio primo nodo ad esempio si chiama **OPNT-NKSN-URM2-0001**.

Timezone: Scegli in questo campo il fuso orario "Europe/Amsterdam" [è il primo che appare premendo il tasto "E" sulla tastiera dopo aver clickato sul menù a tendina]

Provide NTP server: spunta la checkbox.

3.1.07. Ora vai nel Tab "Logging". Effettua le seguenti modifiche:

External system log server: 100.248.248.1

Click Save and Apply.

3.1.08. Ora vai in System > Administration sezione SSH Access > Dropbear instance. Effettua le seguenti modifiche:

Interface: unspecified

Port: 42022

Password authentication: rimuovi la spunta

Allow root logins with password: rimuovi la spunta

Gateway ports: spunta la checkbox

3.1.09. [opzionale - per utenti avanzati] Sezione SSH-Keys in fondo:

Genera sul tuo computer una public/private keypair con il comando [unix only] `ssh-keygen -t rsa -b 4096`. Rispondi alla domanda sul path dove salvare le due chiavi generate. Dopo copia la chiave pubblica con `cat /path/to/your-key_id_rsa.pub` e incollala nel campo di testo.

3.1.10. Premi Save and Apply.

3.2.00. (Section II: Interfaces) Now go to Network > Interfaces. Do the Following.

3.2.01. Find the **Bridged Lan** Interface. Copy (meaning highlight it and Ctrl+C) the **MAC Address** of that interface which looks like **E4:95:6E:40:81:51**. Now go to [Meta Mesh's IP Calculator](http://www.pittmesh.net/ipcalc) here and enter the MAC Address and press "Submit." This will automatically calculate three IP addresses for you. Write these down. You'll need them repeatedly throughout the rest of the configuration.

3.2.02. Setting up the Wireless Mesh Interface:

Click "Add new interface"
Name of the New Interface: mesh
Cover the following interface: Wireless Network: Master "OpenWRT" (lan)
Click Submit
IPv4 Address: (Enter the "Mesh IP Address" here)
IPv4 Netmask: Custom > enter 255.192.0.0
Click Save and Apply
Return to Network > Interfaces

3.2.03. Setting up the Ethermesh Interface:

Click "Add new interface"
Name of the New Interface: ethermesh
Cover the following interface: Ethernet Adapter: "eth0" (wan, wan6)
Click Submit
IPv4 Address: (Enter the "Ethermesh IP Address" here)
IPv4 Netmask: Custom > enter 255.192.0.0
Click Save and Apply
Return to Network > Interfaces

3.2.04. Setting up the LAN Interface:
Click "Edit" in the LAN section
IPv4 Address: (Enter the "WLAN IP Address" here)
Do not change the IPv4 netmask
DHCP Server: General Settings:
Start: 10
Limit: 253
Leasetime: 1h
Advanced Settings
Force: Checked
Click Save and Apply

3.2.05. You will now no longer be able to reach the router at 192.168.1.1. Wait about 10 seconds while your computer gets a new IP address from the router. You should be able to access the router at the new WLAN IP Address (which you, of course, wrote down). Enter that into your broswer and log back in.


<img src="https://static.wixstatic.com/media/d29986_062b018e3efd4efb8f6df1dad8180698~mv2.png/v1/fill/w_1020,h_697,al_c/d29986_062b018e3efd4efb8f6df1dad8180698~mv2.png" alt="" class="inline"/>


3.3.00. (Section III: WiFi) Now go to Network > WiFi. Click the Edit button in the "SSID: OpenWRT" section: Make the following changes.

3.3.01. Setting up the wireless radio and WLAN SSID. Nella sezione "Device Configuration":

Conferma i seguenti valori nella riga "Operating frequency". Correggili nel caso non fossero come segue:

Mode: N
Channel: 11
Width: 20 MHz

3.3.02. Nella sezione "Interface Configuration" > "General Setup":

ESSID: Scrivi "openNET.io" senza virgolette
Mode: conferma che l'opzione selezionata nel menù a tendina sia "Access Point"
Network: Uncheck "Mesh". Make sure only "LAN" is selected.

3.3.03. Nella sezione "Interface Configuration" > "Wireless Security":

Encryption: seleziona "WPA2-PSK" dal menù a tendina
Cipher: seleziona "Force CCMP (AES)"
Key: scrivi "Aurora42+" senza virgolette

Click "Save and Apply."
Click "Back to Overview"

3.4.00. Nella sezione "Wireless Overview" premi il pulsante "Add" sulla destra:

3.4.01. Nella sezione "Interface Configuration" > "General Setup":

ESSID: Scrivi "openNET.io | USRN-DVCC-DVCS" senza virgolette, sostituendo **USRN-DVCC-DVCS** con i tuoi codici esattamente come nello step 3.1.06.
Mode: conferma che l'opzione selezionata nel menù a tendina sia "Access Point"
Network: Seleziona "LAN"

3.4.02. Nella sezione "Interface Configuration" > "Wireless Security":

Encryption: seleziona "WPA2-PSK" dal menù a tendina
Cipher: seleziona "Force CCMP (AES)"
Key: scrivi "Aurora42+admin" senza virgolette

Click "Save and Apply."
Click "Back to Overview"

3.5.00. Nella sezione "Wireless Overview" premi il pulsante "Add" sulla destra:

3.5.01. Nella sezione "Interface Configuration" > "General Setup":

ESSID: Scrivi "openNET.io | 2411-W2PA-OLSR-4SXX" senza virgolette
Mode: seleziona l'opzione "Ad-Hoc"
Network: Seleziona "Mesh"

3.5.02. [Configureremo più avanti la crittografia WPA2-PSK CCMP su questa rete da riga di comando.]

Click "Save and Apply."
Click "Back to Overview"

3.6.00. (Section IV: DHCP and DNS) Now go to Network > DHCP and DNS. 

3.6.01. Make the following changes:

DNS Forwardings: scrivi "8.8.8.8" senza virgolette
Premi l'icona bianca con il "+" verde appena sulla destra della casella di testo. Scrivi "8.8.4.4" senza virgolette nella casella di testo che appare subito sotto la prima.

Click "Save and Apply"

3.7.00. (Section Hostnames) Now go to Network > Hostnames.

3.7.01. Fai le seguenti modifiche:

Nella casella di testo che vedi sulla sinistra digita: "thisnode" senza virgolette.
Nel menù a tendina subito a destra seleziona "-- custom --" e digita il WLAN IP precedentemente generato nella casella di testo che appare.

In basso a sinistra premi il pulsante "Add"

Nella casella di testo che appare sulla sinistra subito sotto la prima digita: "ck.opennet.io" senza virgolette.
Nel menù a tendina subito a destra seleziona "-- custom --" e digita "10.248.248.1" senza virgolette.

3.7.02. Premi "Save and Apply" in basso a destra.

----------------

[ancora in costruzione...]

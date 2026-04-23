# fordypning

# fordypning
Daglig loggCybersikkerhet (TryHackMe)
 Tirsdag (start)
I dag startet jeg med fordypningsoppgaven min. Jeg valgte cybersikkerhet og brukte TryHackMe.
Jeg lagde bruker og begynte på de første oppgavene. Jeg lærte:
•	Hva cybersikkerhet er
•	Forskjellen på å angripe systemer (offensiv) og beskytte systemer (defensiv)
•	Litt om forskjellige typer hackere
Jeg ble også kjent med hvordan siden fungerer.
________________________________________
 Onsdag
I dag jobbet jeg videre på TryHackMe.
Jeg lærte:
•	Hva en IP-adresse er
•	Hvordan datamaskiner snakker sammen på internett
•	Litt om nettsider og hvordan de fungerer
Det var litt nytt, men jeg begynner å forstå mer.
________________________________________
 Torsdag
I dag startet jeg med Linux på TryHackMe.
Jeg lærte noen enkle kommandoer:
•	ls for å se filer
•	cd for å gå inn i mapper
•	pwd for å se hvor jeg er
Jeg brukte også AttackBox og prøvde det selv.
________________________________________
 Fredag
I dag fortsatte jeg med Linux.
Jeg lærte:
•	Hvordan åpne filer
•	Hvordan finne ting på systemet
•	Litt mer øving på kommandoer
Jeg begynner å bli mer vant til å bruke terminal.
________________________________________
 Mandag
I dag jobbet jeg videre med sikkerhet.
Jeg lærte:
•	Hva som gjør et passord sterkt eller svakt
•	At hackere kan gjette passord hvis de er enkle
•	Hvorfor det er viktig med gode passord
Jeg føler jeg har lært mye denne uka og forstår mer av hvordan hacking fungerer.

Idag som er oppdrag vil jeg forsette og jobbe med databsen og legge inn det jeg har lært fra tryhackme sikkerheten til kundene mine. At ingen skal få passordet personligopplysninger osv
tirsdag skal forsette med databasen og koble den til flaksen min, men har fått feil meldinger flere ganger så må egentlig forsette med og feil søke.






og utføre:  Eksamenslogg – MariaDB + Flask prosjekt
 1. Installasjon av MariaDB
sudo apt update
sudo apt install mariadb-server mariadb-client

 Installerer database-server og klient.

 2. Starte database
sudo systemctl start mariadb
sudo systemctl enable mariadb
sudo systemctl status mariadb

 Starter databasen og gjør at den starter automatisk ved oppstart.

 3. Logge inn i database
sudo mariadb

eller

mysql -u root -p

 Logger inn som administrator.

 4. Opprette bruker for Flask
CREATE USER 'flaskuser'@'localhost' IDENTIFIED BY 'passord';
GRANT ALL PRIVILEGES ON testdb.* TO 'flaskuser'@'localhost';
FLUSH PRIVILEGES;

 Lager bruker og gir tilgang til databasen.

 5. Teste bruker
mysql -u flaskuser -p

 Tester at brukeren fungerer.

 6. Åpne for nettverk
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf

Endret:

bind-address = 0.0.0.0

Restart:

sudo systemctl restart mariadb

 Gjør databasen tilgjengelig fra andre maskiner.

 7. Firewall
sudo ufw allow 3306
sudo ufw status

 Åpner port 3306 for database-tilkobling.

 8. Finne IP
ip a

 Viser IP-adressen til serveren.

 9. SMARTE VERKTØY (VIKTIG PÅ EKSAMEN)
 history (viser hva du har gjort)
history

 Viser alle kommandoer du har brukt.

 history + grep (filtrering)
history | grep mariadb
history | grep mysql
history | grep ufw

 Finner kun relevante kommandoer.

 grep (søke i resultater)
systemctl status mariadb | grep Active
ss -tuln | grep 3306
cat /etc/passwd | grep abdi

 Filtrerer ut viktig informasjon.

 Lagre logg (veldig smart triks)
history > logg.txt

 Lager fil med alt du har gjort (kan brukes til dokumentasjon).

 Kombinert smart bruk
history | grep mariadb > mariadb_logg.txt

 Lagrer kun MariaDB-relaterte kommandoer.

 10. Flask kobling til database
import pymysql

conn = pymysql.connect(
    host="10.2.2.93",
    user="flaskuser",
    password="passord",
    database="testdb"
)

 Kobler Flask til MariaDB.

 11. Vanlige feil
Access denied → feil bruker/passord
Connection refused → firewall / bind-address
Can't connect → feil IP eller server ikke tilgjengelig
📊 12. Systemflyt (krokodille/diagram)
Flask app
   ↓
PyMySQL
   ↓
IP server
   ↓
Port 3306
   ↓
MariaDB
   ↓
Database

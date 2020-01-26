# MTTPP-Projekt

1. korak -> Instalacija Android Studio alata
Za izvođenje ovog koraka potrebno je imati unaprijed instaliran Android Studio.
Ukoliko nemate instaliran Android Studio, možete to učiniti putem linka u redu ispod
https://developer.android.com/studio/?gclid=CjwKCAiAjrXxBRAPEiwAiM3DQpGMo8wOGiVWPlU6M5GnsBLoqg2Q1C-OQTQSM-poSTJVfIrtHhARJxoChDEQAvD_BwE
Ukoliko ste već imali instaliran Android Studio, ovaj korak možete preskočiti.
  
2. korak -> Kreiranje virtualnog uređaja (mobitela u našem slučaju) unutar Android Studio alata
Potrebno je pokrenuti Android Studio. Nakon toga odabrati Tools -> AVD Manager. Nakon što se AVD Manager otvorio,
moguće je kreirati novi virtualni uređaj klikom na Create new virtual device. Otvara se prozor gdje je moguće odabrati
rezoluciju uređaja, naziv uređaja itd. Također moguće je kreirati i vlastiti hardver. Nakon odabira rezolucije i naziva uređaja,
potrebno je odabrati operacijski sustav na kojem će se vrtjeti Vaš virtualni uređaj (za ovaj projekt korišten je Android 9.0).
Ovim postupkom Vaš je virtualni uređaj kreiran. 
  
3. korak -> Dodavanje varijable okruženja ANDROID_HOME
Odaberite Start, zatim Upravljačku ploču > Sustav i sigurnost > Sustav. Zatim s lijeve strane odaberite "Dodatne postavke sustava". Otvara se prozor gdje je potrebno kliknuti na Varijable okruženja. Zatim se otvara ponovno novi prozor gdje je potrebno kreirati novu korisničku varijablu.
Odabiremo Novo... gdje pod naziv varijable unosimo ANDROID_HOME, a pod vrijednost putanju do Vaše Android Sdk mape. Odabiremo U redu te 
izlazimo  iz pokrenutih prozora.
Pomoć: Sdk mapu je moguće pronaći na disku gdje je instaliran Vaš Android Studio. 
Forma za primjer: C:\Users\Korisnik1\AppData\Local\Android\Sdk
Napomena: AppData mapa je inicijalno skrivena, u gornjem lijevom uglu potrebno je odabrati karticu Prikaz te označiti Sakrivene
          stavke. Također je preporuka ponovno pokrenuti računalo radi implementiranja korisničke varijable okruženja na razini OS.
  
4. korak -> Provjera postojanosti virtualnog uređaja 
Potrebno je otvoriti komandnu liniju (Start -> Naredbeni redak) te se prebaciti na putanju naredbom
cd C:\Users\Korisnik1\AppData\Local\Android\Sdk\platform-tools. Pritiskom na enter, trebao bi se ispisati emulator-id. Ukoliko 
se ne ispiše niti jedan emulator, znači da nije instaliran (pogledati 2. korak).
  
5. korak -> Pokretanje emulatora
Pokretanje emulatora moguće je provesti direktno iz Android Studia odabirom Tools > AVD Manager > Run. Također, emulator je moguće
pokrenuti i iz komandne linije na sljedeći način. Otvoriti komandnu liniju (Start -> Naredbeni redak). Prebacite se na putanju
naredbom cd C:\Users\Korisnik1\AppData\Local\Android\Sdk\emulator. Upišite naredbu emulator -avd -list-avds da bi ste dobili ispis 
postojećih virtualnih uređaja. Pokrenite emulator naredbom emulator -avd naziv virtualnog uređaja (npr. Huawei_Mate_20_Lite_API_28).
Emulator bi se trebao pokrenuti, u slučaju pogreške potrebno je pokrenuti emulator direktno iz Android Studio alata.

6. korak -> Instaliranje aplikacije za testiranje na virtualni uređaj
Potrebno je prebaciti putanju putem naredbe cd C:\Users\Korisnik1\AppData\Local\Android\Sdk\platform-tools. Kad je putanja prebačena,
naredbom adb -s emulator-id install C:\Users\Korisnik1\MTTPP\app-debug.apk pokrećemo instalaciju aplikacije koju želimo testirati.
Putanja C:\Users\Korisnik1\MTTPP\app-debug.apk je putanja do apk datoteke željene aplikacije za testiranje.
  
7. korak -> Pokretanje ADB poslužitelja za komunikaciju između Android uređaja i Appium alata
Potrebno je prebaciti putanju putem naredbe cd C:\Users\Korisnik1\AppData\Local\Android\Sdk\platform-tools. Kad je putanja prebačena,
naredbom adb start-server pokrećemo ADB poslužitelj koji će upotrebljavati Appium za slanje naredbi na Vaš Android uređaj.
  
8. korak -> Instalacija te pokretanje i postavljanje Appium alata
Informacije: Appium je "HTTP poslužitelj" napisan koristeći Node.js platformu i pogoni iOS i
             Android sesiju pomoću Webdriver JSON mrežnog protokola. Stoga, prije nego što inicijalizira
             poslužitelj aplikacija, Node.js mora biti unaprijed instaliran na sustavu.        
Ukoliko već imate instaliran Appium ovaj podkorak možete preskočiti. Potrebno je na linku  http://appium.io/ skinuti alat.
Prije inicijaliziranja Appium alata, Node.js mora biti unaprijed instaliran. Ukoliko ga nemate instaliranog, moguće ga je skinuti
putem linka https://nodejs.org/en/download/.
Nakon uspješne instalacije Appium alata otvara se prozor poslužitelja sa Start tipkom gdje su već inicijalno popunjena polja za host 
i port. Potrebno je ostaviti predefinirane postavke te pokrenuti poslužitelj klikom na Pokreni poslužitelj. Nakon pokretanja 
poslužitelja, otvara se novi prozor na predefiniranoj host adresi i portu te se prikazuje log poslužitelja. Za mogućnost istraživanja 
svojstava elemenata mobilne aplikacije potrebno je odabrati File -> New Session Window. Otvara se novi prozor gdje je potrebno unijeti
željene sposobnosti mobilnog uređaja i započeti novu sesiju. Unutar JSON Representation odjeljka, kliknuti na ikonu za uređivanje.
Unijeti svojstva na način naveden u primjeru ispod. 
Nakon unesenih svojstava potrebno je spremiti promjene te pokrenuti novu sesiju. Nakon otvaranja sesije, sve je spremno za pregled
svojstava elemenata aplikacije na Vašem emulatoru.
Napomena: inicijalno se koristi jedan slash \ kod putanja unutar sustava Windows. Potrebno je u app pod putanju staviti 
          dva slasha \\. Ujedno ovo je jedna od mogućih pogrešaka prilikom definiranja sposobnosti mobilnog uređaja.
    Primjer:
      {
        "app": "C:\\Users\\Korisnik1\\MTTPP\\app-debug.apk",
        "VERSION": "9.0",
        "deviceName": "emulator",
        "platformName": "Android"
      }
         
9. korak -> Instalacija i postavljanje Maven alata
Informacije: Maven se koristi za definiranje strukture projekta, ovisnosti, gradnje i upravljanja testom.
Za ispravan rad Maven alata potrebno je imati predinstaliran Java JDK 1.7 ili neku noviju verziju. Putem linka moguće je preuzeti 
Java JDK https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html. Nakon preuzimanja, potrebno je 
raspakirati mapu te postaviti JAVA_HOME varijablu okruženja. Slijediti postupak u koraku broj 3 gdje se postavlja varijabla 
ANDROID_HOME, dok je ovdje slučaj varijabla JAVA_HOME. Pod putanju vrijednosti korisničke varijable JAVA_HOME unosi se putanja
do vaše raspakirane JAVA JDK mape. Potrebno je spremiti promjene. Nakon postavljanja JAVA_HOME varijable, sve je spremno za 
postavljanje Maven alata. Također ga je potrebno preuzeti putem poveznice https://maven.apache.org/download.cgi 
Potrebno je raspakirati mapu te postaviti mapu unutar PATH varijable. PATH varijabla nalazi se među sistemskim varijablama.
Unutar PATH varijable potrebno je dodati novu varijablu sa vrijednosti putanje do raspakirane mape MAVEN alata.
Otvaranjem komandne linije te unosom naredbe mvn-v na lokaciji raspakirane mape MAVEN alata moguće je provjeriti da li je alat
uspješno instaliran ili ne. Ukoliko se ispiše verzija skinutog MAVEN alata, instalacija je uspješna. Također je preporuka nakon 
dodavanja varijabli ponovno pokrenuti računalo.
  
10. korak -> Instalacija i postavljanje IntelliJ alata
Potrebno je preuzeti IntelliJ alat putem linka https://www.jetbrains.com/idea/download/ 
Nakon instalacije, potrebno je pokrenuti alat te stvoriti novi Maven projekt odabirom File -> New -> Project -> Maven.
Zatim je potrebno ubaciti Appium i TestNG biblioteke u novi projekt (pom.xml) uz odabir enable auto-import opcije. Nakon što smo 
ubacili biblioteke potrebno je kreirati novu testnu klasu za testiranje Android aplikacije gdje će biti izvršeno nekoliko
testova na korisničkom sučelju. Za testiranje mog primjera potražite kod na GIT repozitoriju MTTPP-Projekt te kopirajte u navedenu .java klasu.
Pokrenite test desnim klikom na naziv klase uz odabir opcije Run za pokretanje testa. Ukoliko se kod izgenerira, otvara se 
emulator gdje napisani testovi bivaju prikazani. Nakon završetka testa ispisuje se koliko je testova prošlo/palo od strane alata
IntelliJ.

Opis mog testa:
Za testiranje sam koristio aplikaciju Radio Stanice. 

Test radi sljedeće:

1. Ulazi u aplikaciju Radio Stanice
2. Odabire prvi element lijevo (popis radio stanica po zemljama)
3. Odabire Hrvatsku 
4. Odabire Antena Radio Zagreb
5. Dodaje Antena Radio Zagreb u favorite (srce gore desno)
6. Zaustavlja Antena Radio Zagreb
7. Vraća se x3 puta unazad (back)
8. Inicijalno se nalazi na početnom zaslonu aplikacije, odabire drugi element (pretraga)
9. Odabire textbox (okvir) za upisivanje ključnih riječi za pretragu te unosi "narodni"
10. Odabire Narodni Radio
11. Postavlja Narodni Radio u favorite (srce gore desno)
12. Pomiče se na sljedeću stanicu prema ključnoj riječi (tipka udesno)
13. Vraća se x1 unazad
14. Ponovno se nalazi na početnom zaslonu aplikacije, odabire treći element (favorite)
15. Ulazi u element favoriti gdje je moguće vidjeti dvije unazad navedene radio stanice kao favorite
16. Vraća se x1 unazad
17. Izlazi iz aplikacije
18. Test je uspješno završen




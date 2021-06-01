# Informatikai rendszerek biztonságtechnikája

**Ajánlott irodalom:**
- [Buttyán Levente, Györfi László, Győri Sándor, Vajda István: Kódolástechnika, 2006 - crysys web változat – 6.](https://docplayer.hu/2525122-Kodolastechnika-2006-crysys-web-valtozat-6-kodolastechnika-buttyan-levente-gyorfi-laszlo-gyori-sandor-vajda-istvan-2006-december-18.html)
- [Buttyán Levente, Vajda István : Kriptográfia és alkalmazásai TYPOTEX ISBN 963-9548-13-8 *fizetős!*](https://www.interkonyv.hu/konyvek/buttyan-levente-vajda-istvan-kriptografia-es-alkalmazasai/)
- Virasztó Tamás : Titkosítás és adatelrejtés. Netacademia Oktatóközpont. ISBN 963-214253-5
- Nagy Sándor: Elektronikus leveleink védelme, Computerbooks, 2005.
- https://www.rejtjelezo.hu/

**Amit találtam irodalom:**
- [Hálózatok Biztonsága - Frész Ferenc, Kálovics Tamás, Puha Gábor](https://cmsadmin-pub.uni-nke.hu/document/vtkk-uni-nke-hu/halozatok-biztonsaga.original.pdf)

**Követelmények:**
- május 06 ZH
- szóbeli vizsga

--------------

## EA1 - alapok
- Tempest támadás
- **passzív támadás:** *lehallgatás* (evesdropping, wire-tapping), az érzékeny információ megszerzésére irányul, a támadó nem módosítja az átviteli csatorna tartalmát
- **aktív támadás:** a támadó beavatkozik a kommunikációba - A támadó maga is forgalmaz a csatornán.•üzenetmódosítás•megszemélyesítés,•visszajátszás•szolgáltatás megtagadás *(DoS ~ denialof  service)* típusú támadások
- IP spoofing: az ip cím meghamisítása - *Pl. egy IP címmel azonosított trusted host megszemélyesítése. Célja csak annyi, hogy egy kiskaput hagyjon maga után, amin keresztül már egyszerűen be tud jutni.* - *Pl. az A és B között fennáll egy TCP kapcsolat, amit C szeretne megszakítani. RST- reset connection*
  - **védekezés:** a tűzfalak bizonyos forrás IP címeket csak bizonyos irányból fogadnak el
- **smurf:** broadcast üzenetet küldünk az áldozatt felé - *a DoS családba tartozó támadás. A megtámadott gép nevében ICMP echo requestüzenetet küld egy irányított IP broadcast címre. Az üzenetet vevő gépek válaszukkal teletömik az áldozat gép hálózatát, de a sajátjukat is, így ők maguk is áldozatok.ICMP(Internet Control Message Protocol) az IP bővítése, lehetővé teszi hibaüzenetek, tesztcsomagok és az IP-vel kapcsolatos információs üzenetek létrehozását*
  - **védekezés:** a routerek IP broadcast-ot ne engedje-nek át, IP broadcast címre küldött ICMP echorequest-re a gépeink ne válaszoljanak!
- **SYN flood:** Ha a rosszindulatú C támadó az A nevében nagy mennyiségű SYN csomagot küld B-nek (a válaszokat C természetesen meg sem kapja), akkor ezzel kimeríti B erőforrásait és az nem lesz képes fogadni a valódi kéréseket. 
  - **Védekezés:** 
    - mikro blokkok használatával: a szabványos adatstruktúránál lényegesen kisebb helyet foglalunk le, és ha a kapcsolat kérés valódinak bizonyul, csak akkor foglaljuk le a szükséges erőforrásokat (10x annyi támadó csomagot bírunk el).
    - syn cookie használatával
- **Xmas, Ymas:** A TCP fejrészben az URG bittől balra levő két bitet 2003 májusában az IANA (Internet Assigned Numbers Authority) az ECN (Explicit Congestion Notification) mechanizmus céljára osztotta ki. A korábbi TCP implementációk azt várják el, hogy ez a 2 bit 0 értékű legyen. A bitek 0-tól különböző értékűre állításával és a TCP implementáció viselkedésének megfigyelésével a támadó információt szerezhet a TCP/IP protocol stack implementációjáról.
- **switchek támadása:** a switch táblájába betesszük a saját címünk is így megkapunk minden üzenetet mi is.
- **arp poisoning:** támadó kéretlen és hamis ARP *(címlekérdező protokoll)* válaszokat küld, amelyben a kérdéses IP címhez a saját MAC címét tünteti fel.
- **ICMP redirect:** ICMP redirect üzenettel egy router egy számítógép számára egy jobb útvonalat tud megadni. A támadó ezzel maga felé tudja irányítani a megtámadott gép forgalmát.
  - **Védekezés:** accept_redirectskikapcsolása.
- **RIP (Routing Information Protocol)távolságvektor hamisítása**: *RIP: distance-vector protokoll, mely egy célponthoz (hálózatok, subnet-ek, állomások, vagy a default router)táblázatában tárolja:* 
  1. A célpont IP címét.
  2. Az odavezető út költségét (egy csomagnak az adott link-en való átküldésének költsége alapján).
  3. Az odavezető út első router-ét.
  4. Időzítőket
- **Source route IP opció:** A forrás megadhatja, hogy adott IP című állomás felé mely routereken keresztül haladjon a csomag. Támadó: privát IP című hálózatok elérésére. *A C támadó az R1 routernek megmondja, hogy R2-n keresztül kell a csomagot küldenie. R2 privát IP címmel rendelkező hálózat gateway-e, a datagrammot már a cél IP cím alapján küldi a címzettnek. A visszaút: a támadó publikus IP címmel rendelkezik.*
  - **Védekezés:** accept_source_routekikapcsolásával lehet.
- **DNS (cache) ellen való támadás:** Kihasználja, hogy lejáraz ns.myisp.comáltal tárolt www.mybank.com TTL ideje 
- social engineering: a támadás az emberi megtévesztésen alapul
- reverse engeneering: amikor elhitetik az áldozattal, hogy ő a kezdeményező, pl *a bejelentett hiba miatt telefonálok*
- xss: a weboldalba beépített mezőkbe írunk `js` kódot vagy szerver oldali kódot és azt futtatjuk

### Informatikai rendszer
> az adatok kezelésére használt elektronikus eszközök, eljárások, valamint az ezeket kiszolgáló és a felhasználó személyekegyüttese
> 
> - Eszközök, módszerek és eljárások, illetve működtető személyzet, információfeldolgozási, tárolási, továbbítási funkciók megvalósítására létrehozott rendszere
> - Egymással szervesen együttműködő és kölcsönhatásban lévő elemek összessége

### Adatkezelés
> adatok gyűjtése, felvétele, tárolása, feldolgozása (megváltoztatása, átalakítása, összegzése, elemzése stb.), továbbítása, törlése, hasznosítása, és felhasználásuk megakadályozása.

### Az informatikai biztonság
> Az informatikai rendszer olyan – az érintett számára kielégítő mértékű – állapota, amelyben annak védelme az informatikai rendszerben kezelt adatok bizalmassága, sértetlensége és rendelkezésre állása, valamint a rendszer elemeinek sértetlensége és rendelkezésre állása szempontjából zárt, teljes körű, folytonos és a kockázatokkal arányos.
> - **bizalmasság:** az adat tulajdonsága, csak az arra jogosultak, csak a jogosultságuk szerint ismerhetik meg, használhatják fel, illetve rendelkezhetnek  felhasználásáról
> - **sértetlenség:** az adat tulajdonsága, az adat tartalma és tulajdonságai az elvárttal megegyeznek, ideértve, hogy az elvárt forrásból származik (hitelesség) és a származás megtörténtének bizonyosságát (letagadhatatlanság) is.
>   – Rendszerelem tulajdonsága, hogy a rendeltetésének megfelelően használható
> - **rendelkezésre állás:** az adat, illetve az informatikai rendszer elemeinek tulajdonsága, amely arra vonatkozik, hogy az arra jogosultak által a szükséges időben és időtartamra használható
> - **zárt védelem:** az összes releváns fenyegetést figyelembe veszi
> - **teljes körű:** a védelmi intézkedések a rendszer összes elemére kiterjednek
> - **folytonosság:** a védelem az időben változó körülmények és viszonyok ellenére is folyamatosan megvalósul
> - **kockázatokkal arányosság:** egy kellően nagy intervallumban a védelem költségei arányosak a potenciális kárértékke

### informatikai rendszer elemei
- A környezeti infrastruktúra elemei
- A rendszerelemekkel kapcsolatba kerülő személyek
- Hardver elemek
- Szoftver elemek (OS, menedzsment, alkalmazások, stb.)
- Adathordozók, adatok, dokumentumok •A kommunikáció elemei

### Sérülékenységek - környezeti elemek
> - Nem védett, helytelenül tervezett átviteli vezetékek
> - Cégen kívüli személyek (szállítók, látogatók, szerelők, stb.) bent tartózkodása
> - Nem felügyelt munkálatok az épületekben, vagy azokon kívül (ablaktisztítás, elektromos vagy telefonszerelés, építési munkálatok stb.)
> - Cégen belüli személyek szükségtelen bent tartózkodása
> - az informatikai berendezések nem védett helyzete (nyílt utcán, kerítés nélküli épületekben, a munkaidőn kívüli őrzés hiánya stb.)
> - A belépési biztonság hanyag kezelése (jelző berendezések kikapcsolása, nyitott ajtók stb.)
> - A védelmi berendezések működési módjának vagy gyengeségeinek jogosulatlanok általi megismerése (például a vezetékek lefutása, riasztórendszerek kapcsolási vázlatai, különösen pedig a számítógép-vezérelt belépés-ellenőrzés)

### Sérülékenységek - Hardver elemek
> - készülékek csekély mérete, súlya (lopás könnyen)
> - Érzékenység az elektromágneses sugárzással szemben
> - Kompromittáló kisugárzás lehetősége (például képernyőkről és rézkábelekről)
> - Ütésérzékenység 

### Sérülékenységek - Szoftverek 
> - Helytelen program-előállítás (specifikációs hiba)
> - A logikai belépés ellenőrzésének hiánya (felhasználó hitelesítés)
> - Az új vagy változtatott szoftverek nem kielégítő minősítő eljárása (implementálási hiba)
> - Bonyolult felhasználói felület
> - Az események hiányzó jegyzőkönyvezése (például belépés, CPU-használat, file-ok megváltoztatása)
> - A kódoló/titkosító algoritmus ismerete
> - A jelszó-táblák olvashatósága
> - jelszó-mechanizmus helytelen kezelése (gyenge jelszavak, változtatás hiánya stb.)
> - Felhasználó-felismerés jelszó nélkül vagy közös jelszavakkal
> - Szükségtelenül nagy hozzáférési jogok
> - más felhasználók ismeretlen programjainak használata (vírusfertőzés)
> - A "kilépés" elhagyása a termináltól való távozás esetén
> - Távolról történő karbantartás, adminisztráció

### Sérülékenységek – Adathordozók
> - Nem védett tárolás
> - Kapcsolható írásvédelem
> - Mágneses érzékenység
> - Érzékenység (hőmérsékletre, nedvességre stb.)
> - Adathordozók ellenőrizetlen használata
> - Könnyen szállíthatóak, mely nehezen ellenőrizhető
> - Szakaszos demagnetizálódás, elöregedés
> - Újrafelhasználhatóság elégtelen kezelése

### Sérülékenységek – Dokumentumok
> - A dokumentumok hiányzó adminisztrációja
> - Hiányzó változtatási szolgálat
> - Nem védett tárolás (tűz, lopás)
> - Nem kellő gondosság a kiselejtezésnél vagy megsemmisítésnél
> - Ellenőrizetlen sokszorosítási lehetőségek
> - A felhasználói dokumentáció közvetlen elérhetésének hiánya a felhasználó számára

### Sérülékenységek – Adatok
> - Hardver, szoftver hibák által keletkező adatvesztések, károsodások, eltérések
> - Hibás manuális adatbeadás/változtatás
> - Hibás futtatásvezérlés vagy kezelés (hibás utasítás vagy paraméter stb.)
> - Manuális program- vagy rendszermegszakítás
> - Jogosultak, jogosulatlanok általi törlés/változtatás (tévedésből/szándékosan)
> - Adatok jogosulatlan másolása

### Informatikai rendszerek biztonsága - Fizikai biztonság
> - védett átviteli vezetékek
>   – Beléptető rendszer (jelző berendezések, ajtók zárása, belépési jogosultság stb.)
> - Szabályozás 
>   – Belépés
>   – Cégen kívüli személyek (látogatók, szerelők, szállítók stb.) bent tartózkodása 
>   – Az épületekben, vagy azokon kívüli munkálatok felügyelete (ablaktisztítás, építési munkák stb.)
>   – Cégen belüli személyek bent tartózkodása
> - az informatikai berendezések védett elhelyezése, tartalék rendszerek
> - A védelmi berendezések működési információinak kezelése (pl. riasztó-rendszerek kapcsolási vázlatai, számítógép-vezérelt belépés-ellenőrzés)
> - Kisugárzás elleni védelem

### Informatikai rendszerek biztonsága - Kommunikáció biztonsága•Kriptológia
> **klasszikusan a titkos illetve védett kommunikáció tudománya**
> – **Kriptográfia:** algoritmikus módszerekkel biztosítja az üzenetek (tárolt információk) titkosságát vagy hitelességét. A passzív támadások megelőzésére és az aktív támadások detektálására törekszik.
> – **Kriptoanalízis:** a titok *- általában illetéktelen -* megfejtésére szolgáló módszerek tudománya.
> 
> **A kriptográfia főbb biztonsági szolgáltatásai**
> - **Titkosítás:** az üzenet kódolása, a megértéséhez szükséges dekódolást csak az arra illetékes felek tudják elvégezni.
> - **Integritásvédelem:** az üzenetet egy kriptográfiai **ellenőrzőösszeg**gel egészítjük ki, melyet csak az arra illetékes felek tudják kiszámolni. Így az üzenet tartalmát egy támadó nem tudja észrevétlenül módosítan
> - **Hitelesítés:** az üzenet küldőjének megbízható azonosítása. Detektálható, ha egy támadó más nevében próbál üzenetet küldeni.
> - **Letagadhatatlanság:** elérhető, hogy egy üzenet küldője később ne tudja letagadni, hogy ő küldte az üzenetet

## EA2-EA6 - Kriptológia
**Céljaink lehetnek:**
–Titkosítás
–Integritásvédelem (tartalom változatlansága)
–Hitelesítés *(feladó személye)*
–Letagadhatatlanság

![plain text to chipher text](https://notes.shichao.io/cnspp/figure_2.1.png)

### Szimetrikus kulcsú rejtjelezés
- a védettsége legfeljebb akkora mint a kulcs védettsége, rossz esetben elmaradhat tőle, ekkor a kulcs ismerete nélkül is lehet mondnai az információról valamit
- a kulcsot titokban kell kicserélni
> #### Kerckhoff-elv
> Titokban csak egy minél kisebb információt (kulcsot) kelljen tartani, NE az egész algoritmust 

> ### Támadó pzíciók 
> #### ismert rejtett szöveg alapú támadó
> csak a rejtett szöveget ismeri, de nem tudja milyen nyilt szöveghez tartozik
> #### ismert rejtett szöveg alapú támadó
> ismeri melyik rejtett szöveghez melyik nyilt szöveg tartozik
> #### választott nyílt szöveg támadás
> olyan nyilt szövegek amelyek többet árulnak el a szövegnél magánál és a rejtett szöveg továbbra is ismert

> #### oldalcsatornás támadás
> Az algoritmus fizikai jellemzői amik kinyerhetőek, *pl: egy processzor áramfelvétele függ attól, hogy mit csinál, és ha elég érzékeny műszerrel mérjük, akkor visszakövetkeztethető, hogy mit csinál a processzor, akár egyes bitek is kolvashatóak.* 

> #### feltételes biztonság
> Brute force támadás, ami alapvetően a legtöbb algoritmusra igaz. Ha nagy kulcsteret *(kulcstér = lehetséges kulcsok száma)* alkalmazunk akkor ez ellen részben védekezhetünk. **A nagy kuclstér viszont csak szükséges de nem elégséges feltétel!** 

> #### létezik feltétel nélküli biztonság
> azaz olyan titkosítás ami brute forceal sem feltörhető soha
> ```
> üzenet: x: 01101110100
> kulcs ~ random számsor: k: 00110111001
> 
> titkosítás ~ x XOR k = T: 01011001101
> dekódolás ~ T XOR k: 01101110100
> ```
> A `XOR` a `mod 2` összeadásnak megfeleltethető.

#### Történelmi példák
##### Caesar-kód - shift-kód
- Valahányal későbbi betűt vesszük ki az ábécéből az eredeti betű helyett
- ROT13 - k=13-al titkosított shift-kód

*kulcstér mérete = használt ábécé faktor => gyakorlatban az effektív használható bitek hosszát adjuk meg, azaz `log2 ábécé!`*

**homofóniás helyettesítés**, mikor nagy gyakoriságú betűket több betűnek feletetünk meg, pl a = a, és alpha, ésekkor az olvasó is ezeket helyettesíti vissza, így betűgyakoriság alapján történő kriptoanalízis nem lehetséges.

##### Vienére-féle módszer
használjuk az alábbi táblázatot úgy, hogy a bemeneti szöveg `x: TAMADJESZAKROL`, a kulcs egy tetszőleges szó, pl `kutya`, ekkor ezt kapjuk:
```
KUTYAKUTYAKUTY
TAMADJESZAKROL
```
Ekkor a nyílt szöveg minden egyes karakterét azzal a monoalfabetikus helyettesítővel kódoljuk amit a fölötte levő szöveg kijelöl az alábbi táblázatban.
```
  A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
A A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
B B C D E F G H I J K L M N O P Q R S T U V W X Y Z A
C C D E F G H I J K L M N O P Q R S T U V W X Y Z A B
D D E F G H I J K L M N O P Q R S T U V W X Y Z A B C
E E F G H I J K L M N O P Q R S T U V W X Y Z A B C D
F F G H I J K L M N O P Q R S T U V W X Y Z A B C D E
G G H I J K L M N O P Q R S T U V W X Y Z A B C D E F
H H I J K L M N O P Q R S T U V W X Y Z A B C D E F G
I I J K L M N O P Q R S T U V W X Y Z A B C D E F G H
J J K L M N O P Q R S T U V W X Y Z A B C D E F G H I
K K L M N O P Q R S T U V W X Y Z A B C D E F G H I J
L L M N O P Q R S T U V W X Y Z A B C D E F G H I J K
M M N O P Q R S T U V W X Y Z A B C D E F G H I J K L
N N O P Q R S T U V W X Y Z A B C D E F G H I J K L M
```
így kapjuk:`DUGYD....`

**A módszer algoritmikus gyengesége** a kulcsfelhasználás ciklikussága, azaz ismétlődik a kódoló karakter, pl `k` val van kódolva`T`, `J`, `K` is. 

**Kasiski-törés:** az ismétlődő részek veéltlenül ugyanazon kulcs alá esnek akkor véletlenül épp a kulcs is lehet megegyező. *(ilyenek pl a névelők)* Ha tudjuk hanyadik pontonként ismétlődik akkor megtudjuk a kulcshosszt, mivel a hossz méretének osztója a kulcs mérete.


### Nyilvános kulcsú rejtjelezés (pulic key)
> a felek kulccsere nélkül is tudnak titokban kommunikálni
A nyilvános kulcsú titkosítás az amikor a nyilvános kulcsból nem könnyen lehet kiszámolni a titkos kulcsot


## EA6
- rendszerinformáció console megnyitás: `rsm32`
- eszközkezelő: a csatlakoztatottt eszközök kezelését és a hozzá tartozó infrmációkat tekinthetjük meg.

gpg titkosítás: https://www.gpg4win.org/
- rsa 2048 (3242 bit-es is jó)

## EA7
*információbiztonság managemenet elvárásai:*
- rendelkezésre álllás
- bizalmasság
- sétretlenség
- hitelesség

**Gyakori hibák:**
- nincsennek általában jól kiosztva a jogosultságok.


**jelszó nehézség ellenörző oldalak:**
- https://password.kaspersky.com/
- http://www.passwordmeter.com/
- https://howsecureismypassword.net/
- https://www.elcomsoft.com/tools_for_home_use.html


### Server beállítások: 
új jelszó kell: Almafa123

## rendszertervezés
- ne legyen super user
- használjunk jól beállított tűzfalakat
- titkosított módon kezeljük a ebállításokat/használt titkosítási metóduokat.

**Támadásokról:**
- motiváció:
  - információszerzés
  - károkozás/rendszerek bénítása
  - szolgáltatásokhoz hozzáférés
- passzív támadás: lehallgatunk
- aktív támadás: akár megszemélyesítjük, kiadjuk magunkat a rendszer egyik résztvevőjének, stb
- csomag alapú támadás (IP spoofing): IP címet hamisítunk, és így lépünk be.
  - RST üzeneteket küldözgethetünk, ellehetetlenítjük a belső kommunikációt
  - ICMP támadás: echo requestet kérünk minden résztvevőtől, és így mindneki válaszolgat, és másnak már nincs hely, megoldás: routerben icmp echo requestet szűrünk
- DNS támadás: TTL időt kihasználva létrehozunk egy áll oldalt ami hasonlít a lekértre, ahol a felhasználó bedja az adatiati, mi lementjük, és továbbküldjük a hivatalos oldalra.
- tiltsunk minden portot mai nincs használatban
- naplózást ne a naplózott gépen tároljuk
- inkább szüntessük meg a bizotnsági hibát és tegyünk be egy újat, mintsem hagyjuk a régit
- címtár: hálózati objektumokat, kötetek, nyomtatók, stb adatainak tárolása

### IBM Tivoli Directory Server
- adatmentés
- csv -> xml konvertálást tudunk létrehzni,
- https://github.com/sivabalanb/Data-Analysis-with-Pandas-and-Python/blob/master/employees.csv
- az a lényege, hogy a cég fejlődésével egyszerre meglévő, működő rendszerekből szedi ki az információkat, és így nem kell a meglévő rendszereknek leállnia, rendszerfrissítés közben.
























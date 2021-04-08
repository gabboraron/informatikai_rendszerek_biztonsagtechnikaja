# Informatikai rendszerek biztonságtechnikája

**Ajánlott irodalom:**
- [Buttyán Levente, Györfi László, Győri Sándor, Vajda István: Kódolástechnika, 2006 - crysys web változat – 6.](https://docplayer.hu/2525122-Kodolastechnika-2006-crysys-web-valtozat-6-kodolastechnika-buttyan-levente-gyorfi-laszlo-gyori-sandor-vajda-istvan-2006-december-18.html)
- [Buttyán Levente, Vajda István : Kriptográfia és alkalmazásai TYPOTEX ISBN 963-9548-13-8 *fizetős!*](https://www.interkonyv.hu/konyvek/buttyan-levente-vajda-istvan-kriptografia-es-alkalmazasai/)
- Virasztó Tamás : Titkosítás és adatelrejtés. Netacademia Oktatóközpont. ISBN 963-214253-5
- Nagy Sándor: Elektronikus leveleink védelme, Computerbooks, 2005.

**Amit találtam irodalom:**
- [Hálózatok Biztonsága - Frész Ferenc, Kálovics Tamás, Puha Gábor](https://cmsadmin-pub.uni-nke.hu/document/vtkk-uni-nke-hu/halozatok-biztonsaga.original.pdf)

**Követelmények:**
- május 06 ZH
- szóbeli ZH

## EA1
- Tempest támadás
- passzív támadás: lehallgatás
- aktív támadás: a támadó beavatkozik a kommunikációba
- IP spoofing: az ip cím meghamisítása
- smurf: broadcast üzenetet küldünk az áldozatt felé
- switchek támadása: a switch táblájába betesszük a saját címünk is így megkapunk minden üzenetet mi is.
- social engineering: a támadás az emberi megtévesztésen alapul
- reverse engeneering: amikor elhitetik az áldozattal, hogy ő a kezdeményező, pl *a bejelentett hiba miatt telefonálok*
- xss: a weboldalba beépített mezőkbe írunk `js` kódot vagy szerver oldali kódot és azt futtatjuk

## EA2

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
























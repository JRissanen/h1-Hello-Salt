# h1-Hello-Salt

__x) Lue ja tiivistä__

## Command Line Basics Revisited

  Hyödyllisiä komentorivin komentoja:
  - pwd -> Näyttää aktiivisen hakemiston.
  - ls -> Listaa hakemistossa olevat tiedostot.
  - cd /(hakemisto) -> Vaihtaa aktiivista hakemistoa.
  - mkdir (hakemiston nimi) -> Luo uuden hakemiston, esimerkiksi kansion.
  - cp -> Kopioi tiedoston.
  - mv -> siirtää tiedoston, tai uudelleen nimeää sen.
  - rm (tiedoston nimi) -> poistaa tiedoston.

  Ssh yhteyden muodostaminen onnnistuu kirjoittamalla käyttäjätunnuksen, sen jälkeen "@" merkin ja sitten serverinnimen. "ssh käyttäjätunnus@serverinnimi.com"
  Ssh yhteyden saa lopetettua "exit" komennolla.

  Avun ja lisäinfon etsiminen:
  - (komento) --help -> Avaa järjestelmän sisäisen tiivistelmän komennon ominaisuuksista.
  - man (komento) -> Avaa järjestelmän sisäiset manuaalisivut, eli ohjekirjan komennolle.

  Pääkäyttäjän oikeudet saa käyttöön "sudo" aloituksella ja käyttäjän salasanalla.
  Hyödyllisiä sudo-komentoja:
  - sudo apt-get update -> Tarkistaa onko käyttöjärjestelmälle saatavilla uutta päivitystä.
  - sudo apt-get upgrade -> Päivittää käyttöjärjestelmän.
  - sudo apt install (ohjelma) -> Lataa asentaa ohjelman.

## Salt States – I Want My Computers Like This

  - Saltin avulla on mahdollista hallita useampaa konetta samanaikaisesti.
  - Saltin toiminta perustuu "Master" ja "Slave" hierarkia rakenteeseen, jossa Master-kone antaa toimintaohjeita kaikille Slave-koneille.
  - Master koneen määrittämät ohjeet Slave-koneille tallennetaan tiedostopolkuun "/srv/salt", joka käyttäjän on itse luotava.
  - Slave-koneiden ohjeet ovat YAML-tiedostoja, ja niiden pääte on "".sls".
  - Komennolla: "sudo salt '*' state.apply", voi ajaa tietyn tilan jokaiseen Slave-koneeseen.
  - "top.sls"-nimisen tiedoston avulla voi määrittää vaiheita, joita Slave-koneet ajavat automaattisesti tietyin aikavälein.

## Raportin kirjoittaminen

  Hyvän raportoinnin ominaisuuksia ja vinkkejä:

  - Kannattaa kirjoittaa raporttia koko ajan tekiessä.
  - Kannattaa tehdä muistiinpanoja.
  - Ympäristö on hyvä huomioida, koska siitä käy ilmi raportin tulokset ja se mahdollistaa raportin toistamisen.
  - Raportoi onnistuneet ja epäonnistuneet vaiheet täsmällisesti sekä mahdolliset vikatilanteet, niin raportista saa paremman kokonaiskuvan.
  - Kirjoita raportti menneessä aikamuodossa.
  - Kiinnitä huomioita kielioppiin, se lisää uskottavuutta.
  - Muista helppolukuisuus eli, väliotsikointi, kappaleiden pituudet, pisteiden ja pilkkujen käyttö yms.
  - Muista antaa lähdeviittaukset kaikkiin käytettyihin lähteisiin.

# Saltin kokeilu tehtävät:

  __a) Tiedoston luominen yksittäisellä komentorivillä (state.single)__

    - Käytetään komentoa: "sudo salt-call --local state.single file.managed /tmp/juliuswashere contents="Sisältö on oikea".
    - Tiedoston voi tarkistaa siirtymällä tmp-hakemistoon ja avaamalla juliuswashere tiedoston jollain tekstieditorilla tai "cat" komennolla.

  __b) Salt idempotentti infrakoodina__

    - Tehdään uusi hakemisto komennolla: "sudo mkdir /srv/salt/helloworld"
    - Tehdään hakemistoon uusi init.sls tiedosto jollakin tekstieditorilla: "sudoedit init.sls"
    - init.sls-tiedoston sisältö tulisi näyttää seuraavalta:
      /tmp/helloworld:
        file.managed:
          - contents: "Hello World!"
    - Ajetaan tiedosto komennolla: "sudo salt-call --local state.apply helloworld
    - Tiedoston voi tarkistaa kuten a) kohdassa.

  __d) Tiedon kerääminen koneesta saltilla__

    - Käytetään komentoa: "sudo salt-call --local grains.items.
    - Aukeaa tiedosto täynnä infoa koneesta, ja sen avulla voi tarkistaa esimerkiksi:
      - Cpu:n mallin
      - Ip-osoitteen
      - Käyttäjän nimen
      - Serverin nimen
      - Kernelin
      - Käyttöjärjestelmän version

  __e) Jokin muu tila kuin file.managed__

    - Ajattelin määrittää tilan, joka asentaa nano-tekstieditorin.
    - Sama idea kuin b) kohdassa, mutta uuden hakemiston nimeksi nano.
    - init.sls-tiedoston sisältö tulisi näyttää seuraavalta:
      nano:
        pkg.installed
    - Tiedoston ajaessa terminaaliin tulostuu joko "ohjelma on jo asennettu, ei muutoksia", tai "asennus onnistui".

__Lähteet__
  
  Palvelintenhallinta, terokarvinen.com: https://terokarvinen.com/2022/palvelinten-hallinta-2022p2/?from=MoodleNews#h1-hello-salt
  
  Command Line Basics Revisited, terokarvinen.com: https://terokarvinen.com/2020/command-line-basics-revisited/
  
  Salt States – I Want My Computers Like This, terokarvinen.com: https://terokarvinen.com/2018/salt-states-i-want-my-computers-like-this/
  
  Raportin kirjoittaminen, terokarvinen.com: https://terokarvinen.com/2006/raportin-kirjoittaminen-4/?fromSearch=raportin%20kirjoittaminen

## h3 Demoni

## x)  Apache installed with Ansible
- Muutokset konfiguraatiotiedostoihin tulevat voimaan vasta, kun palvelu käynnistetään uudelleen.
- `roles/apache2/` sisältää kaiken rooliin liittyvän.
- `tasks/main.yml` luo symbolisen linkin sites-enabled-hakemistoon.
- Huomio: `notify` varmistaa, että restart tapahtuu vain tarvittaessa.
  
## x)  Ansible Community Documentation
- Handler on tehtävä, joka ajetaan vain jos jokin muuttuu.
- Jos loopissa yksikin item aiheuttaa muutoksen → kaikki handlerit ajetaan.
- Roolien handlerit menevät globaalisti samaan listaan.
- Huomio: Handler säästää turhilta restarteilta ja tekee playbookista siistin.
  
## x) ansible-doc service
- service‑moduuli hallitsee palveluiden tilaa eri Linux‑järjestelmissä.
- Sillä voi käynnistää, pysäyttää, restartata ja ottaa palvelun käyttöön tai pois käytöstä.
- Moduuli käyttää järjestelmän omaa init‑järjestelmää.

*enabled*
- Määrittää, käynnistyykö palvelu automaattisesti bootissa.
- Arvot:
```
yes → palvelu käynnistyy automaattisesti
no → ei käynnisty automaattisesti
```
*name*
- Palvelun nimi, jota hallitaan.
- Esim. name: apache2 

*state*
- Määrittää palvelun halutun tilan:
```
started → palvelu käynnissä
stopped → palvelu pysäytetty
restarted → palvelu käynnistetään uudelleen
reloaded → konfiguraatio ladataan uudelleen ilman täyttä restarttia
```

*EXAMPLES*
```
yaml
- name: Ensure apache is running
    name: apache2
    state: started

- name: Restart apache
    name: apache2
    state: restarted

- name: Enable apache on boot
    name: apache2
    enabled: yes
```

## a) Apassi. Asenna Apache 2 käsin. Weppisivun tulee näkyä palvelimen etusivulla. Sivun tulee olla tavallisen käyttäjän muokattavissa, ilman root- tai sudo-oikeuksia.

<img width="986" height="803" alt="Kuva Apache2 Debian Default pagesta." src="https://github.com/user-attachments/assets/e3783696-cf09-4bd9-b0fd-e3a25c8bad65" />

- Asensin Apache 2 ‑palvelimen käsin, testasin sen toiminnan ja loin oman etusivun. Muutin hakemiston omistajuuden tavalliselle käyttäjälle, jotta sivua voi muokata ilman sudo‑oikeuksia. Tässä lopputulos että toimii.

## b) Moottorix. Asenna Nginx käsin. Weppisivun tulee näkyä palvelimen etusivulla. Sivun tulee olla tavallisen käyttäjän muokattavissa, ilman root- tai sudo-oikeuksia. (Muista sammuttaa Apache ensin.)

- Sammutin ensin Apachen, jotta portti 80 vapautui Nginxille. sudo systemctl stop apache2. Asensin Nginxin käsin:
```
sudo apt-get install nginx
```
<img width="944" height="261" alt="Tarkistus, että lähti käyntiin." src="https://github.com/user-attachments/assets/35cab3af-ebea-4587-a015-7d36e4107cc0" />

- Tarkistus, että Nginx lähti käyntiin. Vaihdoit Nginxin oletusjuurihakemiston tavallisen käyttäjän omistukseen, jotta sivua voi muokata ilman sudoa. Lopuksi loin oman index.html‑tiedoston tavallisena käyttäjänä ja se näkyy palvelimen etusivulla osoitteessa http://localhost.

## c) Automoottorix. Automatisoi Nginx asennus Ansiblella. Ylläpitäjän osuus Ansiblella riittää, itse HTML-weppisivut voi tehdä käsin.

- Asensin Nginxin automaattisesti Ansible‑roolilla, joka hoitaa paketin asennuksen, käynnistää palvelun ja kopioi oman `index.html`‑sivuni palvelimelle. Rooli myös vaihtaa hakemiston omistajaksi tavallisen käyttäjän, jotta sivua voi muokata ilman sudoa. Playbookin ajon jälkeen Nginx on valmiina ja näyttää oman etusivun automaattisesti.


## Lähteet
- Karvinen 2026: Apache installed with Ansible | https://terokarvinen.com/apache-ansible/
- Karvinen 2008: Install Apache Web Server on Ubuntu | https://terokarvinen.com/2008/05/02/install-apache-web-server-on-ubuntu-4/index.html
- Ansible Community Documentation: Handlers: running operations on change | https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html
- Karvinen 2026: Palvelinten Hallinta | https://terokarvinen.com/palvelinten-hallinta/#h3-demoni

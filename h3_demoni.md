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

<img width="773" height="426" alt="Hei Apache kuva." src="https://github.com/user-attachments/assets/776bd229-9e18-4cc8-8b8a-a77c07e8b5fe" />

- Asensin Apache2‑palvelimen ja laitoin sen näyttämään oman index.html‑sivuni palvelimen etusivulla. Vaihdoin /var/www/html‑hakemiston omistajaksi tavallisen käyttäjän, jotta sivua voi muokata ilman sudo‑oikeuksia.

## b) Moottorix. Asenna Nginx käsin. Weppisivun tulee näkyä palvelimen etusivulla. Sivun tulee olla tavallisen käyttäjän muokattavissa, ilman root- tai sudo-oikeuksia. (Muista sammuttaa Apache ensin.)

- Sammutin Apachen ja asensin Nginxin, jotta portti 80 vapautui uudelle palvelimelle. Tein oman etusivun ja annoin tavalliselle käyttäjälle oikeudet muokata /var/www/html‑hakemistoa ilman sudoa.
  
<img width="850" height="412" alt="Hei Nginx kuva." src="https://github.com/user-attachments/assets/12ca7bc9-e5f0-4170-bdad-b0fd1c1c27f8" />

## c) Automoottorix. Automatisoi Nginx asennus Ansiblella. Ylläpitäjän osuus Ansiblella riittää, itse HTML-weppisivut voi tehdä käsin.

<img width="567" height="538" alt="image" src="https://github.com/user-attachments/assets/02095914-871e-4952-a423-18da0656ebc0" />

- Automatisoin Nginxin asennuksen Ansible‑roolilla, joka asentaa palvelun, kopioi oman HTML‑sivun ja varmistaa, että käyttäjä voi muokata sitä ilman sudoa. Playbook käynnistää Nginxin automaattisesti ja tekee koko asennuksesta toistettavan.

## Lähteet
- Karvinen 2026: Apache installed with Ansible | https://terokarvinen.com/apache-ansible/
- Karvinen 2008: Install Apache Web Server on Ubuntu | https://terokarvinen.com/2008/05/02/install-apache-web-server-on-ubuntu-4/index.html
- Ansible Community Documentation: Handlers: running operations on change | https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html
- Karvinen 2026: Palvelinten Hallinta | https://terokarvinen.com/palvelinten-hallinta/#h3-demoni

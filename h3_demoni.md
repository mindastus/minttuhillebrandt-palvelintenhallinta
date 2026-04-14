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

-

## b) Moottorix. Asenna Nginx käsin. Weppisivun tulee näkyä palvelimen etusivulla. Sivun tulee olla tavallisen käyttäjän muokattavissa, ilman root- tai sudo-oikeuksia. (Muista sammuttaa Apache ensin.)

-

## c) Automoottorix. Automatisoi Nginx asennus Ansiblella. Ylläpitäjän osuus Ansiblella riittää, itse HTML-weppisivut voi tehdä käsin.

-


## Lähteet
- Karvinen 2026: Apache installed with Ansible | https://terokarvinen.com/apache-ansible/
- Ansible Community Documentation: Handlers: running operations on change | https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html
- Karvinen 2026: Palvelinten Hallinta | https://terokarvinen.com/palvelinten-hallinta/#h3-demoni

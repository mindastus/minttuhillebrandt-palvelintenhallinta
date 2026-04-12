## h3 Demoni

## x) Lue ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva. Ei siis vaadita pitkää eikä essee-muotoista tiivistelmää. Lisää kuhunkin jokin oma kysymys tai huomio.)

Karvinen 2026: Apache installed with Ansible - quick notes
Ansible Community Documentation: Handlers: running operations on change
Handlers: running operations on change (johdantokappale pääotsikon alta)
Notifying handlers
'ansible-doc service':
johdantokappale (MODULE alta)
enabled
name
state

## a) Apassi. Asenna Apache 2 käsin. Weppisivun tulee näkyä palvelimen etusivulla. Sivun tulee olla tavallisen käyttäjän muokattavissa, ilman root- tai sudo-oikeuksia.

-

## b) Moottorix. Asenna Nginx käsin. Weppisivun tulee näkyä palvelimen etusivulla. Sivun tulee olla tavallisen käyttäjän muokattavissa, ilman root- tai sudo-oikeuksia. (Muista sammuttaa Apache ensin.)

-

## c) Automoottorix. Automatisoi Nginx asennus Ansiblella. Ylläpitäjän osuus Ansiblella riittää, itse HTML-weppisivut voi tehdä käsin.

-

Vinkit

Ensin käsin, sitten automaattisesti
Pienen testattava kokonaisuus kerrallaan
Lue lokeja. Weppipalvelimen virheilmoitukset ovat lokeissa, käyttäjälle näkyvä weppisivu ei kerro juuri mitään.
Kaksi demonia ei voi kuunnella samaa porttia. Sulje siis nginx ennen apachen asennusta ja päinvastoin.
'ansible-doc apt': name, state, update_cache. EXAMPLES.
'ansible-doc copy': dest, src; owner, group, mode. EXAMPLES.
'ansible-doc file': src, dest, state. owner, group. EXAMPLES.
nginx asennus on samantapainen kuin Apachen
sites-available/default - tiedoston lopussa on esimerkki yksinkertaisesta konfiguraatiosta
'sudo nginx -t' on samantapainen kuin 'sudo apache2ctl configtest'
Kotisivut käyttäjänä
Weppipalvelin pyörinee käyttäjänä www-data, ryhmä www-data. Jos tiedoston omistaa tero:tero, niin www-data on others eli viimeiset kolme kirjainta.
Jotta se näkee sivut, kansioihin pitää olla x-oikeus ja tiedostoihin r.
/home/tero/publicsite/index.html
chmod ugo+x /home/tero/
chmod ugo+x /home/tero/publicsite/
chmod ugo+r /home/tero/publicsite/index.html
Tarkista oikeudet 'ls -t' ja 'stat'

## Lähteet
Karvinen 2026: Apache installed with Ansible | https://terokarvinen.com/apache-ansible/
Ansible Community Documentation: Handlers: running operations on change | https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html
Handlers: running operations on change (johdantokappale pääotsikon alta)

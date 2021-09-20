# .cpanel.yml fajl

Deploy proces se obavlja uz pomoć fajla pod nazivom `.cpanel.yml`. Ovaj fajl definiše niz komandi koje `bash` interpreter operativnog sistema treba da izvrši. Naredbe unutar ovog fajla su navedene sa u yaml formatu, sa minusom ispred svake komande.

Ovo je primer jednog takvog fajla:

```
---
deployment:
  tasks:
    - DEPLOYPATH="/home/$USER/public_html"
    - /bin/cp index.html ${DEPLOYPATH}/index.html
    - /bin/cp -R ./css ${DEPLOYPATH}/css
```

Deploy fajl treba da bude dodat u osnovni direktorijum projekta, odnosno git repozitorijuma.

Kada je novi git repozitorijum napravljen, i deploy fajl se nalazi u osnovnom direktorijumu projekta, u cpanelu će biti prikazana opcija `Deploy HEAD Commit`

`slika`

Klikom na ovu opciju pokreće se `git deploy` i izvršavaju se naredbe navedene u fajlu, onim redosledom kojim su navedene.

Nakon što je deploy proces uspešno završen, biće prikazano zeleno obaveštenje:

`slika`

Kako biste jednostavnije isprobali `pull deploy` možete klonirati naš primer sa github-a:
https://github.com/dreamwebhost/git-deploy

## Push deploy

Za uspostavljanje `push deploy` radnog procesa, potrebno je prvo kreirati prazan repozitorijum putem cPanel-a: Prazan repozitorijum možete kreirati prema sledećem uputstvu:
https://www.dreamclients.com/help/kb/article/webmaster/kreiranje-git-servera-u-cpanel-nalogu

Nakon što je repozitorijum kreiran, biće prikazan ekran sa listom naredbi koje treba pokrenuti sa lokalnog računara kako bismo repozitorijum sa cPanel-a klonirali na lokalni računar.

Nakon što je repozitorijum kloniran na lokalni računar, možemo kreirati README.md fajl sledećom naredbom:

```
echo -e "# Readme" > README.md
touch '.cpanel.yml'
```

nakon toga treba da dodamo ove izmene u git:

```
git add -A
git commit -m "Dodat README fajl i cPanel deploy."
git push
``` 

Nakon što su izmene poslate cPanel-u sa `git push`, deploy proces će biti pokrenut automatski nakon toga.
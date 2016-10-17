# Labo 2: Linux leren kennen

## Hulp zoeken

1. Hoe vraag je op de command-line documentatie op voor het *commando* `passwd`?

    ```
   $ info passwd of man passwd
PASSWD(1) User utilities PASSWD(1)
NAME
 passwd - update user's authentication tokens
SYNOPSIS
 passwd [-k] [-l] [-u [-f]] [-d] [-e] [-n mindays] [-x maxdays] [-w
 warndays] [-i inactivedays] [-S] [--stdin] [username]
DESCRIPTION
 The passwd utility is used to update user's authentication token(s).
 This task is achieved through calls to the Linux-PAM and Libuser API.
 Essentially, it initializes itself as a "passwd" service with Linux-PAM
 and utilizes configured password modules to authenticate and then
 update a user's password.
 A simple entry in the global Linux-PAM configuration file for this ser‐
 vice would be:
 #
 # passwd service entry that does strength checking of
    ```

2. Hoe vraag je documentatie op voor het *configuratiebestand* `/etc/passwd`?

    ```
    $ info /etc/passwd
    
    ```

3. Hoe vraag je een lijst op van alle documentatie die de string `passwd` bevat?

    ```
    $ man -k passwd
    ```

## Werken op de command-line

1. Wat is de huidige datum en uur?

    ```
    $ date
    
    ```

2. Wat is de huidige directory?

    ```
    $ pwd
    
    ```

3. Toon de inhoud van de huidige directory. De uitvoer zou er ongeveer zo moeten uit zien:

    ```
    $ ls
    Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos
    ```

4. Toon de inhoud van de huidige directory, maar toon voor elk bestand meer informatie en ook "verborgen" bestanden.

    ```
    $ ls -a -l
total 96
drwx------. 14 student student 4096 Sep 24 09:14 .
drwxr-xr-x. 3 root root 4096 Sep 20 13:46 ..
-rw-------. 1 student student 146 Sep 20 14:06 .bash_history
-rw-r--r--. 1 student student 18 Mar 11 2013 .bash_logout
-rw-r--r--. 1 student student 193 Mar 11 2013 .bash_profile
-rw-r--r--. 1 student student 124 Mar 11 2013 .bashrc
drwx------. 8 student student 4096 Sep 20 13:54 .cache
drwxr-xr-x. 16 student student 4096 Sep 20 13:55 .config
drwxr-xr-x. 2 student student 4096 Sep 20 13:53 Desktop
drwxr-xr-x. 2 student student 4096 Sep 20 13:53 Documents
    drwxr-xr-x.  2 student student 4096 Sep 20 13:53 Desktop
    drwxr-xr-x.  2 student student 4096 Sep 20 13:53 Documents
    drwxr-xr-x.  2 student student 4096 Sep 20 13:53 Downloads
    [...]
    ```

5. Toon de inhoud van de hoofddirectory van het Linux-systeem, ook vaak de root-directory genoemd. Geef een uitgebreide listing zoals in de vorige vraag, maar *zonder* verborgen bestanden.

    ```
   $ su -
$ ls -l
    ```

6. Wat betekenen volgende elementen van de uitvoer hierboven?
    - 1e kolom (bv. `drwxr-xr-x.`): ...
    - 2e kolom (getal): ...
    - 3e kolom (bv. `root`, `student`): ...
    - 4e kolom (bv. `root`): ...
    - 5e kolom (getal): ...
    - 6e - 8e kolom (datum): ...
    - de aanduiding `->` (bv. `bin -> usr/bin`): ...
7. Hoe kan je commando's die je voordien uitgevoerd hebt terug ophalen (de "commandogeschiedenis")?

    ```
    $ history
    
    ```

## De plaats van bestanden op een Linux-systeem

Vul de tabel hieronder aan. In de linkerkolom vind je de namen van een directory, in de rechter het soort bestanden dat er in thuis hoort.

| Directory                         | Inhoud                                                  |
| :---                              | :---                                                    |
| `/bin`, `/usr/bin`                | **Essentiele commando binaries**                                            |
| **`/boot`**                    | Uitvoerbare bestanden voor systeembeheertaken           |
| `/var`                            | **Variabele data**                                            |
| **`/tmp`**                    | Tijdelijke bestanden                                    |
| `/opt`, `/usr/local`              | **Add-on packages**                                            |
| **`/root`**                    | Home-directory van de `root` gebruiker                  |
| **`/home/student`**                    | Home-directory van de gebruiker `student`               |
| **`usr/share/man`**                    | De inhoud van de man-pages                              |
| **`usr/share`**                    | Andere documentatie                                     |
| `/lib`, `/usr/lib`, `lib64`, enz. | **Essentiele gedeelde libaries en kernel modules**                                            |
| **`/mnt`**                    | De inhoud van de installatie-cd voor Guest Additions(*) |
| `/dev`                            | **is the location of special or device files.**                                            |
| `/proc`                           | **Informatie over lopende processen en de kernel**                                            |
| **`/etc`**                    | Systeemconfiguratiebestanden                            |

(*) Je kan het insteken van de cd simuleren in het VirtualBox-venster van je VM in het menu "Devices" > "Insert Guest Additions CD image..." (of het Nederlandstalige equivalent).


## Werken met bestanden en directories

Om het verschil tussen een bestand en directory te verduidelijken, wordt in wat volgt de naam van een directory telkens afgesloten met “/”.

### Directories

Open eerst een terminalvenster, start de oefening vanuit je eigen home-directory. Ga enkel naar een andere directory als dat expliciet gevraagd wordt. Geef telkens de gevraagde commando's niet alleen om de taak uit te voeren, maar ook om te testen of dit correct gebeurd is.

In deze oefening leer je onderscheid maken tussen *relatieve* en *absolute paden*. Een *absoluut* pad begint altijd met een `/`, wat overeenkomt met de root-directory. Een *relatief* pad geldt vanaf de huidige directory.

1. Blijf in je home-directory en maak van hieruit een directory `tijdelijk/` aan onder `/tmp/`

    ```
    $ mkdir /tmp/tijdelijk
    
    ```

2. Verwijder deze directory meteen

    ```
    $ rmdir /tmp/tijdelijk
    
    ```

3. Maak onder je home-directory een submap aan met de naam `linux/`

    ```
    $ mkdir linux/
    
    ```

4. Ga naar deze directory

    ```
    $ cd linux/
    
    ```

5. Maak met één commando de subdirectory `a/b/` aan onder `linux/`. Als je nadien het commando `tree` geeft, moet je de gegeven uitvoer zien.

    ```
    $ mkdir -p a/b/
    
    $ tree
    .
    └── a
    └── b
    2 directories, 0 files
    ```

6. Verwijder directory `b/` en daarna `a/` (in twee commando's)

    ```
    $ rmdir a/b/
    & rmdir a/
    
    ```

7. Maak met één commando deze directorystructuur aan.

    ```
[student@localhost linux]$ mkdir c e d
[student@localhost linux]$ tree
.
├── c
├── d
└── e

    3 directories, 0 files
    ```

8. Verwijder in één commando de directory `c/` en alle onderliggende

    ```
    $ rm -rf *
    
    ```

9. Maak met één commando deze directorystructuur aan. Het is de bedoeling de opdrachtregel zo kort mogelijk te maken, dus niet alle directories apart opgeven!

    ```
    $ $ mkdir -p f g/i h/i
    
    $ tree
    .
    └── f
    ├── g
    │   └── i
    └── h
        └── i

    5 directories, 0 files
    ```

Behoud deze directorystructuur voor de volgende oefeningen over bestanden.

### Bestanden

1. Maak een leeg bestand aan met de naam `file1`

    ```
    $ touch file1
    
    ```

2. Maak een *verborgen* bestand aan met de naam `hidden`. Verborgen betekent dat je het niet kan zien met een "gewone" `ls`, maar wel met de gepaste optie.

    ```
    $ touch .hidden
    
    ```

3. Tik volgend commando in, leg uit wat er hier precies gebeurt, wat het effect is.

    ```
    $ echo hello world > file2"
    ```

    **hello world word naar het bestand file2 geschreven** 

4. Toon de inhoud van `file2`

    ```
    $ cat file2
    hello world
    ```

5. Kopieer `file1` naar een nieuw bestand `file3` in de huidige directory

    ```
    $ cp file1 file2
    
    ```

6. Kopieer `file1` naar de directory `f/` (die zou je nog moeten hebben van vorige oefening)

    ```
    $ cp file1 f/file1
    UITVOER
    ```

7. Kopieer `file1` en file2 in één keer naar `f/g/`. Je zou de gegeven situatie moeten krijgen.

    ```
    $ cp -t f/g/ file1 file2
    
    $ tree
    .
    ├── f
    │   ├── file1
    │   ├── g
    │   │   ├── file1
    │   │   ├── file2
    │   │   └── i
    │   └── h
    │       └── i
    ├── file1
    ├── file2
    └── file3
    ```

8. *Hernoem* `file3` naar `file4`

    ```
    $ mv file3 file4
    UITVOER
    ```

9. Verplaats `file2` naar directory `f/`

    ```
    $ cp file2 f/file2
    UITVOER
    ```

10. Verplaats `file1` en `file4` in één keer naar `f/h/`. Je zou de gegeven situatie moeten krijgen.

    ```
   $ cp -t f/h/ file1 file4
    $ tree
    .
    └── f
    ├── file1
    ├── file2
    ├── g
    │   ├── file1
    │   ├── file2
    │   └── i
    └── h
        ├── file1
        ├── file4
        └── i

    5 directories, 6 files
    ```

11. Kopieer `f/h/`, inclusief de inhoud, naar een nieuwe directory `f/j/`

    ```
    $ cp -r f/h f/j
    
    ```

### Pathname expansion (of *file globbing*)

Creëer in de directory `linux/` een aantal lege bestanden met de naam `filea` t/m `filed`, `file1` t/m `file9` en `file10` t/m `file19`. Hier is een trucje om dat snel te doen:

```
[student@localhost ~/linux] $ touch filea fileb filec filed
[student@localhost ~/linux] $ for i in {1..19}; do touch "file${i}"; done 
[student@localhost ~/linux] $ ls 
f       file11  file14  file17  file2  file5  file8  fileb 
file1   file12  file15  file18  file3  file6  file9  filec 
file10  file13  file16  file19  file4  file7  filea  filed 
```

Toon met `ls` telkens de gevraagde bestanden, niet meer en niet minder.

1. Alle bestanden die beginnen met `file`

    ```
    $ ls file*
    UITVOER
    ```

2. Alle bestanden die beginnen met `file`, gevolgd door één letterteken (cijfer of letter)

    ```
    $ ls file?
    UITVOER
    ```

3. Alle bestanden die beginnen met `file`, gevolgd door één letter, maar geen cijfer

    ```
    $ ls file[a-z]
    UITVOER
    ```

4. Alle bestanden die beginnen met `file`, gevolgd door één cijfer, maar geen letter

    ```
    $ ls file[1-9]
    UITVOER
    ```

5. De bestanden `file12` t/m `file16`

    ```
    $ ls file1[2-6]
    UITVOER
    ```

6. Bestandern die beginnen met `file`, *niet* gevolgd door een `1`

    ```
    $ ls file[!1]
    UITVOER
    ```

### Links

Maak in de directory `linux/` twee tekstbestanden aan, met naam `tekst1a` en `tekst2a`. Beide hebben als inhoud “Dit is bestand tekst1” en “Dit is bestand tekst2”, respectievelijk.

1. Voor het volgende commando uit en geef de uitvoer:

    ```
    [student@localhost linux]$ ls -l tekst*
-rw-rw-r--. 1 student student 22 2016-10-17 14:00 tekst1
-rw-rw-r--. 1 student student 22 2016-10-17 14:01 tekst2
    ```

2. Maak een *harde link* van `tekst1a` naar `tekst1b`
ln /home/student/linux/tekst1a /home/student/linux/tekst1b
3. Maak een *symbolische link* van `tekst2a` naar `tekst2b`
ln -s /home/student/linux/tekst2a /home/student/linux/tekst2b
4. Voor het volgende commando uit en geef de uitvoer:

    ```
   [student@localhost linux]$  ls -l tekst*
-rw-rw-r--. 2 student student 22 2016-10-17 14:00 tekst1a
-rw-rw-r--. 2 student student 22 2016-10-17 14:00 tekst1b
lrwxrwxrwx. 1 student student 27 2016-10-17 14:11 tekst2b -> /home/student/linux/tekst2a
    ```

5. Hoe zie je aan de uitvoer van `ls` dat `tekst1b` een harde link is en `tekst2b` een symbolische? Tip: Vergelijk met de uitvoer uit vraag 1!

    **Antwoord**: 

6. Verwijder de oorspronkelijke bestanden, `tekst1a` en `tekst2a`. Maak het commando zo kort mogelijk!

    ```
    $ rm tekst1a tekst2a
    UITVOER
    ```

7. Toon opnieuw de uitvoer van `ls -l tekst*`, en bekijk de inhoud van `tekst1b` en `tekst2b`. Wat valt je op?

    ```
    $ ls -l tekst*
    -rw-rw-r--. 1 student student 0 2016-10-13 11:50 tekst1b
lrwxrwxrwx. 1 student student 27 2016-10-13 11:54 tekst2b.txt -> /home/student/linux/tekst2a.txt
    ```

    **Antwoord**: de softlink gaat ook

### Bestanden archiveren

1. Creëer in je home-directory een archief `linux.tar.bz2` van de directory `linux/` en alle inhoud.

    ```
    $ $ tar -zcvf linux.tar.bz2 linux
linux/
linux/file2
linux/file4
linux/file6
linux/file7
linux/teskt2a
linux/file11
linux/tekst1b
linux/file16
linux/tekst2b
linux/filed
linux/fileb
linux/file12
linux/file10
linux/file13
linux/file8
linux/file9
linux/.hidden
linux/file17
linux/file1
linux/f/
linux/f/file1
linux/f/g/
linux/f/g/file2
linux/f/g/i/
linux/f/g/file1
linux/filec
linux/file5
linux/file18
linux/file14
linux/filea
linux/file19
linux/file15
linux/h/
linux/h/file4
linux/h/i/
linux/h/file1
linux/file3

    ```

2. Verwijder nu volledig de directory `linux/`

    ```
    $ rm -r linux
    UITVOER
    ```

3. Toon de inhoud van het archief zonder opnieuw uit te pakken

    ```
    $ cat linux.tar.bz2 
ހ3W�v�]$ ��3-��;4Ri\�:���ȪYo��XM�D	q�� }�x
                               V��{U�U��H�L|SYm�**���E�x/k`�iOߔe�i��z���s�~������lV�f��	����8S���T�e�vE���o�b��;�� ��l1H��K������	�m�9o�)S�����{׍���¿��-�MyV�۰^�m}�i����* E��Jq� �e0�a��1��S�I�߇��c�/����B��o��?[H������9��!���c���z�|}Q�ww~�_�յ*����[�I��ܐ�
�/A�ϕ�4��"d�� R���2�l���_ÿ������������O���)[
                                                     ����e��S����|P��0��<�K�=��6P����e���Š���/��?��N����C��������_F��`��_u
�F��+����}�{���$�|g&��οq��+C�߰U�      �_�@?�                                                                                  �1�
                                              �/����3 �?�R���-Ƥ�o\�����jK����"d�?l
                                                                                       @�ʢ�!��v��� �EH��N��Y��-��?�����g��?�D�/o�������?��"��9�d���ο1X��a��7�K����z��y�߀��}�c�/����9�7bv�����wn��o�t��S�����;ŧ���'�?ߺ��r�����p����p��ۃG��k�F�G��؎���q�
                                                                                  ��O�&��x
    ```

4. Pak het archief opnieuw uit in je home-directory.

    ```
    # Labo 2: Linux leren kennen

## Hulp zoeken

1. Hoe vraag je op de command-line documentatie op voor het *commando* `passwd`?

    ```
   $ info passwd of man passwd
PASSWD(1) User utilities PASSWD(1)
NAME
 passwd - update user's authentication tokens
SYNOPSIS
 passwd [-k] [-l] [-u [-f]] [-d] [-e] [-n mindays] [-x maxdays] [-w
 warndays] [-i inactivedays] [-S] [--stdin] [username]
DESCRIPTION
 The passwd utility is used to update user's authentication token(s).
 This task is achieved through calls to the Linux-PAM and Libuser API.
 Essentially, it initializes itself as a "passwd" service with Linux-PAM
 and utilizes configured password modules to authenticate and then
 update a user's password.
 A simple entry in the global Linux-PAM configuration file for this ser‐
 vice would be:
 #
 # passwd service entry that does strength checking of
    ```

2. Hoe vraag je documentatie op voor het *configuratiebestand* `/etc/passwd`?

    ```
    $ info /etc/passwd
    
    ```

3. Hoe vraag je een lijst op van alle documentatie die de string `passwd` bevat?

    ```
    $ man -k passwd
    ```

## Werken op de command-line

1. Wat is de huidige datum en uur?

    ```
    $ date
    
    ```

2. Wat is de huidige directory?

    ```
    $ pwd
    
    ```

3. Toon de inhoud van de huidige directory. De uitvoer zou er ongeveer zo moeten uit zien:

    ```
    $ ls
    Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos
    ```

4. Toon de inhoud van de huidige directory, maar toon voor elk bestand meer informatie en ook "verborgen" bestanden.

    ```
    $ ls -a -l
total 96
drwx------. 14 student student 4096 Sep 24 09:14 .
drwxr-xr-x. 3 root root 4096 Sep 20 13:46 ..
-rw-------. 1 student student 146 Sep 20 14:06 .bash_history
-rw-r--r--. 1 student student 18 Mar 11 2013 .bash_logout
-rw-r--r--. 1 student student 193 Mar 11 2013 .bash_profile
-rw-r--r--. 1 student student 124 Mar 11 2013 .bashrc
drwx------. 8 student student 4096 Sep 20 13:54 .cache
drwxr-xr-x. 16 student student 4096 Sep 20 13:55 .config
drwxr-xr-x. 2 student student 4096 Sep 20 13:53 Desktop
drwxr-xr-x. 2 student student 4096 Sep 20 13:53 Documents
    drwxr-xr-x.  2 student student 4096 Sep 20 13:53 Desktop
    drwxr-xr-x.  2 student student 4096 Sep 20 13:53 Documents
    drwxr-xr-x.  2 student student 4096 Sep 20 13:53 Downloads
    [...]
    ```

5. Toon de inhoud van de hoofddirectory van het Linux-systeem, ook vaak de root-directory genoemd. Geef een uitgebreide listing zoals in de vorige vraag, maar *zonder* verborgen bestanden.

    ```
   $ su -
$ ls -l
    ```

6. Wat betekenen volgende elementen van de uitvoer hierboven?
    - 1e kolom (bv. `drwxr-xr-x.`): ...
    - 2e kolom (getal): ...
    - 3e kolom (bv. `root`, `student`): ...
    - 4e kolom (bv. `root`): ...
    - 5e kolom (getal): ...
    - 6e - 8e kolom (datum): ...
    - de aanduiding `->` (bv. `bin -> usr/bin`): ...
7. Hoe kan je commando's die je voordien uitgevoerd hebt terug ophalen (de "commandogeschiedenis")?

    ```
    $ history
    
    ```

## De plaats van bestanden op een Linux-systeem

Vul de tabel hieronder aan. In de linkerkolom vind je de namen van een directory, in de rechter het soort bestanden dat er in thuis hoort.

| Directory                         | Inhoud                                                  |
| :---                              | :---                                                    |
| `/bin`, `/usr/bin`                | **Essentiele commando binaries**                                            |
| **`/boot`**                    | Uitvoerbare bestanden voor systeembeheertaken           |
| `/var`                            | **Variabele data**                                            |
| **`/tmp`**                    | Tijdelijke bestanden                                    |
| `/opt`, `/usr/local`              | **Add-on packages**                                            |
| **`/root`**                    | Home-directory van de `root` gebruiker                  |
| **`/home/student`**                    | Home-directory van de gebruiker `student`               |
| **`usr/share/man`**                    | De inhoud van de man-pages                              |
| **`usr/share`**                    | Andere documentatie                                     |
| `/lib`, `/usr/lib`, `lib64`, enz. | **Essentiele gedeelde libaries en kernel modules**                                            |
| **`/mnt`**                    | De inhoud van de installatie-cd voor Guest Additions(*) |
| `/dev`                            | **is the location of special or device files.**                                            |
| `/proc`                           | **Informatie over lopende processen en de kernel**                                            |
| **`/etc`**                    | Systeemconfiguratiebestanden                            |

(*) Je kan het insteken van de cd simuleren in het VirtualBox-venster van je VM in het menu "Devices" > "Insert Guest Additions CD image..." (of het Nederlandstalige equivalent).


## Werken met bestanden en directories

Om het verschil tussen een bestand en directory te verduidelijken, wordt in wat volgt de naam van een directory telkens afgesloten met “/”.

### Directories

Open eerst een terminalvenster, start de oefening vanuit je eigen home-directory. Ga enkel naar een andere directory als dat expliciet gevraagd wordt. Geef telkens de gevraagde commando's niet alleen om de taak uit te voeren, maar ook om te testen of dit correct gebeurd is.

In deze oefening leer je onderscheid maken tussen *relatieve* en *absolute paden*. Een *absoluut* pad begint altijd met een `/`, wat overeenkomt met de root-directory. Een *relatief* pad geldt vanaf de huidige directory.

1. Blijf in je home-directory en maak van hieruit een directory `tijdelijk/` aan onder `/tmp/`

    ```
    $ mkdir /tmp/tijdelijk
    
    ```

2. Verwijder deze directory meteen

    ```
    $ rmdir /tmp/tijdelijk
    
    ```

3. Maak onder je home-directory een submap aan met de naam `linux/`

    ```
    $ mkdir linux/
    
    ```

4. Ga naar deze directory

    ```
    $ cd linux/
    
    ```

5. Maak met één commando de subdirectory `a/b/` aan onder `linux/`. Als je nadien het commando `tree` geeft, moet je de gegeven uitvoer zien.

    ```
    $ mkdir -p a/b/
    
    $ tree
    .
    └── a
    └── b
    2 directories, 0 files
    ```

6. Verwijder directory `b/` en daarna `a/` (in twee commando's)

    ```
    $ rmdir a/b/
    & rmdir a/
    
    ```

7. Maak met één commando deze directorystructuur aan.

    ```
[student@localhost linux]$ mkdir c e d
[student@localhost linux]$ tree
.
├── c
├── d
└── e

    3 directories, 0 files
    ```

8. Verwijder in één commando de directory `c/` en alle onderliggende

    ```
    $ rm -rf *
    
    ```

9. Maak met één commando deze directorystructuur aan. Het is de bedoeling de opdrachtregel zo kort mogelijk te maken, dus niet alle directories apart opgeven!

    ```
    $ $ mkdir -p f g/i h/i
    
    $ tree
    .
    └── f
    ├── g
    │   └── i
    └── h
        └── i

    5 directories, 0 files
    ```

Behoud deze directorystructuur voor de volgende oefeningen over bestanden.

### Bestanden

1. Maak een leeg bestand aan met de naam `file1`

    ```
    $ touch file1
    
    ```

2. Maak een *verborgen* bestand aan met de naam `hidden`. Verborgen betekent dat je het niet kan zien met een "gewone" `ls`, maar wel met de gepaste optie.

    ```
    $ touch .hidden
    
    ```

3. Tik volgend commando in, leg uit wat er hier precies gebeurt, wat het effect is.

    ```
    $ echo hello world > file2"
    ```

    **hello world word naar het bestand file2 geschreven** 

4. Toon de inhoud van `file2`

    ```
    $ cat file2
    hello world
    ```

5. Kopieer `file1` naar een nieuw bestand `file3` in de huidige directory

    ```
    $ cp file1 file2
    
    ```

6. Kopieer `file1` naar de directory `f/` (die zou je nog moeten hebben van vorige oefening)

    ```
    $ cp file1 f/file1
    UITVOER
    ```

7. Kopieer `file1` en file2 in één keer naar `f/g/`. Je zou de gegeven situatie moeten krijgen.

    ```
    $ cp -t f/g/ file1 file2
    
    $ tree
    .
    ├── f
    │   ├── file1
    │   ├── g
    │   │   ├── file1
    │   │   ├── file2
    │   │   └── i
    │   └── h
    │       └── i
    ├── file1
    ├── file2
    └── file3
    ```

8. *Hernoem* `file3` naar `file4`

    ```
    $ mv file3 file4
    UITVOER
    ```

9. Verplaats `file2` naar directory `f/`

    ```
    $ cp file2 f/file2
    UITVOER
    ```

10. Verplaats `file1` en `file4` in één keer naar `f/h/`. Je zou de gegeven situatie moeten krijgen.

    ```
   $ cp -t f/h/ file1 file4
    $ tree
    .
    └── f
    ├── file1
    ├── file2
    ├── g
    │   ├── file1
    │   ├── file2
    │   └── i
    └── h
        ├── file1
        ├── file4
        └── i

    5 directories, 6 files
    ```

11. Kopieer `f/h/`, inclusief de inhoud, naar een nieuwe directory `f/j/`

    ```
    $ cp -r f/h f/j
    
    ```

### Pathname expansion (of *file globbing*)

Creëer in de directory `linux/` een aantal lege bestanden met de naam `filea` t/m `filed`, `file1` t/m `file9` en `file10` t/m `file19`. Hier is een trucje om dat snel te doen:

```
[student@localhost ~/linux] $ touch filea fileb filec filed
[student@localhost ~/linux] $ for i in {1..19}; do touch "file${i}"; done 
[student@localhost ~/linux] $ ls 
f       file11  file14  file17  file2  file5  file8  fileb 
file1   file12  file15  file18  file3  file6  file9  filec 
file10  file13  file16  file19  file4  file7  filea  filed 
```

Toon met `ls` telkens de gevraagde bestanden, niet meer en niet minder.

1. Alle bestanden die beginnen met `file`

    ```
    $ ls file*
    file1   file12  file15  file18  file3  file6  file9  filec
file10  file13  file16  file19  file4  file7  filea  filed
file11  file14  file17  file2   file5  file8  fileb

    ```

2. Alle bestanden die beginnen met `file`, gevolgd door één letterteken (cijfer of letter)

    ```
    $ ls file?
    file1  file3  file5  file7  file9  fileb  filed
file2  file4  file6  file8  filea  filec

    ```

3. Alle bestanden die beginnen met `file`, gevolgd door één letter, maar geen cijfer

    ```
    $ ls file[a-z]
    filea  fileb  filec  filed
    ```

4. Alle bestanden die beginnen met `file`, gevolgd door één cijfer, maar geen letter

    ```
    $ ls file[1-9]
    file1  file2  file3  file4  file5  file6  file7  file8  file9
    ```

5. De bestanden `file12` t/m `file16`

    ```
    $ ls file1[2-6]
    file12  file13  file14  file15  file16
    ```

6. Bestandern die beginnen met `file`, *niet* gevolgd door een `1`

    ```
    $ ls file[!1]
    file2  file4  file6  file8  filea  filec
file3  file5  file7  file9  fileb  filed

    ```

### Links

Maak in de directory `linux/` twee tekstbestanden aan, met naam `tekst1a` en `tekst2a`. Beide hebben als inhoud “Dit is bestand tekst1” en “Dit is bestand tekst2”, respectievelijk.

1. Voor het volgende commando uit en geef de uitvoer:

    ```
    [student@localhost linux]$ ls -l tekst*
-rw-rw-r--. 1 student student 22 2016-10-17 14:00 tekst1
-rw-rw-r--. 1 student student 22 2016-10-17 14:01 tekst2
    ```

2. Maak een *harde link* van `tekst1a` naar `tekst1b`
ln /home/student/linux/tekst1a /home/student/linux/tekst1b
3. Maak een *symbolische link* van `tekst2a` naar `tekst2b`
ln -s /home/student/linux/tekst2a /home/student/linux/tekst2b
4. Voor het volgende commando uit en geef de uitvoer:

    ```
   [student@localhost linux]$  ls -l tekst*
-rw-rw-r--. 2 student student 25 2016-10-17 15:01 tekst1a
-rw-rw-r--. 2 student student 25 2016-10-17 15:01 tekst1b
-rw-rw-r--. 1 student student 26 2016-10-17 15:01 tekst2a
lrwxrwxrwx. 1 student student 27 2016-10-17 15:04 tekst2b -> /home/student/linux/tekst2a

    ```

5. Hoe zie je aan de uitvoer van `ls` dat `tekst1b` een harde link is en `tekst2b` een symbolische? Tip: Vergelijk met de uitvoer uit vraag 1!

    **Antwoord**: tekst2b heeft een blauwe achtergrond en heeft pijl die verwijst naar 2a, ook de datum van het bestand is anders dan het originele.

6. Verwijder de oorspronkelijke bestanden, `tekst1a` en `tekst2a`. Maak het commando zo kort mogelijk!

    ```
    $ rm tekst1a tekst2a
    UITVOER
    ```

7. Toon opnieuw de uitvoer van `ls -l tekst*`, en bekijk de inhoud van `tekst1b` en `tekst2b`. Wat valt je op?

    ```
    $ ls -l tekst*
    -rw-rw-r--. 1 student student 25 2016-10-17 15:01 tekst1b
lrwxrwxrwx. 1 student student 27 2016-10-17 15:04 tekst2b -> /home/student/linux/tekst2a

    ```

    **Antwoord**: de symbolische link verwijst naar een bestand die niet meer bestaat en staat in het rood

### Bestanden archiveren

1. Creëer in je home-directory een archief `linux.tar.bz2` van de directory `linux/` en alle inhoud.

    ```
    $ $ tar -zcvf linux.tar.bz2 linux
linux/
linux/file2
linux/file4
linux/file6
linux/file7
linux/teskt2a
linux/file11
linux/tekst1b
linux/file16
linux/tekst2b
linux/filed
linux/fileb
linux/file12
linux/file10
linux/file13
linux/file8
linux/file9
linux/.hidden
linux/file17
linux/file1
linux/f/
linux/f/file1
linux/f/g/
linux/f/g/file2
linux/f/g/i/
linux/f/g/file1
linux/filec
linux/file5
linux/file18
linux/file14
linux/filea
linux/file19
linux/file15
linux/h/
linux/h/file4
linux/h/i/
linux/h/file1
linux/file3

    ```

2. Verwijder nu volledig de directory `linux/`

    ```
    $ rm -r linux
    UITVOER
    ```

3. Toon de inhoud van het archief zonder opnieuw uit te pakken

    ```
    $ cat linux.tar.bz2
    �X���n�0
           �}���,���}_�]�ś������C
                                  )��D�d���h
��WR�,�k��ߛJ3�R���)�
                      ���䣍�2di����5s:�ϯu]�Ӷ�����k���t���m�X����-���i�?\lU�;*���/���ÿ�����_��?��`�O��A�O$���<�f�}���ӋP���-�C����*<�}��]��/��(��z�c�p�*�_�d���*��J����M�?d�2քd��nv������7��>�����9��b1V��s���ٿT���;��U(��`����_�¿��f�'�נ���b��c�_����X
                         ��oB��B��Y,�?��
����v;|;�+�[���������/��3��
���5������V���M������������/�e�������O����A��d����_���1���9������?�����
��������8��B���E,�
���������U�U���_�5(���`����*���ǿG�����ݑ��a����B��b�X��
 ��c��B�/v����c�p3:�E/x
    ```

4. Pak het archief opnieuw uit in je home-directory.

    ```
tar -zxvf linux.tar.bz2
linux/
linux/file2
linux/file4
linux/file6
linux/file7
linux/file11
linux/tekst1b
linux/file16
linux/tekst2b
linux/filed
linux/fileb
linux/file12
linux/file10
linux/file13
linux/file8
linux/file9
linux/.hidden
linux/file17
linux/file1
linux/f/
linux/f/file2
linux/f/j/
linux/f/j/file4
linux/f/j/i/
linux/f/j/file1
linux/f/file1
linux/f/g/
linux/f/g/file2
linux/f/g/i/
linux/f/g/file1
linux/f/h/
linux/f/h/file4
linux/f/h/i/
linux/f/h/file1
linux/filec
linux/file5
linux/file18
linux/file14
linux/filea
linux/file19
linux/file15
linux/file3

    ```

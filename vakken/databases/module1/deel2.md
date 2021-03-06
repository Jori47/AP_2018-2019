# Deel 2
## Oefening 1
### 1a
```sql
create database ap;
```
```sql
create table afdeling (
    afdnr char(5) unique,
    budget decimal(8 , 2 ) not null,
    locatie varchar(30),
    telcontact char(13),
    isactief tinyint(1) default 0,
    gempunten decimal(5 , 2 )
);
```
```sql
insert into afdeling values('12345', 2000.25, 'Antwerpen', '(123)45 89 12', false, 12.43);
```

### 1b
```sql
create table tblopleiding
(
    opleidingscode char(10) primary key,
    omschrijving varchar(8000),
    duur tinyint(4)
);
```
```sql
create table tblafdeling
(
    afdelingnr int auto_increment primary key, /*auto_increment: default start-waarde = 1*/
    naam varchar(100),
    replicatiecode char(32)
);
```
```sql
create table tblmedewerker
(
    medewerkernr int auto_increment primary key,
    naam varchar(100),
    adres varchar(200),
    afdelingnr int,
    foreign key (afdelingnr) references tblafdeling(afdelingnr)
);
```
```sql
create table tblgevolgdeopleidingen
(
    medewerkernr int,
    foreign key (medewerkernr) references tblmedewerker(medewerkernr),
    opleidingscode char(10),
    foreign key (opleidingscode) references tblopleiding(opleidingscode),
    datum date,
    voltooing timestamp
);
```

### 1c
```sql
Create database renting;
```
```sql
create table tblFaciliteiten
(
    Faciliteitcode char(20) primary key,
    kookgelegenheid tinyint,
    douche_bad tinyint,
    aantalkamers tinyint
);
```
```sql
create table tblkamerbestand
(
    kamernr int primary key,
    adres varchar(50),
    plaats varchar(50),
    huurprijs dec,
    faciliteitcode char(20),
    foreign key (faciliteitcode) references tblfaciliteiten(faciliteitcode)
);
```
```sql
create table tblstudent
(
    studentnr int primary key,
    naam varchar(50),
    studentadres varchar(50),
    studentplaats varchar(50)
);
```
```sql
create table tblhuurcontract
(
    studentnr int,
    foreign key (studentnr) references tblstudent(studentnr),
    kamernr int,
    foreign key (kamernr) references tblkamerbestand(kamernr),
    contractduur timestamp,
    datumeindecontract date
);
```

### 1d
```sql
create table tblstudent
(
    studentnr int auto_increment primary key,
    naam varchar(100),
    adres varchar(100),
    plaats varchar(100),
    geboortedatum date
);
```
```sql
create table tblcursus
(
    cursusnr int primary key,
    cursusomschrijving varchar(1000)
);
```
```sql
create table tblmodule
(
    cursusomschrijving varchar(500),
    foreign key (cursusomschrijving) references tblcursus(cursusomschrijving),
    modulenr int primary key,
    onderdeel varchar(100),
    omschrijving varchar(500)
);
```
```sql
create table tblresultaat
(
    studentnr int,
    foreign key (studentnr) references tblstudent(studentnr),
    cursusnr int,
    foreign key (cursusnr) references tblcursus(cursusnr),
    modulenr int,
    foreign key (modulenr) references tblmodule(modulenr),
    datum date,
    resultaat dec(4,2)
);
```
## Oefening 2
```sql
create table SPELERS_KOPIE
(
    partnervan int,
    voorletters char(4)
)
AS
(
    SELECT * FROM Tennis.Spelers WHERE plaats = "Den Haag"
);
```
```sql
SELECT * FROM spelers_kopie;
```
## Oefening 3
```sql
create table lessen
(
    lesnr char(5) not null,
    spelersnr int,
    aanwezig tinyint,
    lesdatum date,
    primary key(lesnr, spelersnr),
    unique(spelersnr, lesdatum),
    foreign key(spelersnr) references spelers1(spelersnr)
	on delete cascade /*les verwijderen bij het verwijderen van een speler*/
        on update cascade /*update bij het aanpassen van een speler*/
);
```

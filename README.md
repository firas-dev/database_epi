# database_epi
epi sql 
https://www.mediafire.com/file/2ycyuze6sdhk6v9/TPBD1.docx/file
create table client(
idCL char(7) primary key,
NomCL char(7) NOT NULL, 
PrenomCL char(7), 
AdrCL char(7) NOT NULL, 
Email char(7) UNIQUE check(Email LIKE '%@%') NOT NULL
);
create table produit(
CodP char(8) primary key,
Lib char(8) NOT NULL, 
PU number(7),
QteS number(7) CHECK (QteS>0), 
StkMin number(7) CHECK (StkMin between 10 and 50)
);

create table commande(
Numc number(4) primary key, 
DateC date , 
MontantC number(7),
IDpan number(5),
Foreign key (IDpan)  REFERENCES Panier(IDpan)  

);

create table panier(
IDpan number(5) primary key, 
idCL char(7)  ,
Foreign key (idCL)  REFERENCES client(idCL) 
);

 create table LignePanier(
 IdLigPAn number(5) primary key, 
 CodP char(8),
 Qte number(7) CHECK(Qte>0),
 IDpan number(5),
 Foreign key (IDpan) REFERENCES Panier(IDpan),
 Foreign key (CodP) REFERENCES produit(CodP)
 ); 
 
 create table paiement(
 NumP number(5) primary key, 
 dateP date , 
 etat char(10) CHECK(etat IN('validé','Annuler')), 
 IDcarte number(7)  , 
 Numc number(4),
  Foreign key (IDcarte) REFERENCES carte(IDcarte),
   Foreign key (Numc) REFERENCES commande(Numc) 
 
 ); 
 
 create table carte(
IDcarte number(7) primary key, 
typeC varchar(20), 
dateExp date
 );
 
 DROP table CARTES; 
 
  ALTER TABLE CLIENT
  add(
  login char(5), 
  Password char(20)
  );
  
  ALTER TABLE Produit  MODIFY(Lib varchar(25));
  
  ALTER TABLE client MODIFY(
NomCL varchar(25) ,  
PrenomCL varchar(25) ,
AdrCL  varchar(25) ,
login  varchar(25) ,
Email varchar(25) ,
Password check(length(Password)>=10)
  );
  
  alter table Produit add(
  constraint ck_Qtes check(QteS>=StkMin)
  );
  
    alter table Client add(
  constraint cemailoblig check(Email is not null)
  );
  
    alter table Client add(
  constraint cmpassloblig check(Password is not null and length(Password)>=10)
  );
  
  insert into Produit (CodP,Lib,PU,QteS,StkMin)
  values(100,'robe',200,50,23);
  
    insert into Produit (CodP,Lib,PU,QteS,StkMin)
  values(101,'jupe40',150,200,25);
  
    insert into Produit (CodP,Lib,PU,QteS,StkMin)
  values(102,'costume33',400,1000,10);
  
    insert into Produit (CodP,Lib,PU,QteS,StkMin)
  values(103,'pull02',100,500,42);
  
    insert into Produit (CodP,Lib,PU,QteS,StkMin)
  values(100,'PArfum YSL',785,150,20);
  
  
    insert into client (idCL,NomCL,PrenomCL,AdrCL,Email,login,Password)
  values(789,'Sami','bensalah','sousse','sami@yahoo.com','SAmibensalah01','SBS01sbssss');
  
    insert into client (idCL,NomCL,PrenomCL,AdrCL,Email,login,Password)
  values(790,'Ali','benmoahemd','kairouan','ali@gmail.fr','alibenmed02','ABM02abm');
  
    insert into client (idCL,NomCL,PrenomCL,AdrCL,Email,login,Password)
  values(791,'Moez','Mohamed','Tunis','moez@gmail.com','Moezmed03','MM03mm');
  
    insert into client (idCL,NomCL,PrenomCL,AdrCL,Email,login,Password)
  values(792,'rami','benmahmoud','sousse','rami@gmail.com','Ramibenmah04','RBM04rbm');
  
    insert into client (idCL,NomCL,PrenomCL,AdrCL,Email,login,Password)
  values(793,'Hana','benYoussef','djerba','hana@outlook.fr','HAnaYSf05','HBY05hby');
  
     insert into client (idCL,NomCL,PrenomCL,AdrCL,Email,login,Password)
  values(794,'Malak','Mestiri','Monastir','malak@hotmail.fr','MAlakHM06','MMMo06mmO');
  
  delete from client where NomCL='Sami';
  
  UPDATE Client set AdrCL='Nabeul'
  where idCL=790;

  
  UPDATE Produit SET PU=250
  WHERE PU=200;

select * from Client 
where AdrCL='sousse';

select * from Produit 
where QteS between 10 and 50;

select * from Client 
where substr(NomCL,2,1)='a';

select * from Client 
where NomCL like'%i%';

# PROJECTE DELINQÜÈNCIA AL CARRER

PUNT DE PARTIDA DEL PROJECTE: Estudiar diverses variables que poden influir en la deliqüéncia al carrer a Catalunya. Contrastar amb dades si te fonament la percepció de la població, fomentada per alguns mitjans, de la relació entre la inseguretat ciutadana i l'arribada de menors no acompanyats.   

OBJECTIUS: 
* Realitzar l'anàlisis i les visualitzacions de les dades per tal de respondre les preguntes clau.
* Analitzar la relació entre delinqüència als carrers i afluéncia de menors no acompanyats. Aprofundir en la delinqüència juvenil i la seva relació amb el menors no         
  acompanyats i la inseguretat als carrers. 
* Buscar dades d'altres variables que puguin tenir relació amb la delinqüència als carres com ara l'afluència de turistes a Catalunya.

PREGUNTES CLAU: 
* Es certa relació entre menors no acompanyats i deliqüéncia als carrers? Que en diuen les dades?
* Quina es la relació entre turisme i deliqüéncia als carrers? 
* Quina es la tendéncia dels últims anys en delinqüència als carrer i juvenil.

METODOLOGIA: Partint de dades públiques del portal de transparència de la Generalitat de Catalunya, de l'IDESCAT, del departament de justícia, de la conselleria de turisme i del departament de drets socials i inclusió, obtinc les bases de dades per formar el meu dataset. Examino i valido les dades amb MySQL per després realitzar el modelat i les visualitzacions amb PowerBi.

DADES:
* Visitans estrangers
  * https://
* Estadístiques justícia juvenil
  * https://justicia.gencat.cat/ca/departament/Estadistiques/justicia_juvenil/
* Fets penals
  * https://analisi.transparenciacatalunya.cat/Seguretat/Fets-penals-coneguts-fets-coneguts-resolts-i-deten/qnyt-emjc/explore
* Noves arribades d'infants i joves migrats
  * https://analisi.transparenciacatalunya.cat/Demografia/Noves-arribades-d-infants-i-joves-migrats-sols-a-C/pvrz-iijx/about_data
* Per la visualització de mapes utilitzo el mapa de catalunya per comarques .json  publicat per Xavier Ginménez
  * https://github.com/sirisacademic/catalonia-cartography/blob/master/shapefiles_catalunya_comarcas.topo.json
     
 
PRIMERES CONCLUSIONS:

![image](https://github.com/user-attachments/assets/0d49d539-b6c0-41fa-895b-1837f96c930d)

En una primera aproximació a les dades comprovo que l'augment de la delinqüència al carrer (Furts, robatoris, delictes sexuals, alteració de l'ordre públic, etc) te un patró estacional i guarda una estreta relació amb l'augment de visitants a l'estiu. Per contra no sembla que l'arribada de menors no acompanyats (que es manté estable cada any) ni l'evolució de la població de justicia juvenil segueixin aquest patró.
Amb aquest informació aprofundeixo en la recerca de dades. 

Estructuro l'estudi en diferentes dashboards:

* FETS PENALS Vs ARRIBADES MENORS DE NO ACOMPANYATS

  ![image](https://github.com/user-attachments/assets/5070936a-adde-4e4d-b915-ec2d9ff02900)
  

  * En un gràfic de línies es veu clarament la manca de relació entre les dues variables.
  * Analitzo la composició del menors no acompanyats per sexe, país de procedència i lloc d'arribada a Catalunya. Per fer aquesta útlima variable només disposo de les     
    regions dels serveis territorials. Aquestes no es corresponen exactament amb provincies ni amb comarques. Tampoc disposo de major granularitat d'aquesta dada però            decideixo, deixant de banda el rigor de les dades, obtenir les arribades per comarca:
      * Creo una taula amb MySQL amb les comarques i la importo al model a Power Bi.
        
        ![image](https://github.com/user-attachments/assets/e138f678-8978-44fc-8220-0b2db701de5d)

      * Creo una columna calculada amb DAX d'Id de Regió:
        
        ![image](https://github.com/user-attachments/assets/53714233-149b-4606-8b02-ab5762004f57)
        
      * Baixo un mapa publicat per Xavier Ginménez amb format .json i l'utilitzo de plantilla per fer una visualització de mapa de formes a Power Bi.
        
      * Creo una columna calculada amb DAX per assignar les comarques a cada regió del servei territorial.
        
        ![image](https://github.com/user-attachments/assets/2d57acce-0947-4575-96af-7f1555a7b569)
        
      * Creo una columna calculada en DAX per distribuint les arribades a cada regió per comarques.
 
        ![image](https://github.com/user-attachments/assets/35ee060e-3e18-4f21-999a-949d0a6414d9)
        
      * Creo una columna calculada en DAX per aplicar una ponderació a les diferents comarques en funció de la seva població, extensió i desenvolupament urbà.
        
        ![image](https://github.com/user-attachments/assets/aeb2707d-fd19-48f8-9163-d5d83af38429)        
      
    
* FETS PENALS Vs POBLACIÓ JUSTICIA JUVENIL 
  * Analitzo les tendéncies i la relació entre fets penals i la població de justicia juvenil, la composició d'aquesta població i la proporció respecte els fets penals totals.
    *  S'observa que segueixen una mateixa tendéncia i que hi ha relació entre les dues.
    *  Per posar context analitzo la composició d'aquesta població i quina part dels fets penals totals son comesos per menors. Per fer-ho creo una columna calculada on sumo        als registres d'expedients anuals la taxa de reincidents.

      ![image](https://github.com/user-attachments/assets/a7f40f23-ef02-4aa6-ac56-8c4b888035f5)



* POBLACIÓ JUSTICIA JUVENIL Vs ARRIBADES MENAS
  *

DASHBOARD FINAL:

![image](https://github.com/user-attachments/assets/67f2ae64-9bd6-4443-9f00-7887a91f6969)


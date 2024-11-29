# PROJECTE DELINQÜÈNCIA AL CARRER

PUNT DE PARTIDA DEL PROJECTE: Estudiar diverses variables que poden influir en la deliqüéncia al carrer a Catalunya. Contrastar amb dades si te fonament la percepció de part de la població, fomentada per alguns mitjans, de la relació entre la inseguretat ciutadana i l'arribada de menors no acompanyats.   


OBJECTIUS: 
* Realitzar l'anàlisis i les visualitzacions de les dades per tal de respondre les preguntes clau.
* Analitzar la relació entre delinqüència als carrers i afluéncia de menors no acompanyats. Aprofundir en la delinqüència juvenil i la seva relació amb el menors no         
  acompanyats i la inseguretat als carrers. 
* Buscar dades d'altres variables que puguin tenir relació amb la delinqüència als carres com ara l'afluència de turistes a Catalunya.


PREGUNTES CLAU: 
* Es certa relació entre menors no acompanyats i deliqüéncia als carrers? Que en diuen les dades?
* Quina part del delictes al carrer els cometen joves estrangers?
* Quina es la tendéncia dels últims anys en delinqüència als carrer i delinqüència juvenil? Guarden relació?
* Quina es la relació entre turisme i deliqüéncia als carrers?


METODOLOGIA: Partint de dades públiques del portal de transparència de la Generalitat de Catalunya, de l'IDESCAT, del departament de justícia, de la conselleria de turisme i del departament de drets socials i inclusió, obtinc les bases de dades per formar el meu dataset. Examino i netejo les dades amb MySQL i Pyhton, per després realitzar el modelat i les visualitzacions amb PowerBi.

El model no es un model normalitzat típic d'estrella ja que hi ha moltes taules de fets diferents i poques de dimensions. Creo una taula de dimensió temporal (data) i vinculo totes les taules de fets que tenen temporalitat a aquesta. També creo una de dimensió geogràfica (Catalunya Comarques) a la que vinculo les taules de fets amb referències geogràfiques.
El model resultant es força atípic, amb moltes taules de fets sense conexió entre elles i dues de dimensions:


![image](https://github.com/user-attachments/assets/2d0cdf8f-ff3c-400e-a31c-d850c447e810)


DADES:

* Estadístiques justícia juvenil
  * https://justicia.gencat.cat/ca/departament/Estadistiques/justicia_juvenil/
* Fets penals
  * https://analisi.transparenciacatalunya.cat/Seguretat/Fets-penals-coneguts-fets-coneguts-resolts-i-deten/qnyt-emjc/explore
* Noves arribades d'infants i joves migrats
  * https://analisi.transparenciacatalunya.cat/Demografia/Noves-arribades-d-infants-i-joves-migrats-sols-a-C/pvrz-iijx/about_data
* Per la visualització de mapes utilitzo el mapa de catalunya per comarques .json  publicat per Xavier Ginménez
  * https://github.com/sirisacademic/catalonia-cartography/blob/master/shapefiles_catalunya_comarcas.topo.json
* Població
  * https://www.idescat.cat/pub/?id=censph&n=16354&geo=prov:08 
* Visitans estrangers
  * https://www.idescat.cat/visor/?id=turest&dataset=1&tc=true&tm=factor_ind_factor&td=t.mes,terr.ccaa,mv.mv,tv.tv&tf=t.mes[202409]&cc=true&cm=factor_ind_factor&cd=t.mes,terr.ccaa,mv.mv,tv.tv&cf=t.mes[202409]&filters=temps_24050.202409&filters=territori_emtf_25077.09&rows=n4_emtf_dim_motiu_princ_viatg_25076&columns=n4_emtf_dim_codi_questionari_25072&filters=concept.factor_ind_factor
  * https://www.idescat.cat/indicadors/?id=aec&n=15518
     
 
PRIMERES OBSERVACIONS:

* ANÀLISI EXPLORATORI

  
  ![image](https://github.com/user-attachments/assets/0b4297c0-cb32-42af-bafb-8df7d94999f7)


En una primera aproximació a les dades comprovo que l'augment de la delinqüència al carrer (Furts, robatoris, delictes sexuals, alteració de l'ordre públic, etc) te un patró estacional i guarda una estreta relació amb l'augment de visitants a l'estiu. Per contra no sembla que l'arribada de menors no acompanyats (que es manté estable cada any) ni l'evolució de la població de justicia juvenil segueixin aquest patró.


  ![image](https://github.com/user-attachments/assets/9d1b59ef-dbb6-4bf2-815d-62c58715494d)


Implemento dos models de regressió lineal amb una visualització de gràfic de dispersió i comprobo estadísticament que delictes i arribades de menors no guarden relació, mentre que delictes i turistes sí.

Amb aquest informació aprofundeixo en la recerca i en l'anàlisis de dades. 

Decidedixo estructurar l'estudi en diferentes dashboards comparant entre elles les dades de delinqüència al carrer, arribades de menors migrants, població de justícia juvenil i turisme, en clau temporal i geogràfica. Afegeixo una pàgina de conclusions al final i un link a cada Dashboard per navegar-hi.


* DELICTES AL CARRER I ARRIBADES MENORS DE NO ACOMPANYATS


  ![image](https://github.com/user-attachments/assets/86b1f9d6-aed7-4eb9-89a7-5adac05abe5e)



  
  * En un gràfic de línies, amb series temporals, no s'aprecia una relació directa entre les dues variables.
    
  * Analitzo la composició del menors no acompanyats per sexe, país de procedència i lloc d'arribada a Catalunya.
    Per fer aquesta útlima variable només disposo de les regions dels serveis territorials. Aquestes no es corresponen exactament amb provincies ni amb 
    comarques. Tampoc disposo de major granularitat d'aquesta dada però decideixo, intentant mantenir cert rigor, obtenir les arribades per comarca:
    
      * Creo una taula amb MySQL amb les comarques i la importo al model a Power Bi.
        
        ![image](https://github.com/user-attachments/assets/e138f678-8978-44fc-8220-0b2db701de5d)

      * Creo una columna calculada amb DAX d'Id de Regió:
        
        ![image](https://github.com/user-attachments/assets/53714233-149b-4606-8b02-ab5762004f57)
        
      * Baixo un mapa publicat per Xavier Giménez amb format .json i l'utilitzo de plantilla per fer una visualització de mapa de formes a Power Bi.
        
      * Creo una columna calculada amb DAX per assignar les comarques a cada regió del servei territorial.
        
        ![image](https://github.com/user-attachments/assets/2d57acce-0947-4575-96af-7f1555a7b569)
        
      * Creo una columna calculada en DAX per distribuint les arribades a cada regió per comarques.
 
        ![image](https://github.com/user-attachments/assets/35ee060e-3e18-4f21-999a-949d0a6414d9)
        
      * Creo una columna calculada en DAX per aplicar una ponderació a les diferents comarques en funció de la seva població, extensió i desenvolupament urbà.
        
        ![image](https://github.com/user-attachments/assets/aeb2707d-fd19-48f8-9163-d5d83af38429)        
      
    
* DELICTES AL CARRER I POBLACIÓ JUSTICIA JUVENIL


  ![image](https://github.com/user-attachments/assets/ce766c38-93c0-4b48-9fac-e13ce6d5ad5e)




  * Analitzo les tendéncies i la relació entre fets penals i la població de justicia juvenil, la composició d'aquesta població i la proporció respecte els fets penals totals.
    *  S'observa que segueixen una mateixa tendéncia i que hi ha relació entre les dues.
    *  Per posar context, analitzo la composició d'aquesta població i quina part dels fets penals totals son comesos per menors. Per fer-ho creo una columna 
       calculada on sumo als registres d'expedients anuals totals el nombre de reincidents amb expedients anteriors.

        ![image](https://github.com/user-attachments/assets/a7f40f23-ef02-4aa6-ac56-8c4b888035f5)

    *  Faig una estimació de quin percentatge del total de delictes son comesos per menors estrangers (no necessariament menors migrants no acompanyats). A
       la base de dades de justicia juvenil, no diposem del detall de quin tipus de delicte cometen els menors. Tampoc de quina edat tenen els que cometen 
       delictes a la base de dades de fets penals coneguts.
       Per tant faig una estimació multiplicant el percentatge de delictes comesos per menors del total pel percentatge d'estrangers de la població de justicia juvenil.

        ![image](https://github.com/user-attachments/assets/9c5961b6-c832-478e-a59d-0495a7142763)

       

* POBLACIÓ JUSTICIA JUVENIL I ARRIBADES DE MENORS MIGRANTS NO ACOMPANYATS (MENAS)


  ![image](https://github.com/user-attachments/assets/f6919307-6cbe-4176-9da8-db6d0c447c1f)



  * Comparo l'evolució de la Població Justicia Juvenil amb les Arribades de Menors. No hi ha relació aparent.
  * Comparo l'evolució de la Població Justicia Juvenil amb la de la població general de 14 a 21. Tampoc hi ha un relació clara.
  * Comparo el percentatge de la població total amb edats entre 14 i 21 vs el percentatge de delictes comesos per joves de 14 a 21 respecte els totals.
    Per fer-ho creo aquesta mesura:

    ![image](https://github.com/user-attachments/assets/69920899-c193-430b-86ce-4602933dd19d)

  * Per contextualitzar creo una mesura per calcular la proporció que representen el menors no acompanyats respecte la població total de 14 a 18 anys. 
 
    ![image](https://github.com/user-attachments/assets/6d54392b-2401-486e-a9fa-6228f8aa8529)



* DELICTES AL CARRER I TURISME

  ![image](https://github.com/user-attachments/assets/827289f4-ff5d-4bcb-973c-af45e8c3c3f7)



 * Començo comparant la serie temporal de delictes vs la d'arribades de turistes. La relació es evident. El delictes tenen un comportament estacional igual al de les visites de turistes.
   
* Per comparar la distribució geogràfica dels delictes i de visites de turistes no disposo de la distribució d'arribades de turistes per comarca. Així que les calculo, en una columna calculada, unint les dades de places turístiques de cada tipus disponibles per comarca i les taxes d'ocupació d'aquestes places per cada tipus del 2022.

  ![image](https://github.com/user-attachments/assets/c1ecb73e-d6b7-40f6-b996-73b06969d209)
  
* Per poder obtenir els delictes per comarca creo una columna calculada assignant un Id de Regió Policial a cada regió.

  ![image](https://github.com/user-attachments/assets/76b117b2-56d7-4bad-8ff5-fe750a3a3125)

* Creo una altra columna calculada a la taula de dimensions geogràfiques Comarques Catalunya per tal que a cada ABP (Àrea Bàsica Policial) li correspongui una comarca. M'ajudo de Chat GPT per fer la columna DAX.

   ![image](https://github.com/user-attachments/assets/e5a12ea8-9782-4b96-aece-620e50ea5f72)

* Ho aplico a la visualització de mapes amb la plantilla de comarques per poder comparar la distribució geogràfica de turisme i delictes al carrer.
  S'aprecía coincidencia en les comarques costaneres i les capitals de provincia, terte de Lleida.
  Filtrant la serie temporal per comarques, s'aprecia que les comarques on coincideixen alts index de delinqüència i visitants també hi ha una relació 
  d'estacionalitat a la serie temporal.
* Elaboro un gràfic de columnes de comarques ordenat per delinqüència on s'aprecia que la relació entre les dues variables.


* CONCLUSIONS

   ![image](https://github.com/user-attachments/assets/c5543a15-b6c4-4140-91da-282f9215492d)




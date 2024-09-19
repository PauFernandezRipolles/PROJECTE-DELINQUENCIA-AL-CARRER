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
* Quina es la tendéncia dels útlims anys en delinqüència als carrer i juvenil.

METODOLOGIA: Partint de dades públiques de l'IDESCAT, del departament de justícia, de la conselleria de turisme i del departament de drets socials i inclusió, examino i valido les dades amb MySQL per després realitzar el modelat i les visualitzacions amb PowerBi.

DADES:
* Visitans estrangers
  * https://
* Estadístiques justícia juvenil
  * https://
* Fets penals
  * https://analisi.transparenciacatalunya.cat/Seguretat/Fets-penals-coneguts-fets-coneguts-resolts-i-deten/qnyt-emjc/explore
* Noves arribades d'infants i joves migrats
  * https://
 
PRIMERES CONCLUSIONS:

![image](https://github.com/user-attachments/assets/0d49d539-b6c0-41fa-895b-1837f96c930d)

En una primera aproximació a les dades comprovo que l'augment de la delinqüència "al carrer" (Furts, robatoris, delictes sexuals,etc) te un patró estacional i guarda una estreta relació amb l'augment de visitants a l'estiu. Per contra no sembla que l'arribada de menors no acompanyats (que es manté estable cada any) ni l'evolució de la població de justicia juvenil segueixin aquest patró.

Amb aquest informació aprofundeixo en la recerca de dades. 

Estructuro l'estudi en diferentes dashboards:

* FETS PENALS Vs POBLACIÓ JUSTICIA JUVENIL 
  * Les dades de població en justicia juvenil están segmentades en població per cada tipologia d'intervenció i en cadascuna d'elles consta el percentatge de cada tipologia       de delicte o falta. Amb aquesta informació creo columnes calculades per obtenir el nombre de delictes i faltes totals comesos per la població en justicia juvenil.
  * Analitzo les tendéncies i la relació entre fets penals i la població de justicia juvenil, la composició d'aquesta població i la proporció respecte els fets penals totals.

* FETS PENALS Vs ARRIBADES MENAS
  *
* POBLACIÓ JUSTICIA JUVENIL Vs ARRIBADES MENAS
  *


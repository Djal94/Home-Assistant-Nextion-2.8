## Mise en place d'un écran de contrôle/notification pour Home Assistant




![Nextion](https://user-images.githubusercontent.com/35771339/225013109-b3ed8c40-9fef-4b1d-8148-c2848ab0bb86.jpeg)


### Fonctions : 

- *Indicateurs (points de couleur) de connectivité WIfi/Home Assistant*
- *Date/Heure/Météo*
- *Indicateurs de présence des personnes avec bascule de chaque visage en couleur/N&B*
- *Notification de courrier avec icône enveloppe qui clignote et indicateur du nombre de passages.*
- *Bouton d’ouverture du portail extérieur.*
- *Gestion de l’alarme : Quand l’alarme est activée, il bascule sur un écran vérouillé, et sur un pavé numérique au touché qui permet de désarmer l’alarme avec un code.*
- *La ligne du bas, c’est 4 icônes de notification du ramassage des poubelles, qui prennent la couleur de la poubelle le jour du ramassage.*
- *Ecran éteint lorsque la maison est en mode absent*
- *service pour controler la luminosité depuis HA*

L’idée de cet écran est de le placer juste a coté de la porte d’entrée (intérieur).

#### *Les fonctionalités sur cet ecran ne sont pas nouvelles pour moi, et existent déjà sur mon HA. Il s'agit uniquement de les deporter* - je n'explique pas ici comment mettre en place celles-ci.


### Matériel nécéssaire : 

- Un écran Nextion 2.8P, mais vous pouvez prendre le modèle que vous voulez
    [Ecran Nextion 2.8P](https://fr.aliexpress.com/item/4000593543479.html)
    
- Un controleur de type ESP8266, j'ai pris un Wemos D1 mini. Pensez a en prendre un avec un port USB et des broches, sinon ca va etre plus pénible à alimenter/connecter
    [Wemos D1 Mini](https://fr.aliexpress.com/item/32631693796.html)
    
- [L'éditeur Nextion](https://nextion.tech/nextion-editor/) pour programmer votre écran

- Le module complémentaire [ESPHOME](https://esphome.io/guides/getting_started_hassio.html) pour Home Asisstant, pour programmer votre ESP facilement depuis HA

- Le boitier externe est une impression 3D, voici le fichier .stl, il n'est pas de moi, [vous le trouverez ici](https://cults3d.com/fr/mod%C3%A8le-3d/divers/case-for-nextion-2-8-inches)
### Connexion ESP/Ecran :

 Rien de compliqué ici :
 
 Connectez le RX du Wemos sur le TX de l'écran, le TX du Wemos sur le RX de l'écran, le 5v de l'écran sur le 5v du Wemos, et la terre sur la terre.
 Le Wemos est quand à lui alimenté via le porte USB
 
 
 ### Interface du Nextion : 
 
 ![image](https://user-images.githubusercontent.com/35771339/225095754-c85a02aa-c55a-4bff-8a01-97f23bece094.png)![image](https://user-images.githubusercontent.com/35771339/225095383-daa44c48-be16-4f7a-8566-af4a89afb829.png)![image](https://user-images.githubusercontent.com/35771339/225095476-81ce4af2-d161-485c-97b5-003d50e8fdfd.png)


  Pour programmer l'interface du Nextion, il faut récuperer [l'éditeur Nextion](https://nextion.tech/nextion-editor/)
  Vous pouvez charger mon fichier nextion.tft, et adaptez en fonction de vos besoins. N'hésitez pas à consulter [la documentation](https://nextion.tech/editor_guide/)
  
  Pour charger le fichier sur votre Nextion, cliquer sur File/TFT File Output, copier/coller le fichier .tft sur une carte micro SD à la racine, et alimentez votre       ecran. Une fois l'Update Successfull, éteignez l'ecran, sortez la micro SD et rebranchez -le, et voilà! votre écran est configuré!
  
  (Il existe aussi une méthode pour uploader le fichier en OTA (sans fil), mais cette méthode m'ayant posée pas mal de soucis et étant très inconsistante, je vais la passer)
  
  Mais ce n'est pas tout, pour pouvoir communiquer avec Home Assistant, il va falloir programmer votre ESP (Wemos ici) pour qu'il récupère les infos de HA et les envoie à votre écran. Ca passe par ESPHOME
  
  ### Configuration ESPHOME
  
  Commencez par installer le module complémentaire [ESPHOME](https://esphome.io/guides/getting_started_hassio.html) dans HA
  Voici un [petit guide des premiers pas sur ESPHOME](https://hacf.fr/esphome_installation)
  
  Je vous laisse avec la [documentation de ESPHOME](https://esphome.io/), et celle plus spécifique du [Composant Nextion](https://esphome.io/components/display/nextion.html)
  
  Encore une fois, récupérez mon fichier esp-nextion.yaml et adaptez selon vos besoins.
  
  #### Annexes : 
  
  - Excellent [sujet sur le forum HA de Argonaute](https://forum.hacf.fr/t/ecran-tactile-nextion-avec-esphome-deporter-vos-commandes/10622) duquel je me suis inspiré
  
  #### Je tiens a remercier Argonaute du Forum HA sans qui je n'aurai pas eu l'inspiration, [vous trouverez son github ici](https://github.com/argonaute199/Nextion28-home-assistant)

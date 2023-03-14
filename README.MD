## Mise en place d'un écran de contrôle/notification pour Home Assistant


![Nextion](https://user-images.githubusercontent.com/35771339/225013109-b3ed8c40-9fef-4b1d-8148-c2848ab0bb86.jpeg)


### Matériel nécéssaire : 

- Un écran Nextion 2.8P, mais vous pouvez prendre le modèle que vous voulez
    https://fr.aliexpress.com/item/4000593543479.html
    
- Un controleur de type ESP8266, j'ai pris un Wemos D1 mini. Pensez a en prendre un avec un port USB et des broches, sinon ca va etre plus pénible à alimenter/connecter
    https://fr.aliexpress.com/item/32631693796.html
    
- L'éditeur Nextion pour programmer votre écran : https://nextion.tech/nextion-editor/

- Le module complémentaire ESPHOME pour Home Asisstant, pour programmer votre ESP facilement depuis HA : https://esphome.io/guides/getting_started_hassio.html


### Connexion ESP/Ecran :

 Rien de compliqué ici :
 
 Connectez le RX du Wemos sur le TX de l'écran, le TX du Wemos sur le RX de l'écran, le 5v de l'écran sur le 5v du Wemos, et la terre sur la terre.
 Le Wemos est quand à lui alimenté via le porte USB
 
 
 ### Interface du Nextion : 

  Pour programer l'interface du Nextrion, il faut récuperer l'Editeur Nextion ici : https://nextion.tech/nextion-editor/
  Vous pouvez charger mon fichier nextion.tft, et adaptez en fonction de vos besoins. N'hésitez pas à consulter la documentation : https://nextion.tech/editor_guide/
  
  Pour charger le fichier sur votre Nextion, cliquer sur File/TFT File Output, copier/coller le fichier .tft sur une carte micro SD à la racine, et alimentez votre       ecran. Une fois l'Update Successfull, éteignez l'ecran, sortez la micro SD et rebranchez -le, et voilà! votre écran est configuré!
  
  (Il existe aussi une méthode pour uploader le fichier en OTA (sans fil), mais cette méthode m'ayant posée pas mal de soucis et étant très inconsistante, je vais la passer)
  
  Mais ce n'est pas tout, pour pouvoir communiquer avec Home Assistant, il va falloir programmer votre ESP (Wemos ici) pour qu'il récupère les infos de HA et les envoie à votre écran. Ca passe par ESPHOME
  
  ### Configuration ESPHOME
  
  Commencez par installer le module complémentaire ESPHOME dans HA : https://esphome.io/guides/getting_started_hassio.html
  Voici un petit guide des premiers pas sur ESPHOME: https://hacf.fr/esphome_installation
  
  Je vous laisse avec la documentation de ESPHOME, et celle plus spécifique du composant Nextion : https://esphome.io/ et https://esphome.io/components/display/nextion.html
  
  Encore une fois, récupérez mon fichier nextion.yaml et adaptez selon vos besoins.
  
  #### Annexes : 
  
  - Excellent sujet sur le forum HA de Argonaute duquel je me suis inspiré : https://forum.hacf.fr/t/ecran-tactile-nextion-avec-esphome-deporter-vos-commandes/10622

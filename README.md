# Tp_Spring_Cloud_Streams_Fucntions_Kafka

## L'objectif:

c'est generalement comment utiliser kafka dans une application spring boot.

donc on va creer une applicaton spring boot dont on va voir comment a partir d’un Rest Controller on peut evoyer un messag vers un topic kafka

## Initialisation:

Kafka fonctionne avec ZooKeeper, une plateforme permettant de créer ou maintenir un serveur open-source. Il est nécessaire de démarrer une instance de ZooKeeper pour pouvoir utiliser Kafka. Une fois que vous avez démarré ZooKeeper, vous devez faire de même pour la plateforme Kafka.

### A) Demmarer zookeper :

![image](https://user-images.githubusercontent.com/102171913/173114525-bfda6378-5dc4-4afe-bc59-c22db90c35e2.png)

### B) Demmarer kafka :

![image](https://user-images.githubusercontent.com/102171913/173114623-8ab86b10-7b03-4f51-be0b-96ac9f0b7160.png)

### Test:

*kafka-consumer* permet de consom un topic et visualiser les donner qui consommer par un topic

*kafka-produser* envoyer des message vers un topic kafka 

### C) Lancement de Kafka-Consumer et kafka-Producer::

![image](https://user-images.githubusercontent.com/102171913/173115966-b6455e81-4ea4-412d-bc27-fb4858e865a1.png)

## Partie1:

On va creer une application spring boot qui  produire des message vers un topic et on va les surveiller utilisant kavka-consumer.

d'abord on specifie les dependences qu'on a besoin

![image](https://user-images.githubusercontent.com/102171913/173116822-b186a02a-c484-4db2-ad71-8295adea8042.png)

### Test:

J’ai lancer kafka-consumer et mon application via  RestController et un browser et j’envoi une Requette http avec get, le RestController recupere les parametres et les republier dans le topic R1

![image](https://user-images.githubusercontent.com/102171913/173117830-7a938a5c-3ac3-483a-9e3d-4e40889f18d3.png)

## Partie2:

Au lieu d’utiliser kafka-consumer on va cree une appliction de type consumer 

Pour tester :

Le consumer faire un subscribe ver R1, on a envoyer un message a travers kafka-producer ou le browser  et on visualise les message dans notre application consumer

### A travers le browser :

![image](https://user-images.githubusercontent.com/102171913/173118496-311056b5-c819-42f6-81ad-9af90acac843.png)

### A travers kafka-Producer

![image](https://user-images.githubusercontent.com/102171913/173118515-186d4bb5-e5ce-4079-9d62-e305a1644409.png)

## Partie3:

Creer un producer de type supplier qui produire un evenement chaque seconde a l'aide d'un timer par defaut ou bien on peut specifier le delay par:
### ->spring.cloud.stream.poller.fixed-delay=delay 

### Test: R2

![image](https://user-images.githubusercontent.com/102171913/173118798-2b15ab6b-d845-4846-9724-c2b8a062d5b2.png)

## Partie4 :

Creation d'Une application (in out) dont laquelle elle recoie un enregitrement et elle fait un traitement et puis produit un autre stream on sortie qui l'envoi vers un autre topic

### Teste 1 : input R1 output R3

![image](https://user-images.githubusercontent.com/102171913/173119108-c69b3a59-a0d5-4357-be08-f7043c1a7638.png)

### Test 2 : input R2 et output R3

![image](https://user-images.githubusercontent.com/102171913/173119192-3b5d9133-a0f9-4b14-8a55-023ec4480ecb.png)

## Partie5:

On va Faire Stream processing (on a pas besoin de traitement distribuée) et avoir comment utiliser kafka stream,
on va creer une fonction qui reçoie on input le clé(nom de la page) et la valeur (nombre de fois a été visiter)
l'avantage on peut léutiliser dans 

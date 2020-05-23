Le but de ce poste est de répondre aux questions relatives à la haute disponibilité suivantes:

* Comment on peut lancer dynamiquement plusieurs instances d'un µservice ?
* Comment Ribbon et Eureka fonctionnent ensemble ?

## 1) Comment on peut lancer dynamiquement plusieurs instances d’un µservice  ?

Pour lancer dynamiquement plusieurs instances d'un µservice on peut utiliser la configuration suivante :

```properties
server.port=0
eureka.instance.prefer-ip-address=true
eureka.instance.hostname=${spring.application.name}
eureka.instance.instance-id==${spring.cloud.client.hostname}:${spring.application.name}:${spring.application.instance_id:${random.value}}
```

NB: Si vous utlisez la version Spring Cloud Dalston.SR4, cette config ne va pas marcher dans un contexte SSL, à cause du bug mentionné ici https://github.com/spring-cloud/spring-cloud-netflix/issues/2303. C'est pour cela il est très important de rester toujours à jour avec la version Spring boot et Spring cloud
                              

## 2) Comment Ribbon et Eureka fonctionnent ensemble ?

Ribbon vérifie la disponibilité des serveurs destinations en se basant sur une stratégie de Ping. 
Celle configurée par défaut est l'implementation NIWSDiscoveryPing.
Mais il se trouve que contrairement à ce qu'on aurait pensé, avec cette stratégie Ribbon ne va jamais faire de pings réels pour s'assurer de la disponibilité des destinations,
cette vérification sera plutôt déléguée au composant eureka-client qui maintient une copie de la liste de l'ensemble des µservices censés être UP   

Le NIWSDiscoveryPing reste une stratégie parmi d'autres qu'on peut à moment modifier avec la propriété :

```properties
 <sample-client>.ribbon.NFLoadBalancerPingClassName=com.netflix.loadbalancer.PingUrl
 ```

Un autre point à préciser est que le pool Ribbon des serveurs destinations se réalimente à partir du composant eureka-client chaque 30 secondes. Cette fréquence peut être améliorée avec la propriété :

```properties
 <sample-client>.ribbon.ServerListRefreshInterval=30000
```

Dans le prochain poste toujours sur le sujet de Ribbon et la Haute disponibilité on va aller plus loin avec notre étude en essayant de voir comment se comporte Ribbon en cas d'indisponibilité d'un serveur destination et comment on peut fiabiliser ce comportement

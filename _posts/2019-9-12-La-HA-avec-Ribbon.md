Le but de ce post est de répondre aux questions relatives à la haute disponibilité suivantes:

* Comment on peut lancer dynamiquement plusieurs instances d'un µservice ?
* Comment Ribbon et Eureka fonctionnent ensemble ?

## 1) Comment on peut lancer dynamiquement plusieurs instances d’un µservice  ?

Pour lancer dynamiquement plusieurs instances d'un µservice voici la config à adopter :

```
server.port=0
eureka.instance.prefer-ip-address=true
eureka.instance.hostname=${spring.application.name}
eureka.instance.instance-id==${spring.cloud.client.hostname}:${spring.application.name}:${spring.application.instance_id:${random.value}}
```

NB: Si vous utlisez la version Spring Cloud Dalston.SR4 cette config ne va pas marcher dans un contexte SSL à cause du bug mentionné ici https://github.com/spring-cloud/spring-cloud-netflix/issues/2303. Pour se débloquer on peut soit adopter la solution proposée dans ce lien, soit, idéalement, faire un upgrade de Spring boot et Spring cloud avec la version la plus récente stable
                              

## 2) Comment Ribbon et Eureka fonctionnent ensemble ?

Ribbon vérifie la disponibilité des serveurs destinations à partir du cache eureka-client en se basant sur une stratégie de Ping. 
Celle qu'on trouvera configurée par défaut est la NIWSDiscoveryPing
Toutefois il reste important à savoir qu'avec la stratégie de Ping NIWSDiscoveryPing, contrairement à ce qu'on aurait penser, 
Ribbon ne va jamais faire de pings réels pour s'assurer de la disponiblité de la destination,
Cette vérifcation sera plutôt déléguée au composant eureka-client cencé de maintenir une copie de le la liste de l'ensemble des microservices en cours d'excution   

Cette stratégie de Ping peut à moment être modifiée en utilisant la propriété :
```
 <sample-client>.ribbon.NFLoadBalancerPingClassName=com.netflix.loadbalancer.PingUrl
 ```

Un autre point à préciser aussi est que ce pool Ribbon des serveurs destinations est rechargé à partir d'Eureka-client chaque 30 secondes. Cette fréquence peut être elevée avec la propriété :
```
 <sample-client>.ribbon.ServerListRefreshInterval=30000
```

Dans le prochain posts de cette série de posts sur Ribbon et la Haute disponiblité on essayera de voir comment se comporte Ribbon en cas d'indisponibilité d'un serveur destination et comment on peut fiabliser le comportement de Ribbon

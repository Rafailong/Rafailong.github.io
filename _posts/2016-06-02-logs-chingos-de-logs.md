---
layout: post
title: Logs, chingos de logs!
---

Primero que nada necesitamos instalar un montón de cosas y, como esas cosas no las queremos tener en un nuestra máquina de desarrollo, vamos a usar una virtual. Entonces lo primero es

- Instalar **VirtualBox** y también instalar una virtual con linux, yo uso Debian, no sé porqué pero uso Debian (jaja)
- ya con la virtual lista, debemos tener Java instalado, así que hagamos un `sudo apt-get install openjdk-7-jdk` para instalar el Open Java en la versión 7. una vez que Java esté completamente instalado vamos a verificar que exista en nuestro PATH usando `java -version`
- lo siguiente a instalar es [**elasticsearch**](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/setup-repositories.html \"elasticsearch\") y vamos a usar los repositorios para facilitar el proceso entonces
  - primero descargamos e instalamos el public signing key con `wget -O - http://packages.elasticsearch.org/GPG-KEY-elasticsearch | apt-key add -`
  - ahora agregamos el repositorio a la lista de sources con `deb http://packages.elasticsearch.org/elasticsearch/1.2/debian stable main`
  - y finalmente instalamos el paquete con `apt-get install elasticsearch`
  - una vez que **elascticsearch** se instale, vamos a cambiar su configuración
    - primero creamos los dicrectorios donde va a guardar sus cosas con `mkdir /data` y dentro de `/data` creamos otros dos `mkdir -p /data/{data,logs}`
    - ahora le damos permisos al usuarios creado por elasticsearch que tiene el mismo nombre, usamos el comando `sudo chown -R elasticsearch:elasticsearch /data/data` y `sudo chown -R elasticsearch:elasticsearch /data/logs` despues `sudo chmod -R ug+rw /data/data` y `sudo chmod -R ug+rw /data/logs`
    - si en algun momento se presenta el problema de muchos archivos abierto vea esta [solucion](http://www.elasticsearch.org/tutorials/too-many-open-files/)
  - ahora vamos a instalar **redis** tal y como lo sugiere [esta guía](http://redis.io/topics/quickstart) usando el apartado *Installing Redis more properly*
  - ahora instalemos **logstash** como dice [aquí](https://www.digitalocean.com/community/tutorials/how-to-use-logstash-and-kibana-to-centralize-and-visualize-logs-on-ubuntu-14-04)
  - instalar apache2 como web server `sudo apt-get install apache2`, puede no ser apache, puede ser nginx o IIS depende donde quieras correr **Kibana**
  - instalar git `sudo apt-get install git`
  - con **git** instalado, vamos a clonar **Kibana** de Github y después de eso a configurar el site en nuestro web server que ya instalamos, clonamos con `https://github.com/elasticsearch/kibana.git` recuerda que debes apuntar tu servidor web a la carpeta `src` que es donde está el sitio de **Kibana**

Ya con todo instalado es momento de crear las cosas por separado para ver si corren perronamente.

- Kibana es fácil, con que se vea bien el site en el navegador
- elasticsearch y logstash los vamos a probar por separado con la siguiente configuración de logstash (test.conf)

`input { stdin { } } output { elasticseach { host => \"127.0.0.1\" protocol => http } } `

lo que quiere decir el config anterior es: lo que se le de alogstash por consola será mandado a elasticsearch directamente. Entonces corremos

`$bin/logstash agent -f test.conf`

y si mandas un mensaje, cualquiera desde la consola resultante de correr el comando anterior, podrás ver reflejados los cambios en Kibana. Así de fácil comprobamos que **Kibana, elasticseach y logstash** corren perronamente.

Lo restante sería el *broker* (**redis o RabbitMQ**), este punto es más fácil probarlo con una app pequeña y directo con el *framework* de logging que vayas a utilizar en tu(s) apps. Te recomiendo hagas eso. Puedes encontrar un proyecto que hace eso, usando **RabbitMQ** en este repo, la carpeta se llama *LoggingToRabbitMQ*

NOTA: Recuerda que para probar **logstash** debes primero correrlo con un archivo de configuración como se muestra arriba. Pero ahora el archivo de configuración debe lucir más o menos como

`input { rabbitmq { host => \"127.0.0.1\" exchange => \"logstash\" queue => logstash\" durable => true key => \"logstash\" } } output { elasticsearch { host => \"127.0.0.1\" protocol => http } }`

para que **logstash** agarre como fuente de mensajes **RabbitMQ** y los mande a **elasticsearch**

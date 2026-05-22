# Elaboración de documentación técnica y uso de aplicaciones de propósito general.
# Marco López Alonso.
# Desarrollo de aplicaciones web 1.
# 15/05/2026


# 1. Análisis de Necesidades:
## ¿Qué problema de la empresa resolvemos con Guacamole y Docker? 
Para nuestra empresa el uso de Guacamole y Docker es algo fundamental por las facilidades que estas nos ofrecen, ya que por ejemplo Guacamole utiliza un sistema de acceso remoto basado en protocolos como RDP (Remote Desktop Protocol), VNC (Virtual Network Computing) y SSH (Secure Shell). A través de un servidor intermedio, los usuarios pueden conectarse a sus máquinas sin necesidad de instalar clientes específicos, lo que facilita el acceso desde cualquier dispositivo con un navegador web compatible.
Para qué Guacamole pueda conectarse a un equipo remoto, solo necesita que en el sistema destino esté instalado y configurado el servicio correspondiente:
Para conexiones RDP: Es necesario habilitar el acceso remoto en Windows.
Para conexiones VNC: Se debe instalar un servidor VNC en el equipo remoto, como TightVNC o TigerVNC.
Para conexiones SSH: El servidor debe tener habilitado y configurado el servicio SSH.
Guacamole actúa como un intermediario que traduce estas conexiones y las hace accesibles a través de una interfaz web.


Y en el caso de Docker, esta es una tecnología de encapsulación de aplicaciones, como contenedores de software, para distribuir sin problemas de dependencias ni de incompatibilidades en diversos sistemas operativos (como Windows o Linux) y en entornos locales o cloud como Azure o AWS. Así, los distintos ficheros que conforman nuestras aplicaciones, sus dependencias… se transforman en una imagen Docker, lista para ser desplegada en infinidad de sistemas. 


## ¿Por qué elegimos esta solución y no conectar directamente por RDP a cada máquina?
La elección de una arquitectura basada en Apache Guacamole sobre Docker, en lugar de conexiones RDP directas, responde a una estrategia de seguridad proactiva y eficiencia operativa. Mientras que el RDP directo obliga a exponer múltiples puertos en el firewall, aumentando drásticamente la superficie de ataque, Guacamole actúa como una pasarela centralizada que solo requiere tráfico web estándar. Esta solución elimina la dependencia de clientes pesados, permitiendo un acceso universal y seguro mediante HTML5. Asimismo, el despliegue mediante contenedores garantiza el aislamiento de servicios y una portabilidad superior, optimizando la gestión de recursos y simplificando las tareas de auditoría técnica.


# 2. Estimación de Costes de Infraestructura
## Hoja de Costes:
Para esta primera parte del nuevo trabajo voy a realizar con Google Sheets un despliegue de soluciones de software de nivel profesional, la viabilidad económica y la optimización de recursos, ya que estos son pilares tan críticos como la calidad del código. Por lo que he diseñado esto:
<img width="1099" height="233" alt="image" src="https://github.com/user-attachments/assets/a829bb8b-3166-4a55-bd5e-662e5922e1a9" />

# 3. Estrategia de Despliegue y Comunicación

El flujo de empaquetado y traslado de la aplicación desde el entorno de desarrollo local hacia la instancia de producción cloud se realizará mediante el protocolo seguro SFTP (SSH File Transfer Protocol), operando de forma estricta sobre el puerto criptográfico SSH (puerto 22). Se descarta explícitamente el uso del protocolo FTP tradicional, dado que este último transmite tanto las credenciales de administración como el código fuente en texto plano, exponiendo la infraestructura a ataques de interceptación de tráfico "Man-in-the-Middle". 

El uso de SFTP garantiza que todo el flujo de datos, comandos y autenticación viaje cifrado mediante algoritmos de clave pública/privada (RSA/ED25519), deshabilitando el acceso por contraseña para mitigar ataques de fuerza bruta. En el flujo de trabajo del proyecto, este canal seguro se integrará dentro de una canalización automatizada de Integración y Despliegue Continuo (CI/CD). Al realizar un "push" a la rama principal del repositorio, un corredor "runner" seguro autenticará la sesión utilizando variables de entorno protegidas e inyectará los artefactos de la aplicación de manera directa y aislada en el servidor Cloud.

## Mensajería Electrónica e Integración de Alertas Automáticas

Para asegurarnos el trabajo colaborativo y la alta disponibilidad de la infraestructura, nuestro equipo técnico centralizará la comunicación operativa en un espacio de trabajo de Slack. En vez de tener que depender de revisiones manuales, por lo que se configurará un flujo de monitorización automatizado, el cual utilizará agentes ligeros en el servidor como AWS CloudWatch o un exportador de métricas enlazado a Prometheus.

Este sistema se conectará a Slack mediante un "Incoming Webhook". Por lo que, de este modo, si la infraestructura sufre una caída del servicio, picos de uso de CPU que superen el 90% de forma sostenida, o intentos fallidos de acceso SSH, el servidor enviará de forma autónoma una alerta prioritaria en tiempo real al canal común. Esta estrategia automatizada reduce drásticamente el Tiempo Medio de Recuperación MTTR y centraliza la auditoría de incidentes en un único entorno profesional.

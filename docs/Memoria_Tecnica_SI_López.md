


# Elaboración de documentación técnica y uso de aplicaciones de propósito general.
# Marco López Alonso.
# Desarrollo de aplicaciones web 1.
# 15/05/2026



























# Índice:
Análisis de Necesidades:	3
¿Qué problema de la empresa resolvemos con Guacamole y Docker?	3
¿Por qué elegimos esta solución y no conectar directamente por RDP a cada máquina?	3
































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



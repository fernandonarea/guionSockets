# EXPOSICION SOCKETS UDP

## INICIO - PARTE 1
**Explicacion del codigo ServidorUDP.c**

// Creacion del socket UDP
´sockfd = socket(AF_INET, SOCK_DGRAM, 0);´
SOCK_DGRAM es el responsable de crear el UDP

// Configuracion del servidor
servaddr.sin_family = AF_INET; -> Para usar IPv4
servaddr.sin_addr.s_addr = INADDR_ANY; -> Escucha todas las interfaces de red 
servaddr.sin_port = htons(9000); -> Usa el puerto 9000      

// Asociar el socket al puerto
// Este paso es obligatorio en UDP y TCP pero en UDP no implica establecer conexion
´bind(sockfd, (const struct sockaddr *)&servaddr, sizeof(servaddr)); ´

// Bucle infinito: servidor infinito
´while(1) { 
recvfrom(sockfd, (char *)buffer, MAX, MSG_WAITALL,  
(struct sockaddr *) &cliaddr, &len); 
// ... procesar ... 
}´

- recvfrom()
 - Recibe un datagram
 - Incluye la IP y el puerto del cliente
 - No establece conexion
 - Cada paquete es tratado como evento independiente

## Conclusion - PARTE 1
El codigo mostrado demuestra la implementacion de UDP en dos instancias EC2
demostrando que UDP no mantiene conexion ni estado, el servidor solo recibe datagrams, los proces y sigue escuchando.
Esto hace que sea muy rapido, escalable y eficiente aunque menos confiable que TCP.

# PARTE 2
## INICIO
**Diferencia entre TCP y UDP**

**UDP:**
- No necesita handshake
- No garantiza el orden de los datos
- No garantiza la llegada de todos los paquetes enviados
- Es más rapido y eficiente que TCP, pero menos confiable
- Un solo socket para todos los clientes

**TCP:**
- Garantiza la llegada y el orden de los datos
- Para cada cliente se crea un socket exclusivo
- Mas lento que UDP pero mas confiable

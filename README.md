# dhcp-starvation

# DHCP Starvation Attack

## Descripción

Este laboratorio demuestra cómo funciona un ataque de **DHCP Starvation**, una técnica utilizada para agotar el pool de direcciones IP disponibles en un servidor DHCP mediante el envío masivo de solicitudes DHCP con direcciones MAC falsas.

Cuando el servidor DHCP asigna todas las direcciones disponibles, los nuevos clientes legítimos no pueden obtener una configuración IP válida, provocando una denegación de servicio en la red.

> ⚠️ Este proyecto fue desarrollado exclusivamente con fines académicos, educativos y de investigación en ciberseguridad. :contentReference[oaicite:0]{index=0}

---

# Objetivo del Laboratorio

- Comprender el funcionamiento del protocolo DHCP.
- Analizar el proceso de asignación de direcciones IP.
- Demostrar un ataque DHCP Starvation.
- Observar el agotamiento del pool DHCP.
- Implementar medidas de mitigación y protección.

---

# Topología de Red

# Requisitos

## Software

- Python 3.x
- Scapy
- Kali Linux o Parrot OS
- Wireshark
- Cisco IOS
- GNS3 o PNETLab

## Instalación

```bash
pip install scapy
```

---

# Funcionamiento del Script

El script realiza las siguientes acciones:

1. Escucha solicitudes DHCP Discover en la red.
2. Identifica clientes que solicitan configuración IP.
3. Genera respuestas DHCP falsas.
4. Ofrece una dirección IP controlada por el atacante.
5. Se anuncia como Gateway y DNS.
6. Redirige potencialmente el tráfico hacia el atacante.

---

# Características

- Captura tráfico DHCP en tiempo real.
- Generación automática de DHCP Offer falsos.
- Suplantación de servidor DHCP.
- Configuración de Gateway falso.
- Configuración de DNS falso.
- Compatible con laboratorios virtuales.

---

# Ejecución

<img width="1156" height="678" alt="photo_2026-06-05_07-20-17" src="https://github.com/user-attachments/assets/deb8c43d-80f6-4171-a1b2-20ff978ab794" />

<img width="1052" height="642" alt="photo_2026-06-05_07-20-33" src="https://github.com/user-attachments/assets/b92af8d4-2665-4d44-81fa-aab120655026" />

# ¿Cómo funciona el ataque?

DHCP funciona mediante cuatro mensajes:

```text
DHCP Discover
DHCP Offer
DHCP Request
DHCP Acknowledgment
```

El atacante intercepta o responde rápidamente a los mensajes DHCP Discover.

Posteriormente envía un DHCP Offer falso indicando:

```text
IP: 192.23.61.50
Gateway: 192.23.61.5
DNS: 192.23.61.5
```

De esta manera la víctima puede terminar utilizando parámetros de red controlados por el atacante.

---

# Riesgos de Seguridad

Este tipo de ataque puede provocar:

- Denegación de servicio.
- Agotamiento del pool DHCP.
- Redirección de tráfico.
- Ataques Man-in-the-Middle.
- Manipulación de DNS.
- Pérdida de conectividad para usuarios legítimos.

# Contramedidas

## Configuración de Port Security

Entrar al modo de configuración:

```cisco
configure terminal
```

Seleccionar los puertos de acceso:

```cisco
interface range ethernet 0/1 - 2
```

Configurar modo acceso:

```cisco
switchport mode access
```

Habilitar Port Security:

```cisco
switchport port-security
```

Permitir máximo 3 MAC por puerto:

```cisco
switchport port-security maximum 3
```

Apagar el puerto si se supera el límite:

```cisco
switchport port-security violation shutdown
```

Guardar configuración:

```cisco
end
write
```

<img width="774" height="342" alt="photo_2026-06-05_07-21-15" src="https://github.com/user-attachments/assets/40294327-daf2-4e90-839e-cbece041b901" />



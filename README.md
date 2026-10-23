# portafolio-ccna2
#Crear el diagrama y cablear acorde a la topologia.
<img width="1440" height="900" alt="1-topologia" src="https://github.com/user-attachments/assets/f7e5d51e-4c8d-450a-b2d6-a58fd6dc2691" />
## Tabla A: Dispositivos intermedios (Routers y Switches)

| Dispositivo / Interfaz | VLAN | Segmento de red base | Dirección IP a calcular / configurar | Máscara de subred | Gateway por defecto |
|---|---:|---|---|---|---|
| R1-Core (G0/0/0.10) | 10 | 192.168.10.0/24 | 192.168.10.1/24 | 255.255.255.0 | No aplica |
| R1-Core (G0/0/0.20) | 20 | 192.168.20.0/24 | 192.168.20.1/24 | 255.255.255.0 | No aplica |
| R1-Core (G0/0/0.30) | 30 | 192.168.30.0/24 | 192.168.30.1/24 | 255.255.255.0 | No aplica |
| R1-Core (G0/0/0.99) | 99 | 192.168.99.0/24 | 192.168.99.1/24 | 255.255.255.0 | No aplica |
| SW1 (SVI VLAN 99) | 99 | 192.168.99.0/24 | 192.168.99.2/24 | 255.255.255.0 | 192.168.99.1 |
| SW2 (SVI VLAN 99) | 99 | 192.168.99.0/24 | 192.168.99.3/24 | 255.255.255.0 | 192.168.99.1 |
| SW3 (SVI VLAN 99) | 99 | 192.168.99.0/24 | 192.168.99.4/24 | 255.255.255.0 | 192.168.99.1 |
| Switches (enlaces troncales) | 111 | No aplica | No requiere IP | No aplica | No aplica |
| Switches (puertos inactivos) | 999 | No aplica | No requiere IP | No aplica | No aplica |

## Tabla B: Dispositivos finales (PCs de usuario y gestión)

| Dispositivo final | Puerto del switch | VLAN | Dirección IP (formato CIDR) | Máscara de subred | Gateway por defecto |
|---|---|---:|---|---|---|
| PC-Administración-1 | SW1 → Fa0/1 | 10 | 192.168.10.10/24 | 255.255.255.0 | 192.168.10.1 |
| PC-Administración-2 | SW1 → Fa0/2 | 10 | 192.168.10.11/24 | 255.255.255.0 | 192.168.10.1 |
| PC-Laboratorio-1 | SW2 → Fa0/1 | 20 | 192.168.20.10/24 | 255.255.255.0 | 192.168.20.1 |
| PC-Laboratorio-2 | SW2 → Fa0/2 | 20 | 192.168.20.11/24 | 255.255.255.0 | 192.168.20.1 |
| PC-Dirección-1 | SW3 → Fa0/1 | 30 | 192.168.30.10/24 | 255.255.255.0 | 192.168.30.1 |
| PC-Dirección-2 | SW3 → Fa0/2 | 30 | 192.168.30.11/24 | 255.255.255.0 | 192.168.30.1 |
| PC-Gestión-1 (opcional) | SW1 → Fa0/3 | 99 | 192.168.99.10/24 | 255.255.255.0 | 192.168.99.1 |


#Asignar nombre a los dispositivos con tus iniciales al final
cisco
```
enable
configure terminal
hostname ABLQ
copy running-config startup-config

Switch(config)#hostname SW-Core-ABLQ
SW-Core-ABLQ(config)#end
SW-Core-ABLQ#

Switch# configure
Switch(config)# hostname SW-Lab1-ABLQ
SW-Lab1-ABLQ(config)# end
SW-Lab1-ABLQ#

witch#confi
Switch(config)#hostname SW-Lab2-ABLQ
SW-Lab2-ABLQ(config)#END
SW-Lab2-ABLQ#
```
#Habilitar los enlaces troncales.
enable
configure terminal

vlan 111
 name NATIVA
exit

interface fastEthernet0/1
 switchport mode trunk
 switchport trunk native vlan 111
 switchport trunk allowed vlan 10,20,30,99,111
 no shutdown
exit

interface fastEthernet0/24
 switchport mode trunk
 switchport trunk native vlan 111
 switchport trunk allowed vlan 10,20,30,99,111
 no shutdown
exit

end
copy running-config startup-config

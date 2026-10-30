# 03 – Arquitectura y topología

## Topología original

![Topología original](../diagrams/topologia-original.png)

*Captura original del emulador: R1 ↔ SW ↔ WINDOWSSERVER. Se conserva sin modificar.*

## Diagrama lógico

```mermaid
flowchart LR
    R1["R1-0697<br/>Gi1/0 - 20.25.6.1/24"]
    SW["SW-0697<br/>Vlan97 - 20.25.6.2/24"]
    SRV["SRV-0697 (lab0697.local)<br/>AD DS - DNS - NPS<br/>20.25.6.97/24"]
    R1 ---|"R1 Gi1/0 - SW Gi0/1 (VLAN 97)"| SW
    SW ---|"SW Gi0/2 (VLAN 97)"| SRV
```

*Diagrama elaborado a partir de las descripciones de interfaz del running-config. El puerto de R1 (Gi1/0) tiene la descripción `Enlace a SW-0697`; la NIC del servidor es `Ethernet0 2` (Intel PRO/1000 MT).*

## Plan de direccionamiento

| Dispositivo | Interfaz | IP | Máscara | Notas |
|---|---|---|---|---|
| R1-0697 | GigabitEthernet1/0 | 20.25.6.1 | 255.255.255.0 | `ip radius source-interface Gi1/0` |
| SW-0697 | Vlan97 | 20.25.6.2 | 255.255.255.0 | Gateway 20.25.6.1 |
| SRV-0697 | Ethernet0 2 | 20.25.6.97 | 255.255.255.0 | Gateway 20.25.6.1, DNS 20.25.6.97 ([`ipconfig /all`](../images/servidor/srv-ipconfig-y-version.png)) |

## Puertos del switch

| Puerto | Descripción | Modo | VLAN |
|---|---|---|---|
| Gi0/1 | `Enlace a R1-0697` | access | 97 |
| Gi0/2 | `Enlace a SRV-0697` | access | 97 |

Los demás puertos no tienen configuración específica.

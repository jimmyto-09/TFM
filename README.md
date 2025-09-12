# SD-WAN sobre Kubernetes – Caso de uso A (Controlador embebido)

Arquitectura SD-WAN de laboratorio con VNFs ejecutándose como *pods* en Kubernetes y orquestadas con Terraform.  
En este **Caso A**, el controlador SDN **Ryu** está **embebido en `vnf-wan`** y se establecen **túneles VXLAN entre sedes**.  
El tráfico VoIP se enruta por la red corporativa MPLS simulada, mientras que el tráfico entre PCs cruza Internet con NAT.

## 🗺️ Arquitectura

- **Dos sedes remotas** (site1, site2) con hosts: `h1/h2` (PC) y `t1/t2` (teléfonos IP).
- **VNFs por sede**: `vnf-access`, `vnf-cpe`, `vnf-wan` (con OVS + Ryu embebido).
- **Backhaul**: túneles **VXLAN** entre sedes; **MPLS/MetroEthernet** para tráfico corporativo.
- **Internet simulado** mediante `isp1` y `isp2` con **NAT** para alcanzar destinos públicos (p. ej., 8.8.8.8).

> Consulta las figuras 12–13 del documento para el diagrama de alto nivel.

## 📂 Estructura del repositorio

```
.
├── variables.tf
├── locals.tf
├── vnf-access.tf
├── vnf-cpe.tf
├── vnf-wan.tf          # Ryu embebido 
├── apply_flow.sh # inyección automática vía REST/



# 🧱 Arquitectura de Red – MPLS Enterprise Network Lab

Este documento describe la arquitectura lógica y física del laboratorio de red empresarial desarrollado en GNS3. El diseño está orientado a entornos corporativos con alta disponibilidad y segmentación eficiente.

---

## 🧩 Topología General

La red está compuesta por **tres sedes (A, B y C)**, cada una con su propio switch, VLANs y dispositivos terminales (VPCS). Los routers están interconectados en una **topología triangular** utilizando enlaces punto a punto. El backbone está habilitado con **MPLS LDP** para transporte eficiente de datos.

```bash
       +---------+           +---------+
       | RouterA |-----------| RouterB |
       +----+----+           +----+----+
            \                    /
             \                  /
              \                /
             +----------------+
             |    RouterC     |
             +----------------+
```


---

## 🗂️ Componentes por Sede

### Sede A
- RouterA (Cisco 3725)
- SwitchA (NM-16ESW)
- VLAN 10: IT_A → `192.168.10.0/24`
- VLAN 20: Contabilidad_A → `192.168.20.0/24`
- VLAN 30: RRHH_A → `192.168.30.0/24`

### Sede B
- RouterB (Cisco 3725)
- SwitchB (NM-16ESW)
- VLAN 110: IT_B → `192.168.110.0/24`
- VLAN 120: Contabilidad_B → `192.168.120.0/24`
- VLAN 130: RRHH_B → `192.168.130.0/24`

### Sede C
- RouterC (Cisco 3725)
- SwitchC (NM-16ESW)
- VLAN 210: IT_C → `192.168.210.0/24`
- VLAN 220: Contabilidad_C → `192.168.220.0/24`
- VLAN 230: RRHH_C → `192.168.230.0/24`

---

## 🌐 Enrutamiento y MPLS

- Protocolo OSPF en área 0 (única área backbone)
- Configuración de subinterfaces dot1Q en routers
- Activación de `mpls ip` en enlaces entre routers
- Transporte de paquetes basado en etiquetas MPLS

---

## 📌 Observaciones Técnicas

- La separación lógica por VLAN permite control de broadcast y seguridad por departamento.
- MPLS acelera el reenvío de paquetes y simula una red de núcleo empresarial real.
- Diseño ideal para roles de ingeniero de redes, soporte de infraestructura y formación técnica.


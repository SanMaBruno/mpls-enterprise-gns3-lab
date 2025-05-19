# 🔎 Diagnóstico de Fallas – MPLS Enterprise Network Lab

Este documento detalla los errores reales encontrados durante la implementación del laboratorio de red, con su respectivo análisis y solución técnica. Su propósito es dejar evidencia de troubleshooting aplicado en un entorno empresarial simulado.

---

## 🧪 Falla 1: VPCS sin IP tras reinicio

- **Síntoma:** Al volver a ejecutar el laboratorio, los VPCS aparecen sin IP (`0.0.0.0`) y no responden a pings.
- **Diagnóstico:** Las configuraciones IP no fueron guardadas en el VPCS.
- **Solución:**
  Ejecutar el siguiente comando en cada VPCS al configurar la IP:
  ```bash
  ip 192.168.X.10 192.168.X.1 24
  save
    ```

 Esto asegura que la IP persista luego de reiniciar el proyecto.
## 🧪 Falla 2: Vecinos OSPF no se establecen

- **Síntoma:** El comando `show ip ospf neighbor` no muestra ningún vecino o se queda en estado `2WAY`.

- **Diagnóstico:** La interfaz entre routers puede estar administrativamente apagada o la red OSPF no fue correctamente anunciada.

- **Solución:**

  1. Asegúrate de que la interfaz esté activa:
     ```bash
     interface FastEthernetX/X
     no shutdown
     ```

  2. Verifica que el `network` OSPF incluya la red correcta:
     ```bash
     router ospf 1
     network 10.0.0.0 0.0.0.255 area 0
     ```

  3. Si la interfaz aún no se conecta, valida que ambas partes usen la misma área OSPF.

## 🧪 Falla 3: VPCS no alcanza a su gateway

- **Síntoma:** El VPCS no puede hacer ping a su gateway aunque tenga IP correctamente asignada.

- **Diagnóstico:** La subinterfaz en el router puede estar mal configurada (sin encapsulación dot1Q o con VLAN incorrecta).

- **Solución:**

  1. Revisa que la subinterfaz tenga la encapsulación adecuada:
     ```bash
     interface FastEthernet2/0.10
     encapsulation dot1Q 10
     ip address 192.168.10.1 255.255.255.0
     ```

  2. Asegúrate de que el switch tenga permitidas esas VLANs (si aplica).

  3. Verifica la IP del VPCS y su gateway:
     ```bash
     ip 192.168.10.10 192.168.10.1 24
     ping 192.168.10.1
     ```
## 🧪 Falla 4: MPLS no genera etiquetas (tabla vacía)

- **Síntoma:** Al ejecutar `show mpls forwarding-table`, la tabla aparece vacía sin etiquetas generadas.

- **Diagnóstico:** MPLS no está activado en las interfaces o LDP no se establece correctamente entre routers.

- **Solución:**

  1. Asegúrate de activar MPLS en cada interfaz punto a punto entre routers:
     ```bash
     interface FastEthernet0/0
     mpls ip
     ```

  2. Habilita el protocolo de etiquetas globalmente:
     ```bash
     mpls label protocol ldp
     ```

  3. Verifica los vecinos LDP:
     ```bash
     show mpls ldp neighbor
     ```

  4. Confirma que haya rutas OSPF propagadas entre los routers:
     ```bash
     show ip route ospf
     ```

  5. Finalmente, vuelve a revisar la tabla de etiquetas:
     ```bash
     show mpls forwarding-table
     ```

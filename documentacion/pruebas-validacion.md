# ✅ Pruebas de Validación – MPLS Enterprise Network Lab

Este documento registra las pruebas realizadas para verificar la conectividad, enrutamiento y funcionamiento correcto de la red empresarial simulada. Las pruebas fueron diseñadas para cubrir tanto el plano de datos como el plano de control.

---

## 🧪 Prueba 1: Conectividad intra-sede (LAN)

**Objetivo:** Verificar que cada host (VPCS) dentro de una sede pueda comunicarse con su gateway de VLAN.

**Comandos:**
```bash
VPCS1 > ping 192.168.10.1
VPCS2 > ping 192.168.20.1
VPCS3 > ping 192.168.30.1
```
Resultado esperado: Todos los pings devuelven respuesta satisfactoria.

✅ Validación exitosa

## 🧪 Prueba 2: Conectividad inter-sede (departamentos equivalentes)

**Objetivo:** Validar que departamentos equivalentes de distintas sedes (ej. IT) pueden comunicarse entre sí a través del backbone MPLS.

**Comandos:**
```bash
VPCS1 > ping 192.168.110.10  # IT_A → IT_B
VPCS1 > ping 192.168.210.10  # IT_A → IT_C

VPCS4 > ping 192.168.10.10   # IT_B → IT_A
VPCS7 > ping 192.168.10.10   # IT_C → IT_A
```

Resultado esperado: Todos los pings deben retornar respuesta. Los paquetes deben pasar por el backbone MPLS.

✅ Resultado: Prueba superada, conectividad confirmada entre sedes.



---

### 🧪 Prueba 3: Vecinos OSPF formados

```markdown
## 🧪 Prueba 3: Vecinos OSPF formados

**Objetivo:** Verificar que los routers forman vecinos OSPF correctamente.

**Comando:**
```bash
RouterA# show ip ospf neighbor
```

Resultado esperado: Cada router debe tener como mínimo un vecino en estado FULL.

✅ Resultado: Vecinos OSPF activos entre RouterA, RouterB y RouterC. Estado FULL verificado.




---

### 🧪 Prueba 4: Propagación de rutas OSPF

```markdown
## 🧪 Prueba 4: Propagación de rutas OSPF

**Objetivo:** Validar que las rutas de red locales en cada sede están siendo propagadas dinámicamente por OSPF.

**Comando:**
```bash
RouterA# show ip route ospf
```

Resultado esperado: La tabla de enrutamiento debe contener rutas con código O (OSPF) correspondientes a otras sedes.

✅ Resultado: Rutas OSPF recibidas correctamente. Enrutamiento dinámico funcionando.


---

### 🧪 Prueba 5: Tabla de etiquetas MPLS

```markdown
## 🧪 Prueba 5: Tabla de etiquetas MPLS

**Objetivo:** Confirmar que MPLS está funcionando y que existen etiquetas generadas para las rutas aprendidas.

**Comando:**
```bash
RouterA# show mpls forwarding-table
```
Resultado esperado: La tabla debe mostrar FECs (Forwarding Equivalence Classes) con etiquetas asignadas.

✅ Resultado: MPLS funcional con etiquetas visibles en la tabla de forwarding.



---

### 🧪 Prueba 6: Trazado de ruta (MPLS + OSPF)

```markdown
## 🧪 Prueba 6: Trazado de ruta (MPLS + OSPF)

**Objetivo:** Verificar el camino que sigue un paquete desde un host de una sede a otro de una sede remota.

**Comando:**
```bash
VPCS1 > trace 192.168.110.10
```

Resultado esperado: El traceroute debe mostrar saltos por los routers intermedios (ej. RouterA → RouterB).

✅ Resultado: Saltos intermedios detectados. Camino de paquetes a través del backbone MPLS validado.



---

### 🧠 Conclusión

```markdown
## 🧠 Conclusión

La red empresarial simulada ha pasado todas las pruebas funcionales clave:

- Conectividad LAN y entre VLANs locales
- Comunicación exitosa entre sedes mediante MPLS
- Ruteo dinámico efectivo con OSPF
- Formación de vecinos OSPF y propagación de rutas
- MPLS activado con forwarding-table operativa
- Trazabilidad del flujo de datos confirmada

✅ Se valida el correcto diseño, implementación y operación de la red empresarial bajo estándares de ingeniería de redes. El laboratorio está preparado para ser incluido en un portafolio profesional técnico de alto nivel.

```
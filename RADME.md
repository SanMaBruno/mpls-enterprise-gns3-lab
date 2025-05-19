# 🏢 MPLS Enterprise Network Lab – Proyecto de Simulación en GNS3

Este repositorio contiene un laboratorio técnico de simulación de una red empresarial de tres sedes interconectadas mediante un backbone MPLS y enrutamiento dinámico OSPF. El proyecto fue desarrollado siguiendo principios de diseño profesional (Clean Code, SOLID) y buenas prácticas de documentación técnica para ser parte de un portafolio senior.

---

## 🎯 Objetivo del Proyecto

- Simular una red empresarial multi-sede (Sede A, B y C)
- Implementar segmentación por VLAN en cada sede
- Configurar enrutamiento dinámico con OSPF
- Implementar backbone MPLS funcional con LDP
- Documentar configuraciones, fallas, validaciones y plan de contingencia
- Ejecutar pruebas de conectividad interdepartamental

---

## 🧱 Componentes Utilizados

- **GNS3** (entorno de emulación de red)
- **Cisco 3725 + NM-16ESW** (para routing y switching)
- **VPCS** (simulación de hosts de usuarios)
- **macOS Terminal / Windows PowerShell**
- **Draw.io** para el diagrama de topología
- **Markdown** para documentación técnica estructurada

---

## 📂 Estructura del Proyecto

```bash
> Ruta local base:
Mpls_Enterprise_Network_Lab/
│
├── README.md                        ← Resumen general del proyecto 
├── .gitignore                       ← Exclusiones para control de versiones
│
├── configuraciones/                ← Configuraciones de todos los dispositivos
│   ├── configuracion-completa.txt  ← Routers + Switches (todo en un solo archivo)
│   ├── vpcs-sedeA.txt              ← Configuración IP para hosts de la sede A
│   ├── vpcs-sedeB.txt              ← Configuración IP para hosts de la sede B
│   └── vpcs-sedeC.txt              ← Configuración IP para hosts de la sede C
│
├── documentacion/                  ← Documentación técnica estructurada
│   ├── README.md                   ← Descripción técnica extendida del laboratorio
│   ├── plan-contingencia.md        ← Medidas frente a fallas e interrupciones
│   ├── diagnostico-fallas.md       ← Registro de errores reales y sus soluciones
│   ├── pruebas-validacion.md       ← Validaciones funcionales realizadas
│   └── arquitectura-red.md         ← Descripción del diseño lógico y físico
│
├── topologia/                      ← Diagramas de red
│   ├── topologia.drawio            ← Diagrama editable (Draw.io)
│   └── topologia.jpeg              ← Exportación en imagen del diagrama
│
└── proyecto-gns3/                  ← Archivo fuente del proyecto GNS3
    └── Mpls_Enterprise_Network.gns3project

```


---

## 📡 Topología General

- Conexión en forma de triángulo entre RouterA, RouterB y RouterC.
- Cada router se conecta vía trunk a un switch configurado con subinterfaces dot1Q.
- Cada switch tiene 3 VLANs correspondientes a los departamentos:
  - IT
  - Contabilidad
  - RRHH

---

## 🌐 Direccionamiento IP (resumen)

- Enlaces entre routers:
  - RouterA ↔ RouterB: `10.0.0.0/24`
  - RouterB ↔ RouterC: `10.0.0.8/30`
  - RouterC ↔ RouterA: `10.0.0.4/30`

- VLANs sede A: `192.168.10.0/24`, `192.168.20.0/24`, `192.168.30.0/24`
- VLANs sede B: `192.168.110.0/24`, `192.168.120.0/24`, `192.168.130.0/24`
- VLANs sede C: `192.168.210.0/24`, `192.168.220.0/24`, `192.168.230.0/24`

---

## 🧪 Validaciones Realizadas

- `ping` entre VPCS de distintas sedes
- Verificación de vecinos OSPF: `show ip ospf neighbor`
- Verificación de etiquetas MPLS: `show mpls forwarding-table`
- Trazado de rutas (`trace`) y revisión de rutas OSPF: `show ip route ospf`

---

## 🔧 Comandos Destacados en el Proyecto

```bash
# Configuración de OSPF
router ospf 1
 network 10.0.0.0 0.0.0.255 area 0
 network 192.168.X.0 0.0.0.255 area 0

# Activación MPLS
mpls ip
mpls label protocol ldp

# Validaciones
show ip ospf neighbor
show mpls ldp neighbor
show mpls forwarding-table
```

## 🧠 Enfoque de Buenas Prácticas
## 🧩 Diseño modular, orientado a SOLID (responsabilidad única por carpeta)

## 🧾 Documentación clara, trazable y profesional en Markdown

## ⚙️ Uso de estructuras limpias, nombres explícitos y separación de responsabilidades

## 🛠 Preparado para automatizar pruebas VPCS y refactorizar configuraciones

## 🧑‍💻 Autor
Bruno San Martín Navarro
🔗 GitHub: github.com/SanMaBruno
🔗 LinkedIn: linkedin.com/in/SanMaBruno

## 📘 Licencia
Este repositorio es parte de un portafolio personal de simulación y formación profesional. Puedes usarlo con fines educativos mencionando la autoría.
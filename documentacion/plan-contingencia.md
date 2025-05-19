# 🛡️ Plan de Contingencia – MPLS Enterprise Network Lab

Este documento describe las acciones correctivas y preventivas ante posibles fallas que afecten la conectividad y funcionamiento de la red empresarial simulada. Su objetivo es asegurar continuidad operativa y facilitar la recuperación ante incidentes.

---

## 🔄 Escenarios de Falla y Respuesta Inmediata

| Escenario Crítico                                | Impacto                              | Acción Inmediata                                                    | Prevención                                                  |
|--------------------------------------------------|---------------------------------------|----------------------------------------------------------------------|-------------------------------------------------------------|
| ❌ Caída de enlace entre routers (MPLS)           | Pérdida de conectividad entre sedes   | Verificar estado de interfaces y reiniciar enrutamiento OSPF        | Diseño en triángulo con múltiples rutas OSPF               |
| ❌ VPCS sin IP después de reinicio                | Host sin conexión local ni remota     | Reconfigurar IP y gateway + `save`                                  | Usar scripts en `scripts-vpcs/` para auto configuración    |
| ❌ Subinterfaz dot1Q mal configurada              | VLAN sin acceso a red                 | Corregir `encapsulation dot1Q` y dirección IP en subinterfaz        | Validación previa con plantilla de VLANs por sede          |
| ❌ OSPF no propaga rutas                          | No hay enrutamiento dinámico          | Revisar `show ip ospf neighbor` y redes anunciadas                  | Checklist de verificación tras cambios                     |
| ❌ MPLS no aplica etiquetas                       | Enrutamiento sin MPLS                 | Verificar `mpls ip`, `mpls label protocol ldp` y tabla de etiquetas | Activar `show mpls ldp neighbor` en script de validación   |
| ❌ Error en configuración avanzada (port-security)| Fallo de IOS                          | Omitir comando y documentar limitación del módulo NM-16ESW          | Validar compatibilidad de funciones según modelo e IOS     |

---

## 🧩 Recomendaciones Generales

- 📄 **Guardar configuraciones**: Exportar regularmente `configuracion-completa.txt` tras cambios exitosos.
- 💾 **Uso de scripts**: Implementar y mantener actualizados los scripts de IP en `scripts-vpcs/`.
- 📷 **Versionado visual**: Actualizar el diagrama de topología en `topologia/topologia.drawio` con cada modificación importante.
- ✅ **Pruebas post-falla**: Realizar pruebas de validación después de corregir cualquier falla (ver `pruebas-validacion.md`).
- 📚 **Control de cambios**: Registrar cambios y observaciones técnicas en la documentación correspondiente.

---

## 🔧 Procedimiento de Recuperación Básico

1. Verificar conectividad física y estado de interfaces:
   ```bash
   show ip interface brief
   show cdp neighbors
    ```

2. Confirmar rutas OSPF propagadas:
   ```bash
    show ip route ospf
    ```
3. Validar etiquetas MPLS generadas:
   ```bash
    show mpls forwarding-table
    ``` 
4. Realizar pruebas entre hosts VPCS:

   ```bash
    ping 192.168.X.X
    trace 192.168.X.X
    ```


## ✅ Plan de Continuidad
Este entorno de laboratorio fue diseñado para facilitar reinicios y pruebas frecuentes, por lo que incluye mecanismos de rápida recuperación, documentación detallada, y scripts reutilizables.
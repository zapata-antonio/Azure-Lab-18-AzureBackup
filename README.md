# Lab 18: Continuidad de Negocio con Azure Backup (Recovery Services Vault)

## Objetivo
Configurar copias de seguridad de una máquina virtual en Azure con Azure Backup y, lo más importante, validar que se puede restaurar.  
Este lab cubre un caso real de continuidad de negocio: borrados accidentales, ransomware, fallos del sistema o cambios mal aplicados.

Idea clave: un backup “activado” no sirve si nunca se prueba un restore.

---

## Escenario
Tengo una VM en Azure que quiero proteger con copias diarias. Para ello:
- Creo un Recovery Services Vault (RSV).
- Defino una política diaria con retención.
- Habilito backup en la VM.
- Lanzo un Backup now para generar el primer punto de recuperación.
- Realizo una restauración de prueba para confirmar que la recuperación funciona.

---

## Servicios utilizados
- Recovery Services Vault (RSV)
- Azure Backup / Backup Center
- Azure Virtual Machines

---

## Tareas realizadas
1. Creación de Recovery Services Vault.
2. Configuración de política diaria y retención.
3. Habilitación de backup para una VM.
4. Ejecución de Backup now y verificación del Recovery Point.
5. Restore de prueba (validación de recuperación).

---

## Evidencias (capturas)
Ajusta los nombres si usas otro esquema, pero intenta mantenerlo consistente.

- RSV creado: `images/01-rsv-created.png`
- Política y retención: `images/02-backup-policy.png`
- Ítem protegido (Protected item) + estado: `images/03-protected-item-status.png`
- Recovery Point / Jobs completado: `images/04-recovery-point.png`
- Restore iniciado: `images/05-restore-start.png`
- Resultado restore / recurso restaurado: `images/06-restore-result.png`

---

## Checklist de verificación
- [ ] RSV creado y accesible
- [ ] Política diaria aplicada con retención definida
- [ ] VM aparece como Protected
- [ ] Existe al menos 1 Recovery Point
- [ ] Restore de prueba realizado y verificado (VM/discos/archivos)

---

## Notas prácticas (lo que suele fallar en real)
- Un backup no es continuidad de negocio si no hay pruebas de restauración.
- “Detener” una VM no significa coste 0 ni seguridad: el backup depende de política y puntos de recuperación.
- La protección se debe complementar con buenos permisos (evitar que cualquiera desactive backup o borre el vault).

En empresa añadiría: alertas, RBAC mínimo y protección del RSV (soft delete / locks).

---

## Qué le diría a un cliente / en entrevista
“Azure Backup no es solo activarlo: necesitas política, retención, monitorización y validar que el restore funciona. Yo siempre dejo al menos un recovery point probado y documentado.”

---

## Limpieza (para evitar costes)
- Eliminar la VM restaurada (si creaste una nueva).
- Revisar y eliminar recursos asociados: discos, NICs, IP públicas.

---

## Próximas mejoras
- Alertas de fallos de backup y notificaciones.
- Soft Delete y/o locks en el Recovery Services Vault.
- Backup Reports (Log Analytics) para reporting y visibil

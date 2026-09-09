# DESR Ultimate Backup v1.0

[Español](#español)

## English

**DESR Ultimate Backup** is a local preservation utility for Sony PSX DESR, built into wLaunchELF R3Z 4.76. It creates and verifies a portable system backup from the console itself, without removing the internal drive or relying on a network connection.

### Features

- Backs up `xfrom:/`, PS2-system PFS partitions on `hdd0:`, and DVR PFS partitions `dvr_hdd0:__xcontents` and `dvr_hdd0:__xdata`.
- Copies XFROM first, then HDD and DVR storage.
- Reopens and byte-compares every copied or restored file.
- Creates a new `B001`, `B002`, … folder for each run; existing backups are never overwritten.
- Creates `MANIFEST.TXT` only after successful completion. Failed or cancelled copies keep `ERROR.TXT` and are excluded from restoration.
- Version 2 machine fingerprint: direct ROMVER, MechaCon NVRAM serial and i.Link console identity are combined without storing those raw values.
- Legacy manifests are always labelled **unverified**; only a matching, version-2 physical-console fingerprint is labelled as this DESR.
- English, Spanish and Japanese interfaces.
- Restore catalogue with an Up/Down cursor selection.
- Storage-phase indicator: **XFROM → HDD → DVR**. It is intentionally not an overall percentage: computing all bytes first would require a second full scan and greatly increase run time.
- Safe backup cancellation with **SELECT**.

### Scope

This is a **DESR system-state backup**, not an HDD game-library imager. It intentionally does not copy APA game partitions installed with XMB Manager, `hdl_dump`, HDLGameInstaller, or equivalent tools. Copying installed games could require many hours and very large USB storage; games can be reinstalled separately, while the DESR system configuration cannot.

Restoration writes and verifies files present in the chosen backup. It deliberately does **not** delete files added after the backup, so it is conservative rather than an exact wipe-back-to-date restore.

### Hardware validation

| System | Firmware | Backup | Restore | Result |
| --- | --- | --- | --- | --- |
| DESR-5100S (PSX1) | 1.31 | Completed and verified | Completed and verified | Booted normally to XMB afterwards |
| DESR-7700 (PSX2) | 2.11 | Completed and verified | Completed and verified | Booted normally to XMB afterwards  |
| DESR-7500 (PSX2) | 2.10 | In hardware validation | Pending | Used to validate PSX2 restoration |

PSX1 and PSX2 have materially different HDD/DVR layouts. A successful PSX1 end-to-end restoration is encouraging, but it does not prove every model, firmware, or modified installation behaves identically.

### Restore safety

Restoration writes to XFROM and internal storage. Treat it as destructive.

- Select the exact copy with Up/Down, then press Circle.
- Triangle returns or cancels at every confirmation.
- A cross-machine restore requires two explicit experimental warnings and a final two-second `L1 + R1 + Circle` hold.
- Never use cross-machine restore except for deliberate, recoverable research.
- Never remove USB, reset, or power off the DESR during backup or restoration.

#### Current identity limitation

Backups made by early beta builds use an older fingerprint format. They are always treated as **unverified**, even if an older build labelled them as this console. New v1.0 backups record a version-2 fingerprint and the identity sources used; only an exact, strong version-2 match is labelled as this console.

### Usage

1. Place `DESR_BACKUP_TRILINGUE.ELF` and `ELISA100.FNT` together on a USB drive.
2. Start the ELF from wLaunchELF R3Z.
3. Language: Circle = English, Cross = Spanish, Square = Japanese, Triangle = exit.
4. Main menu: Circle = full backup, Cross = read-only inventory, Square = restore catalogue, Triangle = exit.
5. Press **SELECT** during backup to stop safely.

```text
DESR_BACKUP/
  DESR-XXXXXXXX/
    B001/
      MANIFEST.TXT
      xfrom/
      hdd0/
      dvr_hdd0/
```

`MANIFEST.TXT` means completion; `ERROR.TXT` identifies a partial diagnostic copy.

### Disclaimer

Provided **as is**, without warranty. You accept all risk of data loss, DVR-recording loss, partition corruption, XFROM modification, boot failure, or an unusable DESR. Create a known-good backup of the destination console before an experimental restore.

Sony, PlayStation, PSX and DESR are trademarks of their respective owners. This project is unaffiliated with Sony.

### Credits and dependencies

- **[Teo Tormo](https://www.arcadeartisan.com/)** — project direction, real-DESR testing and preservation research.
- **Jarvis (OpenAI Codex)** — assisted development of this beta.
- **R3Z3N / Saildot4K** — [wLaunchELF_R3Z](https://github.com/saildot4k/wLaunchELF_R3Z), base environment and DESR storage support.
- **israpps** — [wLaunchELF ISR](https://github.com/israpps/wLaunchELF_ISR), reference HDD/PATINFO work.
- **PS2DEV contributors** — [PS2SDK](https://github.com/ps2dev/ps2sdk), toolchain and PS2/IOP libraries.
- **gsKit contributors** — graphics infrastructure used through wLaunchELF R3Z.
- **ELISA100.FNT** — Japanese Shift-JIS font; retain its original attribution and licence when redistributing it.

Keep upstream notices and licences with binaries and source releases.

### Source code

Publishing the source is recommended: a preservation/recovery tool benefits from public audit, independent maintenance, model-specific fixes and transparency around destructive operations. Publish with upstream licences intact, third-party assets clearly separated, a beta warning and a hardware-test matrix.

---

## Español

**DESR Ultimate Backup** es una utilidad local de preservación para Sony PSX DESR, integrada en wLaunchELF R3Z 4.76. Crea y verifica una copia portátil del sistema desde la propia consola, sin desmontar el disco interno ni depender de red.

### Funciones

- Copia `xfrom:/`, las particiones PFS de sistema PS2 en `hdd0:` y las particiones PFS DVR `dvr_hdd0:__xcontents` y `dvr_hdd0:__xdata`.
- Copia primero XFROM, después HDD y DVR.
- Reabre y compara byte a byte cada archivo copiado o restaurado.
- Crea una carpeta nueva `B001`, `B002`, … en cada ejecución; nunca sobrescribe una copia existente.
- Solo crea `MANIFEST.TXT` al terminar correctamente. Las copias fallidas o canceladas conservan `ERROR.TXT` y no se ofrecen para restauración.
- Huella de máquina versión 2: combina ROMVER leído directamente, serie NVRAM del MechaCon e identidad i.Link sin guardar esos valores en bruto.
- Los manifests antiguos siempre se etiquetan como **sin verificar**; solo una huella física versión 2 coincidente se marca como de esta DESR.
- Interfaz en inglés, español y japonés.
- Catálogo de restauración con cursor Arriba/Abajo.
- Indicador de fases: **XFROM → HDD → DVR**. No es un porcentaje global: calcular todos los bytes antes obligaría a una segunda lectura completa y alargaría mucho el proceso.
- Cancelación segura de copias con **SELECT**.

### Alcance

Es una copia del **estado del sistema DESR**, no un clonador de bibliotecas de juegos. De forma deliberada no copia las particiones APA de juegos instalados con XMB Manager, `hdl_dump`, HDLGameInstaller ni herramientas equivalentes. Copiar juegos instalados requeriría muchas horas y muchísimo espacio USB; los juegos se pueden reinstalar, la configuración única de la DESR no.

La restauración escribe y verifica los archivos presentes en la copia elegida. Deliberadamente no borra archivos añadidos después de crear la copia: es conservadora, no una restauración exacta que limpie todo lo sobrante.

### Validación en hardware

| Sistema | Firmware | Copia | Restauración | Resultado |
| --- | --- | --- | --- | --- |
| DESR-5100S (PSX1) | 1.31 | Terminada y verificada | Terminada y verificada | Volvió a arrancar normalmente en XMB |
| DESR-7700 (PSX2) | 2.11 | Terminada y verificada | Terminada y verificada | Volvió a arrancar normalmente en XMB |
| DESR-7500 (PSX2) | 2.10 | En validación | Pendiente | Se usa para validar restauración PSX2 |

PSX1 y PSX2 tienen estructuras HDD/DVR materialmente distintas. Una restauración completa correcta en PSX1 es una señal excelente, pero no demuestra aún que todos los modelos, firmwares o instalaciones modificadas se comporten igual.

### Seguridad de restauración

La restauración escribe en XFROM y almacenamiento interno. Trátala como destructiva.

- Elige la copia exacta con Arriba/Abajo y pulsa Círculo.
- Triángulo vuelve o cancela en todas las confirmaciones.
- Una restauración entre máquinas exige dos avisos experimentales explícitos y, al final, mantener `L1 + R1 + Círculo` dos segundos.
- No uses restauración entre máquinas salvo para investigación deliberada y recuperable.
- No retires el USB, reinicies ni apagues la DESR durante copia o restauración.

#### Limitación actual de identificación

Las copias creadas por las primeras betas usan un formato de huella antiguo. Siempre se tratan como **sin verificar**, aunque una compilación anterior las etiquetara como de esta consola. Las nuevas copias v1.0 registran una huella versión 2 y las fuentes empleadas; solo una coincidencia exacta y sólida de versión 2 se marca como de esta DESR.

### Uso

1. Copia `DESR_BACKUP_TRILINGUE.ELF` y `ELISA100.FNT` juntos a un pendrive.
2. Ejecuta el ELF desde wLaunchELF R3Z.
3. Idioma: Círculo = inglés, X = español, Cuadrado = japonés, Triángulo = salir.
4. Menú: Círculo = copia completa, X = inventario de solo lectura, Cuadrado = catálogo de restauración, Triángulo = salir.
5. Durante una copia, pulsa **SELECT** para detener con seguridad.

```text
DESR_BACKUP/
  DESR-XXXXXXXX/
    B001/
      MANIFEST.TXT
      xfrom/
      hdd0/
      dvr_hdd0/
```

`MANIFEST.TXT` significa que la copia terminó correctamente; `ERROR.TXT` identifica una copia parcial de diagnóstico.

### Descargo de responsabilidad

Se proporciona **tal cual**, sin garantía. El uso es bajo tu responsabilidad: puede haber pérdida de datos, grabaciones DVR, corrupción de particiones, modificación de XFROM, fallo de arranque o una DESR inutilizable. Haz una copia válida de la consola destino antes de una restauración experimental.

Sony, PlayStation, PSX y DESR son marcas de sus respectivos titulares. Este proyecto no está afiliado a Sony.

### Créditos, dependencias y código fuente

- **[Teo Tormo](https://www.arcadeartisan.com/)** — dirección, pruebas en DESR reales e investigación de preservación.
- **Jarvis (OpenAI Codex)** — desarrollo asistido de esta beta.
- **R3Z3N / Saildot4K** — [wLaunchELF_R3Z](https://github.com/saildot4k/wLaunchELF_R3Z).
- **israpps** — [wLaunchELF ISR](https://github.com/israpps/wLaunchELF_ISR).
- **Colaboradores de PS2DEV** — [PS2SDK](https://github.com/ps2dev/ps2sdk), toolchain y bibliotecas PS2/IOP.
- **Colaboradores de gsKit** — infraestructura gráfica usada mediante wLaunchELF R3Z.
- **ELISA100.FNT** — fuente japonesa Shift-JIS; conserva atribución y licencia originales al redistribuirla.

Conviene publicar el código fuente: permite auditoría, mantenimiento independiente, correcciones por modelo y transparencia antes de operaciones destructivas. Conserva las licencias upstream, separa activos de terceros e incluye siempre un aviso beta y una matriz de pruebas de hardware.
# DESR-Ultimate-Backup
A simple tool for making and managing multiple backups on your PSX DESR consoles

# Guía: Compatibilidad de Hyper-V, HAXM y Emuladores de Android en Windows

> **Autor:** Jhon Alejandro Diaz J.  
> **Descripción:** Aspiring Back-end Developer | Systems Technician Student | Passionate about Python · Java · JavaScript | Learning Flask · Spring Boot · Node.js

Este documento explica los principales problemas de compatibilidad entre Hyper-V, HAXM y los emuladores de Android en Windows. Es útil para desarrolladores móviles y full-stack que usan Android Studio, IntelliJ, React Native y herramientas basadas en Node.js.

## Índice

- [Descripción](#descripción)
- [Problema con Emuladores y Virtualización](#problema-con-emuladores-y-virtualización)
- [Soluciones de Configuración](#soluciones-de-configuración)
- [Lenguajes y Frameworks afectados](#lenguajes-y-frameworks-afectados)
- [Notas y recomendaciones](#notas-y-recomendaciones)

## Descripción

Documenta cómo los sistemas de virtualización en Windows (Hyper-V y HAXM) pueden generar conflictos al utilizar emuladores de Android, y sintetiza las mejores prácticas para evitarlos o solucionarlos.

## Problema con Emuladores y Virtualización

- **Conflicto entre Hyper-V y HAXM:** No pueden coexistir activos al mismo tiempo. Ambos requieren control exclusivo de la virtualización de hardware.
- **Impacto típico:** 
  - Emulador de Android no inicia, es muy lento o muestra mensajes de error.
  - Herramientas CLI o frameworks que dependen de emuladores fallan en pruebas, builds automáticos o debugging.

## Soluciones de Configuración

- **Para usar HAXM (mejor rendimiento en emuladores x86):**
  1. Desactiva Hyper-V desde "Activar o desactivar características de Windows".
  2. Ejecuta en terminal como administrador:
     ```
     bcdedit /set hypervisorlaunchtype off
     ```
  3. Reinicia el equipo e instala HAXM desde el SDK Manager de Android Studio.

- **Para usar Hyper-V (necesario para Docker y otras VMs):**
  1. Desinstala HAXM.
  2. Activa Hyper-V y la Plataforma de hipervisor de Windows.
  3. Selecciona el emulador compatible (WHPX) desde Android Studio.

- **Nota:** Alternar entre modos puede requerir reinicios y reconfiguración según necesidades del desarrollo.

## Lenguajes y Frameworks Afectados

- **Directamente:** Java, Kotlin, Dart (Flutter), React Native, cualquier herramienta Node.js que automatice pruebas móviles.
- **Indirectamente/no afectados:** Node.js (servidor y scripts generales), React (web). Solo se afectan si automatizan pruebas Android mediante emulador.

## Notas y Recomendaciones

- Elige el modo de virtualización según tu flujo principal:  
  - Si priorizas desarrollo móvil: **Desactiva Hyper-V** y usa HAXM.
  - Si necesitas Docker/vms: **Activa Hyper-V** y usa emulador compatible.
- Para React Native y multiplataforma, considera alternativas como Genymotion si los problemas persisten.
- Mantén tu guía actualizada según evolucionen las herramientas.

---

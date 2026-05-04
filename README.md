<div align="center">

<br/>

```
 ██████╗ ██████╗ ██████╗ ██████╗ ██╗███╗   ██╗ █████╗  ██████╗██╗ ██████╗ ███╗   ██╗
██╔════╝██╔═══██╗██╔═══██╗██╔══██╗██║████╗  ██║██╔══██╗██╔════╝██║██╔═══██╗████╗  ██║
██║     ██║   ██║██║   ██║██████╔╝██║██╔██╗ ██║███████║██║     ██║██║   ██║██╔██╗ ██║
██║     ██║   ██║██║   ██║██╔══██╗██║██║╚██╗██║██╔══██║██║     ██║██║   ██║██║╚██╗██║
╚██████╗╚██████╔╝╚██████╔╝██║  ██║██║██║ ╚████║██║  ██║╚██████╗██║╚██████╔╝██║ ╚████║
 ╚═════╝ ╚═════╝  ╚═════╝ ╚═╝  ╚═╝╚═╝╚═╝  ╚═══╝╚═╝  ╚═╝ ╚═════╝╚═╝ ╚═════╝ ╚═╝  ╚═══╝
```

### _Coordinación de dos robots IRB120 en RobotStudio_

<br/>

[![RobotStudio](https://img.shields.io/badge/Software-RobotStudio-FF6F00?style=for-the-badge)](https://new.abb.com/products/robotics/robotstudio)
[![RAPID](https://img.shields.io/badge/Language-RAPID-FF6F00?style=for-the-badge)](https://library.e.abb.com/public/688894b98123f87bc1257cc50044e809/Technical%20reference%20manual_RAPID_3HAC16581-1_revJ_en.pdf)
[![Multirobots](https://img.shields.io/badge/Sistema-Multirobot-333333?style=for-the-badge)](https://en.wikipedia.org/wiki/Multi-robot_system)

<br/>

> **Proyecto Académico** · Sistemas Multirobots · Coordinación de Manipuladores · 2025

</div>

---

## 🤖 ¿Qué contiene este repositorio?

Tres simulaciones de **coordinación multirobot** con dos brazos **IRB120** en RobotStudio, replicando las condiciones reales del laboratorio. Cada comportamiento plantea un reto distinto de sincronización y comunicación entre robots.

---

## 🗂️ Estructura

```
Comportamientos-ABB/
├── Coomportamiento1.rspag   # Trayectoria rectangular coordinada
├── comportamiento2.rspag    # Manipulación conjunta de caja
└── Comportamiento3.rspag    # Construcción de torre Jenga

```

> Los archivos `.rspag` son paquetes de RobotStudio que incluyen la estación completa, los modelos 3D y el código RAPID.

---

## 🔬 Los Tres Comportamientos

### Comportamiento 1 — Trayectoria Rectangular Coordinada

Ambos robots ejecutan una trayectoria rectangular sincronizada, comenzando y terminando en el mismo punto al mismo tiempo.

**Técnica:** puntos de trayectoria configurados simétricamente para ambos robots con la misma velocidad y precisión, garantizando la coordinación temporal.

---

### Comportamiento 2 — Manipulación Conjunta de una Caja

Los dos robots cogen una caja de **200×400×200 mm** situada entre ellos, realizan movimientos conjuntos manteniéndola estable y la depositan en el mismo punto.

**Técnica:**
- Puntos de agarre programados simétricamente a ambos lados de la caja
- **Smart Component** con bloques `Attacher` / `Detacher` para simular la manipulación física
- Señales individuales por robot sincronizadas mediante una **puerta lógica AND**

---

### Comportamiento 3 — Torre Jenga

Construcción de una torre de Jenga completa con **6 piezas por robot** (25×75×15 mm), alternando orientaciones y comunicando ambos robots en tiempo real.

**Técnica:**
- Posicionamiento con **offset relativo** desde un punto base, evitando programar cada posición manualmente
- Cola de prioridad (`queue`) para gestionar el orden de colocación de piezas
- **Comunicación RAPID entre robots**: señales de entrada/salida para que un robot espere a que el otro termine antes de continuar
- Herramienta personalizada modelada en RobotStudio simulando una ventosa (cilindro base + cilindro alargado + cono invertido)

```rapid
! Robot izquierdo manda señal al derecho y espera respuesta
SetDO signal_to_right, 1;
WaitDI signal_from_right, 1;
```

---

## 🛠️ Cómo abrir las simulaciones

1. Tener instalado **ABB RobotStudio** (versión 2024 o superior recomendada)
2. `File` → `Open` → seleccionar el archivo `.rspag` deseado
3. Dar **Play** a la simulación

---

## 📚 Contexto Académico

**Asignatura:** Coordinación de Manipuladores · Sistemas Multirobots  
**Autor:** Nicolás Fernández Blánquez  
**Fecha:** Abril 2025

---

<div align="center">

**Hardware simulado:** ABB IRB120 × 2  
**Stack:** RobotStudio · RAPID · Smart Components

</div>

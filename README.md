<div align="center">

# 🤖 Celda PAROL6 — Impresión 3D continua y desatendida

**Un brazo robótico de 6 ejes que cambia la placa de la impresora y lanza el siguiente trabajo, solo**

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![TypeScript](https://img.shields.io/badge/React_+_TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![three.js](https://img.shields.io/badge/three.js-000000?style=flat-square&logo=threedotjs&logoColor=white)
![Klipper](https://img.shields.io/badge/Klipper-B12F35?style=flat-square)

[🌐 Ver portafolio](https://azixtechnologyco-rgb.github.io/#celda)

</div>

![Panel web con el brazo en 3D](capturas/01-panel.jpg)

## El problema

Una impresora 3D se detiene cada vez que termina una pieza: alguien tiene que retirar la placa,
limpiarla y lanzar el siguiente trabajo. Eso impide producir de noche o en series largas.

## La solución

Una celda automática en la que un **brazo PAROL6 de 6 ejes** atiende a una impresora Bambu Lab P1S:

1. Detecta que la impresión terminó (MQTT).
2. Retira la placa de acero con la pieza usando un **electroimán** en el efector.
3. Coloca una placa limpia.
4. Lanza el siguiente trabajo de la cola.

Además:

- **Panel web en 3D** (three.js) con la posición de cada junta, sensores, cámaras y alertas.
- **Puesta en marcha guiada** por niveles de riesgo, junta por junta, con paro de emergencia.
- Mantenimiento por horas de máquina y kilos de filamento, y **cotizador** de piezas.
- **Piezas mecánicas propias** diseñadas por código, con chequeo de colisiones contra la impresora.
- Usuarios con roles, sesiones revocables y contraseñas con PBKDF2.

## Capturas

| Puesta en marcha | Disposición de la celda |
|---|---|
| ![Puesta en marcha](capturas/02-puesta.jpg) | ![Celda](capturas/04-celda.jpg) |
| **Piezas diseñadas** | **Efector, antes y después** |
| ![Modificaciones](capturas/03-modificaciones.jpg) | ![Efector](capturas/05-efector.jpg) |

## Arquitectura

```mermaid
flowchart LR
  P[Bambu Lab P1S] -- MQTT / FTP --> C[Cerebro · Python]
  C -- HTTP --> M[Moonraker]
  M --> K[Klipper]
  K -- USB --> O[Octopus V1.1]
  O --> R[6 motores + electroimán]
  C --> W[API FastAPI]
  W --> UI[Panel · React + three.js]
```

**Stack:** Python · FastAPI · React + TypeScript · three.js · Vite · Klipper · Moonraker · MQTT · SQLite · CAD paramétrico · Linux

---

> 🔒 El código fuente es privado. Las capturas del panel muestran el **modo simulado**, sin hardware conectado.
>
> Desarrollado por **[Azix Technology](https://azixtechnologyco-rgb.github.io)** · Isaac Ávila

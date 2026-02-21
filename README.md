```md
# App Zona Azul (Visión Artificial + Lectura de Matrículas)

Sistema de **control de estacionamiento en Zona Azul** basado en **visión artificial** que detecta vehículos y **lee matrículas automáticamente** para apoyar a controladores y/o automatizar comprobaciones.

Este repositorio está orientado a un flujo típico de ANPR (Automatic Number Plate Recognition):

1. Detección del vehículo en la escena
2. Detección de la matrícula dentro del vehículo
3. Preprocesado de la matrícula
4. OCR / lectura del texto
5. Registro de resultados (CSV / BD) y lógica de alertas (repetición / tiempo)

---

## 🎯 Objetivo

- Detectar coches y matrículas en imágenes o vídeo.
- Leer la matrícula con OCR.
- Guardar resultados y generar lógica de control:
  - “Visto have X minutos”
  - “Reincidente”
  - “Caducado”
  - Exportación para informes o integración con sistemas municipales.

---

## ✅ Características

- Detección con modelos YOLO (vehículos y matrículas).
- Pipeline de recorte y preprocesado (gris + threshold, etc.).
- Exportación a CSV para auditoría / informes.
- Preparado para integraciones:
  - Base de datos (PostgreSQL/MySQL)
  - API REST
  - App Android / Web panel
  - Cámaras IP / RTSP

---

## 🧱 Estructura del proyecto (recomendada)
```

App-Zona-Azul/
├─ models/ # pesos (vehicle detector / plate detector)
├─ videos/ # vídeos de prueba
├─ images/ # imágenes de prueba
├─ outputs/ # CSVs, logs, resultados
├─ sort/ # tracker (SORT/DeepSORT si aplica)
├─ util.py # utilidades: OCR, get_car, write_csv...
├─ main.py # pipeline principal
└─ README.md

````

---

## ⚙️ Requisitos

- Python 3.9+ (recomendado 3.10)
- OpenCV
- Ultralytics (YOLO)
- Numpy
- (Opcional) Tracker: SORT / DeepSORT
- (Opcional) OCR: EasyOCR / Tesseract / PaddleOCR

Instalación rápida:

```bash
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
````

---

## ▶️ Ejecución

### 1) Ejecutar sobre vídeo

```bash
python main.py --source ./videos/video_modelo.mp4 --out ./outputs/results.csv
```

_(Adapta los arguments a tu `main.py`. Si no los tienes, puedes dejarlo fijo en el script.)_

---

## 🧠 Lógica de control Zona Azul (idea)

- Persistencia local de matrículas por día.
- Reinicio automático al cambio de fecha.
- Ventana de tiempo configurable: “alertar si se repite antes de X minutos”.
- Exportación y/o sincronización con backend.

---

## 🛣️ Roadmap

- [ ] Mejor OCR en condiciones reales (noche, reflejos, movimiento)
- [ ] Soporte RTSP (cámaras IP)
- [ ] Panel web / app para controladores
- [ ] API para consultar matrículas y eventos
- [ ] Enmascarado / privacidad (blur de caras si se require)

---

## 🔒 Privacidad y cumplimiento

Este sistema puede procesar datos sensibles (matrículas). Asegúrate de cumplir:

- RGPD (España/UE)
- Retención mínima de datos
- Accesos y auditoría
- Justificación legal del tratamiento

---

## 📩 Contacto

One-Hilo

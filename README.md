# Comunicaciones Digitales — Laboratorios en MATLAB

Repositorio de apoyo para el desarrollo de laboratorios de **Comunicaciones Digitales**, centrado en el análisis de señales muestreadas, estimación de desfase mediante correlación cruzada y visualización del espectro en frecuencia (FFT) con **MATLAB**.

![MATLAB](https://img.shields.io/badge/MATLAB-Signal%20Processing-0076A8?style=flat-square)
![Área](https://img.shields.io/badge/%C3%81rea-Comunicaciones%20Digitales-0F766E?style=flat-square)

---

## Descripción

El script incluido (`Matlab.txt`) procesa datos experimentales de muestreo y espectro FFT capturados en laboratorio (por ejemplo, desde un osciloscopio o sistema de adquisición) y realiza automáticamente las siguientes etapas:

1. **Carga de datos experimentales:** lee dos archivos de texto de dos columnas (`512_muestras.txt` en el dominio del tiempo y `512_fft.txt` en el dominio de la frecuencia).
2. **Estimación de parámetros de la señal:** calcula la frecuencia de muestreo $f_s = 1 / \overline{\Delta t}$ y detecta la frecuencia fundamental mediante la magnitud de la FFT (eliminando la componente DC).
3. **Extracción de dos ciclos y alineación de fase:** recorta dos periodos ($2T$) de la señal muestreada y calcula el desfase óptimo frente a una senoide continua de referencia ($f_{\text{ref}} = 200\ \text{Hz}$, $V_{pp} = 2\ \text{V}$, $V_{dc} = 1.5\ \text{V}$) usando correlación cruzada (`xcorr`), permitiendo además un ajuste fino manual (`ajuste_manual`).
4. **Visualización comparativa:**
   - **Figura 1:** señal muestreada discreta (`stem`) superpuesta con la señal sinusoidal continua de referencia alineada (`plot`).
   - **Figura 2:** representación espectral de la FFT a 200 Hz (potencia en dBm frente a frecuencia en Hz).

---

## Estructura del proyecto

```text
ComunicacionesDigitales/
├── Matlab.txt          # Script de análisis temporal, correlación cruzada y gráfica FFT
└── README.md           # Documentación del repositorio
```

---

## Requisitos y ejecución

### Requisitos

- **MATLAB** (con *Signal Processing Toolbox* para la función `xcorr`).
- Archivos de entrada en el mismo directorio de trabajo (no incluidos en el repositorio):
  - `512_muestras.txt`: columna 1 = tiempo (s), columna 2 = voltaje (V).
  - `512_fft.txt`: columna 1 = frecuencia (Hz), columna 2 = potencia (dBm).

### Cómo ejecutar

1. Clona o descarga el repositorio:
   ```powershell
   git clone https://github.com/JuanCan00/ComunicacionesDigitales.git
   ```
2. Copia el contenido de `Matlab.txt` en un archivo `.m` (por ejemplo, `analisis_muestreo.m`) dentro de tu carpeta de trabajo de MATLAB junto con `512_muestras.txt` y `512_fft.txt`.
3. Si tu práctica usa otros parámetros de señal de referencia, ajusta al inicio del script:
   ```matlab
   Vpp = 2;          % Voltaje pico a pico (V)
   Vdc = 1.5;        % Offset DC (V)
   f_ref = 200;      % Frecuencia de referencia (Hz)
   ajuste_manual = 0; % Ajuste manual adicional del desfase (s)
   ```
4. Ejecuta el script desde MATLAB para obtener en consola los valores de desfase y generar las dos gráficas.

---

## Autor

**Juan Pablo Cano** · [@JuanCan00](https://github.com/JuanCan00)  
Ingeniería en Telecomunicaciones — Universidad Militar Nueva Granada

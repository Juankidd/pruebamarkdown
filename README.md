# Extractor de Log TXT → DataFrame (Pandas)

Este repositorio contiene un script sencillo para **leer un archivo de log en texto plano** y convertirlo en un **DataFrame de Pandas**, separando cada línea en campos estructurados.

- Script principal: `extracciontxt.py` :contentReference[oaicite:0]{index=0}  
- Archivo de ejemplo: `log_maquina_industrial.txt` :contentReference[oaicite:1]{index=1}

---

## 1) ¿Qué problema resuelve?

En entornos industriales es común tener logs con eventos por máquina en formato texto. Este script:

1. Lee el archivo línea por línea.
2. Valida el formato esperado de cada registro.
3. Construye una lista de filas (dicts).
4. Convierte esa lista en un DataFrame.
5. (Opcional) Deja listo el DataFrame para exportarlo a CSV.

---

## 2) Formato de entrada esperado (TXT)

Cada línea del log debe tener exactamente **3 segmentos** separados por `/`:



### 2.1) Significado de cada campo

- **nombre_maquina**: identificador de la máquina / línea (ej: `L1-ENVASADORA-01`)
- **codigo_error**: código alfanumérico (ej: `E1357`, `A2786`, `I2360`)
- **status_maquina**: estado operativo (ej: `RUN`, `STOP`, `FAULT`, `IDLE`, `MAINT`, `ESTOP`)

---

## 3) Salida (DataFrame) y esquema

El script genera un DataFrame con estas columnas:

| Columna          | Tipo (actual) | Descripción |
|------------------|---------------|-------------|
| `nombre_maquina` | `object`      | Nombre/ID de la máquina |
| `codigo_error`   | `object`      | Código de error / evento |
| `status_maquina` | `category`    | Estado de la máquina (convertido a categoría) |
| `raw`            | `object`      | **Solo aparece** cuando una línea no cumple el formato |

> Nota: La columna `raw` **solo se agrega** en filas inválidas, para facilitar depuración. :contentReference[oaicite:3]{index=3}

---

## 4) Comportamiento ante datos inválidos (muy importante)

El script espera 3 partes por línea. Si una línea:

- está vacía → se ignora
- **no tiene exactamente 3 segmentos** al hacer `split("/")` → se registra como fila inválida:

```python
{"nombre_maquina": None, "codigo_error": None, "status_maquina": None, "raw": "<línea original>"}


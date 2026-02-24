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

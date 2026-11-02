# Ejercicio: Entornos virtuales (mismo Python 3.12, diferentes dependencias)

## Objetivo
Ejecutar el mismo script de Python (`app_config_demo.py`) en **dos entornos virtuales**
(misma versión de Python 3.12) pero con **versiones diferentes de la librería Pydantic**,
para observar resultados distintos:
- Con **Pydantic v2** → el script **funciona**.
- Con **Pydantic v1** → el script **falla al importar** (no existe `field_validator`).

---

## Archivos
- `app_config_demo.py` → Script principal.
- `requirements_ok.txt` → Dependencias para el **entorno que funciona** (Pydantic v2).
- `requirements_fail.txt` → Dependencias para el **entorno que falla** (Pydantic v1).

---

## Pasos (Windows / Linux / macOS)

### 1) Crear entorno que FUNCIONA
>- Con el entorno activo instalar el fichero de dependencias *'requirements_ok.txt'*:
>- Posteriormente, ejecutar el script *'app_config_demo.py'* de la siguiente forma:
```bash
python app_config_demo.py
# Deberías ver "✅ Config válida..." y un JSON normalizado
```
>- Desactiva tu entorno virtual

### 2) Crear entorno que FALLA
>- Con el entorno activo instalar el fichero de dependencias *'requirements_fail.txt'*:
>- Posteriormente, ejecutar el script *'app_config_demo.py'* de la misma forma que en el paso anterior:
```bash
python app_config_demo.py
# Esperado: ImportError al intentar importar 'field_validator' desde Pydantic v1
```

### 3) (Opcional) Probar con un JSON propio
```bash
# Ejemplo con workers inválido (0)
echo {"app_name":"Test","workers":0,"log_level":"INFO"} > config.json
python app_config_demo.py --config config.json  # En v2: valida y mostrará error por workers<1
```

---

## Entrega en Git
Sube al repositorio:
- `app_config_demo.py`
- `requirements_ok.txt`
- `requirements_fail.txt`
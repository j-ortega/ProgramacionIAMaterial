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

## Pasos (Windows PowerShell / Linux / macOS)
Asegúrate de tener **Python 3.12** en tu PATH.

### 1) Entorno que FUNCIONA
```bash
python -m venv .venv_ok
# Activar:
#  - Windows (PowerShell): .\.venv_ok\Scripts\Activate.ps1
#  - Linux/macOS: source .venv_ok/bin/activate

python -m pip install -r requirements_ok.txt
python app_config_demo.py
# Deberías ver "✅ Config válida..." y un JSON normalizado
deactivate
```

### 2) Entorno que FALLA
```bash
python -m venv .venv_fail
# Activar:
#  - Windows (PowerShell): .\.venv_fail\Scripts\Activate.ps1
#  - Linux/macOS: source .venv_fail/bin/activate

python -m pip install -r requirements_fail.txt
python app_config_demo.py
# Esperado: ImportError al intentar importar 'field_validator' desde Pydantic v1
deactivate
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

Ejemplo de comandos:
```bash
git init
git add app_config_demo.py requirements_ok.txt requirements_fail.txt
git commit -m "feat: ejercicio entornos virtuales (pydantic v1 vs v2)"
git branch -M main
git remote add origin <URL_de_tu_repo>
git push -u origin main
```
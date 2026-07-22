# Predictor de Salario — Adult Income Dataset

Proyecto MLOps que entrena y despliega un modelo de Machine Learning capaz de predecir si una persona gana **más o menos de 50K$/año** en base a sus características demográficas y laborales, utilizando el clásico [Adult Census Income Dataset](https://archive.ics.uci.edu/dataset/2/adult).

El pipeline completo abarca entrenamiento con seguimiento de experimentos en **MLflow (Azure ML)**, empaquetado en **Docker** y exposición del modelo como **API REST con FastAPI**.

### Estado
>  Finalizado

---

## 🗂 Estructura del proyecto

```
├── src/                  # Lógica de entrenamiento
│   ├── main.py           # Punto de entrada: carga datos, entrena y registra en MLflow
│   ├── data_loader.py    # Carga y preprocesamiento del dataset
│   ├── model.py          # Definición del modelo (scikit-learn)
│   └── evaluate.py       # Métricas de evaluación
├── deployment/
│   ├── Dockerfile        # Imagen Docker para la API
│   └── app/
│       └── main.py       # API REST con FastAPI (/predict, /health, /metrics)
├── scripts/              # Scripts auxiliares de CI/CD
└── requirements.txt
```

---

## ⚙️ Instalación

**Prerrequisitos:** Python 3.10+, pip, Docker (para despliegue)

```bash
# 1. Clonar el repositorio
git clone https://github.com/alchemistC137/pontia-mlops-IA0526-grupo1.git
cd pontia-mlops-IA0526-grupo1

# 2. Crear entorno virtual e instalar dependencias
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt

# 3. Colocar el dataset en la ruta esperada
mkdir -p data/raw
# Copiar adult.data y adult.test en data/raw/
curl -o data/raw/adult.data https://archive.ics.uci.edu/ml/machine-learning-databases/adult/adult.data
curl -o data/raw/adult.test https://archive.ics.uci.edu/ml/machine-learning-databases/adult/adult.test
```

---

##  Uso



### Endpoints disponibles

| Método | Ruta | Descripción |
|--------|------|-------------|
| `GET` | `/health` | Estado del servicio y del modelo |
| `POST` | `/predict` | Realiza una predicción |
| `GET` | `/metrics` | Contador de predicciones (formato Prometheus) |

### Ejemplo de predicción

```bash
curl -X POST http://localhost:8000/predict \
  -H "Content-Type: application/json" \
  -d '{
    "age": 39,
    "workclass": "State-gov",
    "fnlwgt": 77516,
    "education": "Bachelors",
    "education-num": 13,
    "marital-status": "Never-married",
    "occupation": "Adm-clerical",
    "relationship": "Not-in-family",
    "race": "White",
    "sex": "Male",
    "capital-gain": 2174,
    "capital-loss": 0,
    "hours-per-week": 40,
    "native-country": "United-States"
  }'
```

**Respuesta:** `{"prediction": [0]}` → `0 = ≤50K`, `1 = >50K`

---

## Tecnologías

| Categoría | Herramienta |
|-----------|-------------|
| Lenguaje | Python 3.10+ |
| ML | scikit-learn, pandas, numpy |
| Tracking | MLflow + Azure ML |
| API | FastAPI |
| Contenerización | Docker |
| Artefactos | Azure Blob Storage |

---

## Contribuciones

1. Haz un fork del repositorio
2. Crea una rama: `git checkout -b feature/mi-mejora`
3. Realiza tus cambios y haz commit: `git commit -m "feat: descripción"`
4. Abre un Pull Request hacia `master`

---

## 📄 Licencia

Por definir.

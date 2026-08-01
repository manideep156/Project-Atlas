# ⚙️ PySpark Local Setup

This file records the local PySpark setup used in Project Atlas.

---

## Environment

| Component | Configuration |
|---|---|
| Operating System | Windows |
| Python | 3.11.9 |
| Java | 17 or later |
| Environment | `.venv` |
| Editor | VS Code |
| Notebook | Jupyter |

---

## 1. Verify Python

```powershell
python --version
```

---

## 2. Verify Java

```powershell
java -version
javac -version
```

Current PySpark requires Java 17 or later.

---

## 3. Activate the Environment

```powershell
.\.venv\Scripts\Activate.ps1
```

---

## 4. Install PySpark

```powershell
python -m pip install pyspark
```

Verify:

```powershell
python -m pip show pyspark
```

---

## 5. Configure Jupyter

```powershell
python -m pip install ipykernel
```

Register the environment when required:

```powershell
python -m ipykernel install --user --name project-atlas --display-name "Python (Project Atlas)"
```

Select the following kernel in VS Code:

```text
Python (Project Atlas)
```

---

## 6. Verify PySpark

```python
import pyspark

print(pyspark.__version__)
```

---

## 7. Test Spark

```python
from pyspark.sql import SparkSession

spark = (
    SparkSession.builder
    .appName("Project Atlas Setup Test")
    .master("local[*]")
    .getOrCreate()
)

print(spark.version)

spark.stop()
```

---

## Setup Checklist

- [x] Python verified
- [x] Java verified
- [x] Virtual environment activated
- [x] PySpark installed
- [x] Correct notebook kernel selected
- [x] Spark session created successfully

---

# 🔧 Troubleshooting

## PowerShell: Running scripts is disabled

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

---

## Verify `JAVA_HOME`

```powershell
echo $env:JAVA_HOME
```

Expected:

```text
C:\Program Files\Eclipse Adoptium\jdk-17.0.12.7-hotspot
```

---

## Verify Java

```powershell
java -version
javac -version
```

---

## Verify Active Python Environment

```powershell
python --version
where.exe python
```

---

## Verify Notebook Interpreter

```python
import sys

print(sys.executable)
```

The notebook should use:

```text
Project-Atlas\.venv\Scripts\python.exe
```

---

## Verify PySpark Installation

```powershell
python -m pip show pyspark
```

---

## Register the Jupyter Kernel

```powershell
python -m ipykernel install --user --name atlas-pyspark --display-name "Python (Atlas PySpark)"
```

---

## Verify PySpark

```python
import pyspark

print(pyspark.__version__)
```
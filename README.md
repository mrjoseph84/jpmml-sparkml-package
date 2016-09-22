JPMML-SparkML-Package
=====================

JPMML-SparkML as an [Apache Spark Package] (https://spark-packages.org/).

# Prerequisites #

* [Apache Spark] (http://spark.apache.org/) 2.0.X.

# Installation #

Check out the JPMML-SparkML-Package project and enter its directory:
```
git clone https://github.com/jpmml/jpmml-sparkml-package.git
cd jpmml-sparkml-package
```

Build the project:
```
mvn clean package
```

The build produces an uber-JAR file `target/jpmml-sparkml-package-1.0-SNAPSHOT.jar`.

# PySpark usage #

Launching the PySpark shell with JPMML-SparkML-Package; use `--jars` to specify the location of the uber-JAR file, and `--py-files` to specify the location of the Python utility functions script:
```
pyspark --jars /path/to/jpmml-sparkml-package/target/jpmml-sparkml-package-1.0-SNAPSHOT.jar --py-files /path/to/jpmml-sparkml-package/src/main/python/jpmml.py
```

Fitting an example pipeline model:
```python
data = spark.read.csv("wine.csv", header = True, inferSchema = True)

from pyspark.ml import Pipeline
from pyspark.ml.feature import RFormula
from pyspark.ml.regression import DecisionTreeRegressor

formula = RFormula(formula = "quality ~ .")
regressor = DecisionTreeRegressor()
pipeline = Pipeline(stages = [formula, regressor])
pipelineModel = pipeline.fit(data)
```

Exporting the fitted example pipeline model to PMML byte array:
```python
from jpmml import toPMMLBytes

pmmlBytes = toPMMLBytes(sc, data, pipelineModel)
print(pmmlBytes)
```

# License #

JPMML-SparkML-Package is licensed under the [GNU Affero General Public License (AGPL) version 3.0] (http://www.gnu.org/licenses/agpl-3.0.html). Other licenses are available on request.

# Additional information #

Please contact [info@openscoring.io] (mailto:info@openscoring.io)
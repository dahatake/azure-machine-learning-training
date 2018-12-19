# Python Developer のための Azure を使った 機械学習/深層学習 のための Training リソース
Azure を利用しての 機械学習 を行うための各種ドキュメント および サンプルコード群です。

# 開発環境 / ツール

Python 開発をより円滑にするツール達です。Windows | MacOS | Linux で動きます。

## 1. Azure Notebook

無料の `JupyterNotebook` 環境である、`Azure Notebook` が大幅リニューアルです。

Azure Notebooks at Microsoft Connect() 2018:

https://github.com/Microsoft/AzureNotebooks/wiki/Azure-Notebooks-at-Microsoft-Connect()-2018

ドキュメント:

https://docs.microsoft.com/ja-jp/azure/notebooks/

### Tips

### 1. リモート実行すると、特定のファイルが無い

特に推論用の score.py などを JupyterNotebook のコードから参照しているときに FileNotFound エラーが出ます。`%%writefile <file-name>` コマンド以下に、当該ファイルの内容をコピーして、そのセルを実行してください。ファイルが作成されます。

```python
%%writefile score.py
import pickle
import json
import numpy
import azureml.train.automl
from sklearn.externals import joblib
from azureml.core.model import Model


def init():
    global model
    model_path = Model.get_model_path(model_name = '<<modelid>>') # this name is model.id of model that we want to deploy
    # deserialize the model file back into a sklearn model
    model = joblib.load(model_path)

def run(rawdata):
    try:
        data = json.loads(rawdata)['data']
        data = numpy.array(data)
        result = model.predict(data)
    except Exception as e:
        result = str(e)
        return json.dumps({"error": result})
    return json.dumps({"result":result.tolist()})
```

## 2. Visual Studio Code + Python Extension

`Visual Studio Code` での `Python` サポートです。

Python in Visual Studio Code:

https://code.visualstudio.com/docs/languages/python

Visual Studio Code の Download:

https://code.visualstudio.com/

Visual Studio Code の開発環境の構築には、こちらの Python Extension Pack が便利です:

https://marketplace.visualstudio.com/items?itemName=donjayamanne.python-extension-pack

## サンプルコード

Azure Machine Learning の Python SDK を使っています。

https://github.com/dahatake/MachineLearningNotebooks


# 学習フェーズ

## 1. Data Science Virtual Machine

Azure の `GPU` インスタンスの仮想マシンです。NVIDIA Dockerをはじめ、様々な Deep Learning を動かすためのモジュールが入っています。

ドキュメント:

https://docs.microsoft.com/ja-jp/azure/machine-learning/data-science-virtual-machine/dsvm-ubuntu-intro


残念ながら、 Azure Machine Learning services Python SDK が古い場合があります (2018/12/20 のバージョン = 1.0.2)。その場合は Update をしてください。JupyterNotebook で実行している場合は、Kernel 自身の Restart もお忘れなく。

```bash
pip freeze --local | grep -v '^\-e' | cut -d = -f 1 | xargs pip install -U pip
```

確認用の Python コード 例
```python
import azureml.core
print(azureml.core.VERSION)
```

Azure Machine Learning Service - Python SDK のインストール

https://docs.microsoft.com/en-us/python/api/overview/azure/ml/intro?view=azure-ml-py

Reference:

https://qiita.com/manji0/items/d3d824d77c18c2f28569

## 2. Azure Machine Learning services

なんといっても、`Azure Machine Learning services` が大幅にアーキテクチャを一新させ、GAしました。

Announcing general availability of Azure Machine Learning service: A look under the hood:

https://azure.microsoft.com/en-us/blog/azure-machine-learning-service-a-look-under-the-hood/

ドキュメント:

https://docs.microsoft.com/ja-jp/azure/machine-learning/service/

![アーキテクチャ](https://docs.microsoft.com/ja-jp/azure/machine-learning/service/media/concept-azure-machine-learning-architecture/workflow.png)

- Azure Machine Learning Workbench と Azure Batch AI は今後なくなります。
- 上記2つと Azure Machine Learning Experiment Services と Azure Machine Learning Model Management Services の2つはは、 Azure Machine Learning Services へ統合されます。
- Python SDK (Data Prep | SDK (メインの) | Monitoring) が提供されています。これは、Pythonが動いていれば、Edge | PC/Mac | SmartPhone | Cloud どこからでも、呼べます。

### サンプルコード の実行

最初に `configuration.ipynb` を実行して、作成した Azure Machine Learning Workspace への接続情報を設定します。
以下に似たコードがあります。

```python
import os

subscription_id = os.getenv("SUBSCRIPTION_ID", default="<my-subscription-id>")
resource_group = os.getenv("RESOURCE_GROUP", default="<my-resource-group>")
workspace_name = os.getenv("WORKSPACE_NAME", default="<my-workspace-name>")
workspace_region = os.getenv("WORKSPACE_REGION", default="eastus2")
```

# 推論 フェーズ

## 1. Python on Azure Function

REST APIとして公開するための、`Azure Functions` での Python Support ! ようやくです!

Native Python support on Azure App Service on Linux: new public preview!:

https://azure.microsoft.com/en-us/blog/native-python-support-on-azure-app-service-on-linux-new-public-preview/


ドキュメント:

https://docs.microsoft.com/en-us/azure/app-service/containers/quickstart-python

## 2. Cognitive Services

`Cognitive Services` の一部のサービスは、Docker Container ベースですが、デバイス側で Model を動作させる事が出来ます。

- Computer Vision (Recognize Text)
- Face
- Text Analytics
- Custom Vision Service
- Language Understanding Intelligent Service

Azure Cognitive Services でのコンテナーのサポート:

https://docs.microsoft.com/ja-jp/azure/cognitive-services/cognitive-services-container-support

現状は、Computer Vision (Recognize Text) と Face の利用前には、別途 Web Form での申し込みが必要です。

Getting started with Azure Cognitive Services in containers:
    
https://azure.microsoft.com/ja-jp/blog/getting-started-with-azure-cognitive-services-in-containers/

## 3. ONNX Runtime

業界標準のモデルファイルフォーマットである ONNX の推論実行環境が Open Source のプロジェクトとして公開されました。推論環境構築を最小限にして、多様なチップセット (CPU / GPU など) への対応を目指します。

https://azure.microsoft.com/ja-jp/blog/onnx-runtime-is-now-open-source/

# Azure Developer Reference

Microsoft Learn -- 概要を理解する

https://docs.microsoft.com/ja-jp/learn/

Azure ドキュメント -- 自習書、目的別手順、サンプル、API仕様

https://docs.microsoft.com/ja-jp/azure/
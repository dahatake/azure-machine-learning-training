# Python Developer のための Azure を使った 機械学習/深層学習 のための Training リソース
Azure を利用しての 機械学習 を行うための各種ドキュメント および サンプルコード群です。

## 開発環境

Python 開発をより円滑にするツール達です。Windows | MacOS | Linux で動きます。

無料の `JupyterNotebook` 環境である、`Azure Notebook` が大幅リニューアルです。

Azure Notebooks at Microsoft Connect() 2018:

https://github.com/Microsoft/AzureNotebooks/wiki/Azure-Notebooks-at-Microsoft-Connect()-2018

ドキュメント:

https://docs.microsoft.com/ja-jp/azure/notebooks/


`Visual Studio Code` での `Python` サポートです。

Python in Visual Studio Code:

https://code.visualstudio.com/docs/languages/python

Visual Studio Code の Download:

https://code.visualstudio.com/


## 学習

なんといっても、`Azure Machine Learning services` が大幅にアーキテクチャを一新させ、GAしました。

Announcing general availability of Azure Machine Learning service: A look under the hood:

https://azure.microsoft.com/en-us/blog/azure-machine-learning-service-a-look-under-the-hood/

ドキュメント:

https://docs.microsoft.com/ja-jp/azure/machine-learning/service/

![アーキテクチャ](https://docs.microsoft.com/ja-jp/azure/machine-learning/service/media/concept-azure-machine-learning-architecture/workflow.png)

- Azure Machine Learning Workbench と Azure Batch AI は今後なくなります。
- 上記2つと Azure Machine Learning Experiment Services と Azure Machine Learning Model Management Services の2つはは、 Azure Machine Learning Services へ統合されます。
- Python SDK (Data Prep | SDK (メインの) | Monitoring) が提供されています。これは、Pythonが動いていれば、Edge | PC/Mac | SmartPhone | Cloud どこからでも、呼べます。


## 推論

### AI on Serverless

REST APIとして公開するための、`Azure Functions` での Python Support ! ようやくです!

Native Python support on Azure App Service on Linux: new public preview!:

https://azure.microsoft.com/en-us/blog/native-python-support-on-azure-app-service-on-linux-new-public-preview/


ドキュメント:

https://docs.microsoft.com/en-us/azure/app-service/containers/quickstart-python

### AI on the Edge

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

### ONNX Runtime

業界標準のモデルファイルフォーマットである ONNX の推論実行環境が Open Source のプロジェクトとして公開されました。推論環境構築を最小限にして、多様なチップセット (CPU / GPU など) への対応を目指します。

https://azure.microsoft.com/ja-jp/blog/onnx-runtime-is-now-open-source/

# 本チュートリアルについて

本チュートリアルはGoogle Cloud Shell上にkind(Kubernetes in Docker)をインストールして使い始めるためのものです。  
ちょっとした検証やトレーニングにお役立てください。

**所要時間** : 約 10 分  
**前提条件** : Googleアカウント  
**続行** ボタンをクリックして次のステップに進みます。

# Google Cloud Shell とは

Google Cloud Shellはブラウザ上から Google Cloud Platform をCLIで管理するためのターミナルです。  
Debianの上に、Google Cloudを扱うためのいくつかのツールがインストールされています。  詳細は [Google Cloud のドキュメント](https://cloud.google.com/shell/?hl=ja)を参照してください。

# [kind](https://kind.sigs.k8s.io/)とは

kind(Kubernetes in Docker) は、Kubernetesをローカルマシンで動かすためのツールです。KubernetesのNodeがDockerコンテナとして起動します。  
Kubernetes自体を検証するためにKubenetesコミュニティで正式に作られたものです。単一マシンでマルチノードクラスタを簡易に構築できます。

詳細は[公式ドキュメント](https://cloud.google.com/shell/?hl=ja)を参照してください。

# kind on Google Cloud Shell

Google Cloud ShellではDockerがプリインストールされています。  
kindもインストールされていますが、2021/2/5 現在では v0.7.0 となっていて、なんとCloud Shell上では動きません。  
v0.10.0からCloud Shellでも動くようになったので、まずはこれをインストールします。

```
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.10.0/kind-linux-amd64
chmod +x ./kind
```

kindのバイナリをPATHの通っているディレクトリに移動する必要がありますが、Cloud Shellではホームディレクトリ以外に置いたファイルは再接続時に消えてしまいます。ホームディレクトリ配下に置いてPATHを通しましょう。

```
mkdir ~/bin
mv kind ~/bin/
echo "export PATH=~/bin:$PATH" > ~/.bashrc
source ~/.bashrc
```

正しくバージョンがv.0.10.0になっていればOKです。

```
kind version
```

# kubernetesクラスタの構築

実際にkubernetesクラスタを構築してみましょう。

```
kind create cluster
```

これだけです。処理が完了したら、クラスタが構築されていることを確認します。

```
kubectl get node
kubectl version
```

configファイルを使うことで、ノード数やバージョン、その他細かいフラグを変更することが可能です。詳細は[ドキュメント](https://kind.sigs.k8s.io/docs/user/configuration/)を参照してください。

クラスタは下記のコマンドで削除します。

```
kind delete cluster
```

# おわりに

<walkthrough-conclusion-trophy></walkthrough-conclusion-trophy>

すべて完了しました。やったね！  
あとは色々試してみてください。

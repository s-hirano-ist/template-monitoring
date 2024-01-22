# 監視システム

- Grafana
- Prometheus
- Node exporter
- Windows exporter

を利用した監視システムのテンプレート。

## 監視システム (Grafana × Prometheus)の起動方法

### 初期セットアップ（Node exporterのセットアップを含む）

1. `docker compose up --build -d`を実行する。

2. `http://localhost:3000`にアクセスする。

3. 初期ユーザ名: `admin`、パスワード: `admin`を入力。

4. ログインしたらパスワードを変更するように求められるので変更する。

5. Home→Administration→Data SourceからAdd new data sourceでPrometheusを追加する。

6. `Prometheus server URL`に`http://prometheus:9090`を入力し、他はデフォルトのまま、`Save & test`をクリックし、エラーを吐かないことを確認する。

7. Home→DashboardsからNewでDashboardをimportする（`import`をクリック）。

8. `Import via grafana.com`に、`1860`を入力する。`1860`は[Node exporterのテンプレート](https://grafana.com/grafana/dashboards/1860-node-exporter-full/)のIDである。

9. `Import via grafana.com`の右にある`Load`ボタンをクリックする。

10. `Dashboard`一覧にデータが追加されていることを確認する。

### 新たなnode exporterの監視対象を追加したい場合

1. `grafana-prometheus/prometheus/prometheus.yaml`の`targets`に追記。

2. `docker restart prometheus`を実行。

### Alerts

<!-- TODO: -->

## Node exporter

マシン自体をモニタリングし、OSカーネルが開示するCPU、メモリ、ストレージなどのメトリクスを提供する。

### 初期セットアップ

```bash
bash ./monitoring/client/setup.sh
```

### 動作確認

<http://localhost:9100> にアクセスできること。

## 参考文献

- [Node exporter](https://github.com/prometheus/node_exporter)
- [Grafana for Node exporter](https://grafana.com/grafana/dashboards/1860-node-exporter-full)
- [Windows exporter](https://github.com/prometheus-community/windows_exporter)
- [Grafana for Windows exporter](https://grafana.com/grafana/dashboards/14694-windows-exporter-dashboard)

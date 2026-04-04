# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-04T16:57:02Z
- **Commit:** [`0fa1ad7`](https://github.com/Hawthorne001/client_java/commit/0fa1ad7dcb71f7f02e19ee9604c07d9c48802f04)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.23K | ± 608.22 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.95K | ± 358.51 | ops/s | 1.2x slower |
| prometheusAdd | 51.38K | ± 135.67 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.01K | ± 1.88K | ops/s | 1.4x slower |
| simpleclientInc | 6.70K | ± 16.34 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.42K | ± 130.16 | ops/s | 10x slower |
| simpleclientAdd | 6.11K | ± 308.15 | ops/s | 11x slower |
| openTelemetryInc | 1.40K | ± 229.42 | ops/s | 47x slower |
| openTelemetryAdd | 1.33K | ± 82.47 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.29K | ± 35.24 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.25K | ± 1.79K | ops/s | **fastest** |
| simpleclient | 4.47K | ± 24.61 | ops/s | 1.2x slower |
| prometheusNative | 2.55K | ± 45.38 | ops/s | 2.1x slower |
| openTelemetryClassic | 731.04 | ± 57.40 | ops/s | 7.2x slower |
| openTelemetryExponential | 535.41 | ± 23.50 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.56K | ± 2.72K | ops/s | **fastest** |
| prometheusWriteToByteArray | 487.84K | ± 2.32K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 480.12K | ± 2.97K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 474.62K | ± 3.83K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49007.243   ± 1882.831  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1327.664     ± 82.468  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1403.672    ± 229.420  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1285.377     ± 35.238  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51384.236    ± 135.670  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66230.060    ± 608.219  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56948.316    ± 358.512  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6105.462    ± 308.151  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6698.798     ± 16.338  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6424.646    ± 130.160  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        731.043     ± 57.404  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        535.415     ± 23.504  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5254.175   ± 1787.664  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2545.068     ± 45.378  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4470.564     ± 24.607  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474620.492   ± 3828.297  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     480116.843   ± 2972.643  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487842.513   ± 2317.002  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489562.245   ± 2715.984  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |

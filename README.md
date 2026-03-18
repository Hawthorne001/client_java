# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-18T09:35:21Z
- **Commit:** [`b81332e`](https://github.com/Hawthorne001/client_java/commit/b81332e3a09e465f956f118a2403e64b83771ae5)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.92K | ± 666.12 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.76K | ± 833.71 | ops/s | 1.2x slower |
| prometheusAdd | 50.50K | ± 787.41 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.61K | ± 2.00K | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 171.13 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.58K | ± 210.82 | ops/s | 10x slower |
| simpleclientAdd | 6.28K | ± 230.05 | ops/s | 10x slower |
| openTelemetryAdd | 1.49K | ± 219.47 | ops/s | 44x slower |
| openTelemetryInc | 1.33K | ± 137.35 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.23K | ± 41.29 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.37K | ± 1.59K | ops/s | **fastest** |
| simpleclient | 4.55K | ± 61.74 | ops/s | 1.2x slower |
| prometheusNative | 3.08K | ± 183.50 | ops/s | 1.7x slower |
| openTelemetryClassic | 709.37 | ± 17.39 | ops/s | 7.6x slower |
| openTelemetryExponential | 551.82 | ± 30.99 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 490.28K | ± 3.27K | ops/s | **fastest** |
| prometheusWriteToByteArray | 483.90K | ± 4.92K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.16K | ± 3.14K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 469.80K | ± 6.38K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49613.751   ± 1996.943  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1488.539    ± 219.467  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1325.584    ± 137.345  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1225.028     ± 41.285  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50500.647    ± 787.407  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65916.498    ± 666.115  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56758.826    ± 833.709  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6284.102    ± 230.051  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6661.760    ± 171.128  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6576.211    ± 210.823  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        709.370     ± 17.389  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        551.823     ± 30.991  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5370.523   ± 1592.593  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3080.917    ± 183.502  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4551.365     ± 61.736  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469799.225   ± 6379.302  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481158.195   ± 3143.323  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     483901.145   ± 4923.431  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490282.499   ± 3267.905  ops/s
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

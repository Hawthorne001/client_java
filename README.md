# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-12T05:27:12Z
- **Commit:** [`e854af4`](https://github.com/Hawthorne001/client_java/commit/e854af48392c5ad5535a153bafa62253d2dced24)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.63K | ± 1.66K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.43K | ± 1.38K | ops/s | 1.1x slower |
| prometheusAdd | 51.60K | ± 148.49 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.85K | ± 8.40K | ops/s | 1.5x slower |
| simpleclientInc | 6.77K | ± 19.35 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.59K | ± 191.02 | ops/s | 9.8x slower |
| simpleclientAdd | 6.19K | ± 54.55 | ops/s | 10x slower |
| openTelemetryAdd | 1.27K | ± 67.28 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.23K | ± 46.45 | ops/s | 53x slower |
| openTelemetryInc | 1.20K | ± 31.37 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.26K | ± 990.10 | ops/s | **fastest** |
| simpleclient | 4.55K | ± 34.98 | ops/s | 1.4x slower |
| prometheusNative | 2.83K | ± 339.94 | ops/s | 2.2x slower |
| openTelemetryClassic | 654.13 | ± 25.94 | ops/s | 9.6x slower |
| openTelemetryExponential | 559.87 | ± 10.39 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 496.09K | ± 1.75K | ops/s | **fastest** |
| prometheusWriteToByteArray | 494.13K | ± 1.90K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 488.50K | ± 5.53K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 480.83K | ± 6.21K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43846.663   ± 8401.459  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1272.311     ± 67.276  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1204.272     ± 31.371  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1226.981     ± 46.452  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51600.237    ± 148.492  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64628.282   ± 1656.649  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56425.291   ± 1375.420  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6188.751     ± 54.553  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6772.674     ± 19.353  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6587.582    ± 191.018  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        654.126     ± 25.941  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        559.865     ± 10.386  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6263.329    ± 990.095  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2826.502    ± 339.943  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4549.908     ± 34.985  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     480827.305   ± 6207.137  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488499.659   ± 5533.496  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     494134.913   ± 1901.847  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     496092.156   ± 1746.503  ops/s
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

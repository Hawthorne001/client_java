# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-03T09:18:16Z
- **Commit:** [`922943c`](https://github.com/Hawthorne001/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| codahaleIncNoLabels | 28.61K | ± 586.49 | ops/s | **fastest** |
| prometheusNoLabelsInc | 27.82K | ± 417.92 | ops/s | 1.0x slower |
| prometheusInc | 27.25K | ± 234.81 | ops/s | 1.0x slower |
| prometheusAdd | 26.48K | ± 429.28 | ops/s | 1.1x slower |
| openTelemetryIncNoLabels | 17.66K | ± 145.88 | ops/s | 1.6x slower |
| openTelemetryInc | 15.75K | ± 143.30 | ops/s | 1.8x slower |
| openTelemetryAdd | 13.86K | ± 96.58 | ops/s | 2.1x slower |
| simpleclientNoLabelsInc | 6.94K | ± 39.86 | ops/s | 4.1x slower |
| simpleclientInc | 6.90K | ± 36.63 | ops/s | 4.1x slower |
| simpleclientAdd | 6.88K | ± 83.47 | ops/s | 4.2x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 7.14K | ± 22.16 | ops/s | **fastest** |
| simpleclient | 4.45K | ± 50.30 | ops/s | 1.6x slower |
| prometheusClassic | 3.09K | ± 668.89 | ops/s | 2.3x slower |
| prometheusClassicSingleThread | 3.08K | ± 99.02 | ops/s | 2.3x slower |
| prometheusNative | 2.15K | ± 492.90 | ops/s | 3.3x slower |
| openTelemetryClassic | 504.24 | ± 34.57 | ops/s | 14x slower |
| openTelemetryExponential | 461.79 | ± 41.66 | ops/s | 15x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 18.41K | ± 114.76 | ops/s | **fastest** |
| openMetricsWriteToNull | 18.29K | ± 209.31 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 286.16K | ± 889.91 | ops/s | **fastest** |
| prometheusWriteToByteArray | 283.97K | ± 948.71 | ops/s | 1.0x slower |
| openMetricsWriteToNull | 268.96K | ± 1.74K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 266.72K | ± 1.27K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28611.020    ± 586.488  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      13860.948     ± 96.584  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      15746.963    ± 143.303  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      17655.394    ± 145.880  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      26477.439    ± 429.283  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      27253.516    ± 234.813  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      27824.362    ± 417.918  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6875.079     ± 83.466  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6898.181     ± 36.632  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6935.513     ± 39.855  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        504.238     ± 34.572  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        461.787     ± 41.665  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3089.250    ± 668.887  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15       7135.126     ± 22.158  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       3080.565     ± 99.023  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2152.995    ± 492.895  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4447.654     ± 50.296  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      18286.526    ± 209.310  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      18414.907    ± 114.756  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     266721.298   ± 1266.041  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     268960.873   ± 1743.737  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     283973.495    ± 948.708  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     286157.470    ± 889.906  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval
- **Within run** compares benchmarks in the same result set, not against the base commit.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |

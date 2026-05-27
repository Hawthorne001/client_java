# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-27T01:01:15Z
- **Commit:** [`5ee188f`](https://github.com/Hawthorne001/client_java/commit/5ee188ff288806f76e53a89d32431a93bb53da11)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.58K | ± 654.05 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.49K | ± 81.73 | ops/s | 1.2x slower |
| prometheusAdd | 51.32K | ± 216.28 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.72K | ± 415.46 | ops/s | 1.3x slower |
| simpleclientInc | 6.58K | ± 14.82 | ops/s | 10x slower |
| simpleclientAdd | 6.35K | ± 193.61 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.34K | ± 42.88 | ops/s | 10x slower |
| openTelemetryInc | 3.38K | ± 478.34 | ops/s | 20x slower |
| openTelemetryAdd | 3.19K | ± 412.73 | ops/s | 21x slower |
| openTelemetryIncNoLabels | 3.06K | ± 226.92 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.72K | ± 299.59 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 54.57 | ops/s | 1.5x slower |
| prometheusNative | 2.81K | ± 308.71 | ops/s | 2.4x slower |
| openTelemetryClassic | 788.51 | ± 30.10 | ops/s | 8.5x slower |
| openTelemetryExponential | 567.47 | ± 17.30 | ops/s | 12x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.04K | ± 1.67K | ops/s | **fastest** |
| openMetricsWriteToNull | 23.20K | ± 941.52 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 498.66K | ± 4.79K | ops/s | **fastest** |
| prometheusWriteToByteArray | 489.47K | ± 4.42K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.69K | ± 3.56K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 474.39K | ± 2.82K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49723.195    ± 415.461  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3186.878    ± 412.726  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3381.200    ± 478.344  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3064.737    ± 226.923  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51318.577    ± 216.285  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66581.639    ± 654.054  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56486.410     ± 81.725  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6351.766    ± 193.612  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6582.612     ± 14.819  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6343.431     ± 42.884  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        788.514     ± 30.100  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        567.469     ± 17.295  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6724.003    ± 299.586  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2806.472    ± 308.709  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4420.733     ± 54.573  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23195.295    ± 941.523  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24036.296   ± 1671.001  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474391.965   ± 2824.238  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476694.404   ± 3556.025  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     489469.214   ± 4415.981  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     498663.365   ± 4788.956  ops/s
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

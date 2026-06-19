# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-18T09:01:06Z
- **Commit:** [`e550766`](https://github.com/Hawthorne001/client_java/commit/e550766096ab9986f47767a1609e73220e10967a)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.98K | ± 354.79 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.79K | ± 221.74 | ops/s | 1.2x slower |
| prometheusAdd | 51.54K | ± 202.61 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.34K | ± 772.56 | ops/s | 1.3x slower |
| simpleclientInc | 6.51K | ± 51.91 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.44K | ± 245.78 | ops/s | 10x slower |
| simpleclientAdd | 6.31K | ± 260.58 | ops/s | 10x slower |
| openTelemetryInc | 3.61K | ± 361.18 | ops/s | 18x slower |
| openTelemetryIncNoLabels | 3.51K | ± 381.85 | ops/s | 19x slower |
| openTelemetryAdd | 2.98K | ± 212.99 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.65K | ± 1.12K | ops/s | **fastest** |
| simpleclient | 4.35K | ± 40.44 | ops/s | 1.3x slower |
| prometheusNative | 2.66K | ± 109.24 | ops/s | 2.1x slower |
| openTelemetryClassic | 712.36 | ± 12.05 | ops/s | 7.9x slower |
| openTelemetryExponential | 662.68 | ± 35.87 | ops/s | 8.5x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 24.00K | ± 243.46 | ops/s | **fastest** |
| prometheusWriteToNull | 23.51K | ± 465.98 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 503.88K | ± 5.49K | ops/s | **fastest** |
| prometheusWriteToByteArray | 500.33K | ± 4.58K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 487.74K | ± 3.99K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 478.90K | ± 4.36K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49338.683    ± 772.555  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2980.317    ± 212.988  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3609.595    ± 361.176  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3508.136    ± 381.854  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51535.771    ± 202.608  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65976.711    ± 354.787  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56789.133    ± 221.737  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6308.671    ± 260.575  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6508.124     ± 51.909  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6441.875    ± 245.776  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        712.362     ± 12.052  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        662.681     ± 35.875  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5654.537   ± 1119.397  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2659.045    ± 109.235  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4346.575     ± 40.437  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24000.284    ± 243.459  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23505.256    ± 465.983  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     478899.149   ± 4362.429  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     487744.594   ± 3990.912  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     500328.244   ± 4583.352  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     503880.854   ± 5491.995  ops/s
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

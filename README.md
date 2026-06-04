# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-03T04:19:21Z
- **Commit:** [`9c3b097`](https://github.com/Hawthorne001/client_java/commit/9c3b097f6842ffc08fb3a2ed00217c73a6c2b191)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.67K | ± 2.04K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.90K | ± 1.36K | ops/s | 1.2x slower |
| prometheusAdd | 51.18K | ± 381.60 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.19K | ± 3.03K | ops/s | 1.3x slower |
| simpleclientInc | 6.46K | ± 144.11 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.36K | ± 19.21 | ops/s | 10x slower |
| simpleclientAdd | 6.30K | ± 209.22 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.74K | ± 316.05 | ops/s | 17x slower |
| openTelemetryInc | 3.27K | ± 351.89 | ops/s | 20x slower |
| openTelemetryAdd | 3.10K | ± 285.20 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.32K | ± 69.16 | ops/s | **fastest** |
| prometheusClassic | 4.30K | ± 568.00 | ops/s | 1.0x slower |
| prometheusNative | 2.62K | ± 197.58 | ops/s | 1.7x slower |
| openTelemetryClassic | 752.39 | ± 25.69 | ops/s | 5.7x slower |
| openTelemetryExponential | 610.42 | ± 73.19 | ops/s | 7.1x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.92K | ± 604.57 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.37K | ± 1.47K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 516.50K | ± 5.18K | ops/s | **fastest** |
| prometheusWriteToByteArray | 502.38K | ± 10.69K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 487.46K | ± 1.82K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 487.41K | ± 2.55K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49194.685   ± 3031.833  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3096.317    ± 285.204  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3266.643    ± 351.887  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3738.166    ± 316.051  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51181.790    ± 381.598  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64668.382   ± 2040.055  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55904.002   ± 1361.229  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6298.279    ± 209.221  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6459.889    ± 144.114  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6356.821     ± 19.212  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        752.389     ± 25.688  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        610.424     ± 73.194  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4297.404    ± 567.996  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2615.884    ± 197.585  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4321.042     ± 69.160  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23368.789   ± 1467.268  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23915.731    ± 604.574  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     487463.419   ± 1823.358  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     487406.137   ± 2552.297  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     502379.841  ± 10692.415  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     516495.634   ± 5176.436  ops/s
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

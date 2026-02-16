# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-16T15:03:37Z
- **Commit:** [`bcec4c7`](https://github.com/Hawthorne001/client_java/commit/bcec4c72721c03f05b5999e208f51ad6af4c6df7)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.32K | ± 1.25K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.71K | ± 710.99 | ops/s | 1.2x slower |
| prometheusAdd | 51.61K | ± 170.25 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.37K | ± 719.65 | ops/s | 1.3x slower |
| simpleclientInc | 6.72K | ± 125.16 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.58K | ± 163.82 | ops/s | 9.9x slower |
| simpleclientAdd | 6.51K | ± 95.19 | ops/s | 10x slower |
| openTelemetryAdd | 1.47K | ± 221.71 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.43K | ± 191.39 | ops/s | 46x slower |
| openTelemetryInc | 1.24K | ± 14.13 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.36K | ± 1.40K | ops/s | **fastest** |
| simpleclient | 4.49K | ± 25.10 | ops/s | 1.2x slower |
| prometheusNative | 2.69K | ± 140.07 | ops/s | 2.0x slower |
| openTelemetryClassic | 672.09 | ± 10.36 | ops/s | 8.0x slower |
| openTelemetryExponential | 552.16 | ± 10.96 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.92K | ± 2.86K | ops/s | **fastest** |
| prometheusWriteToByteArray | 485.97K | ± 3.77K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 479.52K | ± 7.79K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.38K | ± 9.15K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49367.485    ± 719.648  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1468.676    ± 221.712  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1243.188     ± 14.132  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1432.391    ± 191.390  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51613.589    ± 170.252  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65322.424   ± 1248.099  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56711.843    ± 710.992  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6509.041     ± 95.192  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6718.856    ± 125.162  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6583.368    ± 163.823  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        672.091     ± 10.356  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        552.160     ± 10.962  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5355.245   ± 1400.099  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2685.575    ± 140.069  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4492.157     ± 25.098  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473381.011   ± 9145.594  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     479522.128   ± 7788.928  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485972.809   ± 3771.613  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489915.316   ± 2860.540  ops/s
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

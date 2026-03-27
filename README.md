# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-27T13:50:36Z
- **Commit:** [`6beb7fd`](https://github.com/Hawthorne001/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 31.05K | ± 214.50 | ops/s | **fastest** |
| prometheusInc | 30.43K | ± 1.75K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.34K | ± 1.57K | ops/s | 1.1x slower |
| prometheusAdd | 28.51K | ± 104.97 | ops/s | 1.1x slower |
| simpleclientInc | 6.70K | ± 212.41 | ops/s | 4.6x slower |
| simpleclientAdd | 6.61K | ± 45.85 | ops/s | 4.7x slower |
| simpleclientNoLabelsInc | 6.57K | ± 177.02 | ops/s | 4.7x slower |
| openTelemetryIncNoLabels | 1.36K | ± 9.93 | ops/s | 23x slower |
| openTelemetryInc | 1.34K | ± 55.02 | ops/s | 23x slower |
| openTelemetryAdd | 1.27K | ± 24.21 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.48K | ± 30.49 | ops/s | **fastest** |
| prometheusClassic | 4.26K | ± 2.34K | ops/s | 1.1x slower |
| prometheusNative | 2.14K | ± 117.73 | ops/s | 2.1x slower |
| openTelemetryClassic | 527.39 | ± 23.41 | ops/s | 8.5x slower |
| openTelemetryExponential | 403.89 | ± 13.71 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 312.00K | ± 2.52K | ops/s | **fastest** |
| prometheusWriteToByteArray | 308.89K | ± 3.56K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 292.34K | ± 2.35K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 290.01K | ± 2.73K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29344.060   ± 1569.196  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1271.926     ± 24.207  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1343.803     ± 55.023  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1356.164      ± 9.930  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28513.353    ± 104.974  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30426.116   ± 1745.799  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31053.132    ± 214.497  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6608.507     ± 45.845  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6695.040    ± 212.407  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6573.375    ± 177.017  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        527.392     ± 23.407  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        403.894     ± 13.708  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4261.718   ± 2339.198  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2140.438    ± 117.731  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4478.463     ± 30.493  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     290014.208   ± 2731.230  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     292335.840   ± 2353.968  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     308889.650   ± 3560.776  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     312004.599   ± 2520.153  ops/s
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

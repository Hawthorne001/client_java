# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-20T16:42:28Z
- **Commit:** [`9776bc9`](https://github.com/Hawthorne001/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 67.25K | ± 465.76 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.11K | ± 419.04 | ops/s | 1.2x slower |
| prometheusAdd | 51.78K | ± 117.74 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.25K | ± 1.62K | ops/s | 1.4x slower |
| simpleclientInc | 6.69K | ± 120.29 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.57K | ± 228.09 | ops/s | 10x slower |
| simpleclientAdd | 6.24K | ± 272.50 | ops/s | 11x slower |
| openTelemetryAdd | 1.75K | ± 181.17 | ops/s | 38x slower |
| openTelemetryIncNoLabels | 1.30K | ± 14.38 | ops/s | 52x slower |
| openTelemetryInc | 1.24K | ± 83.75 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.99K | ± 834.68 | ops/s | **fastest** |
| simpleclient | 4.50K | ± 22.72 | ops/s | 1.1x slower |
| prometheusNative | 3.03K | ± 226.88 | ops/s | 1.6x slower |
| openTelemetryClassic | 676.97 | ± 24.00 | ops/s | 7.4x slower |
| openTelemetryExponential | 522.81 | ± 18.81 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.67K | ± 1.42K | ops/s | **fastest** |
| openMetricsWriteToNull | 490.96K | ± 4.01K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 489.50K | ± 3.35K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.55K | ± 7.00K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48252.681   ± 1620.715  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1752.133    ± 181.174  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1240.975     ± 83.749  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1301.508     ± 14.385  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51780.859    ± 117.742  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      67247.751    ± 465.762  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57113.192    ± 419.044  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6239.083    ± 272.501  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6690.606    ± 120.290  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6568.977    ± 228.090  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        676.967     ± 23.995  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        522.809     ± 18.813  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4985.169    ± 834.676  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3031.679    ± 226.876  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4495.591     ± 22.722  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473547.253   ± 7000.332  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     490958.579   ± 4011.716  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     489501.916   ± 3345.375  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493671.234   ± 1417.245  ops/s
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

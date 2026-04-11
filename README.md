# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-11T20:53:05Z
- **Commit:** [`0fa1ad7`](https://github.com/Hawthorne001/client_java/commit/0fa1ad7dcb71f7f02e19ee9604c07d9c48802f04)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.79K | ± 1.84K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.24K | ± 117.21 | ops/s | 1.1x slower |
| codahaleIncNoLabels | 50.96K | ± 648.49 | ops/s | 1.3x slower |
| prometheusAdd | 50.81K | ± 527.33 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.60K | ± 19.84 | ops/s | 10.0x slower |
| simpleclientInc | 6.57K | ± 213.62 | ops/s | 10x slower |
| simpleclientAdd | 6.09K | ± 27.19 | ops/s | 11x slower |
| openTelemetryAdd | 1.30K | ± 24.37 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.25K | ± 11.03 | ops/s | 52x slower |
| openTelemetryInc | 1.25K | ± 58.38 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.52K | ± 1.33K | ops/s | **fastest** |
| simpleclient | 4.47K | ± 88.29 | ops/s | 1.2x slower |
| prometheusNative | 3.00K | ± 286.25 | ops/s | 1.8x slower |
| openTelemetryClassic | 681.76 | ± 43.06 | ops/s | 8.1x slower |
| openTelemetryExponential | 562.57 | ± 40.64 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.58K | ± 5.30K | ops/s | **fastest** |
| openMetricsWriteToNull | 484.27K | ± 3.06K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 484.04K | ± 4.99K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 476.75K | ± 6.06K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50958.428    ± 648.489  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1300.028     ± 24.371  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1251.408     ± 58.375  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1253.607     ± 11.032  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50814.428    ± 527.335  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65787.525   ± 1837.929  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57244.579    ± 117.206  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6087.218     ± 27.194  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6566.533    ± 213.621  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6596.444     ± 19.837  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        681.757     ± 43.064  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        562.574     ± 40.636  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5522.619   ± 1328.086  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2995.194    ± 286.245  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4474.573     ± 88.291  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     476754.753   ± 6055.938  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     484270.572   ± 3059.906  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     484038.589   ± 4989.614  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488576.049   ± 5295.864  ops/s
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

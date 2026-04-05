# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-05T16:26:21Z
- **Commit:** [`0fa1ad7`](https://github.com/Hawthorne001/client_java/commit/0fa1ad7dcb71f7f02e19ee9604c07d9c48802f04)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.23K | ± 361.95 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.66K | ± 366.04 | ops/s | 1.2x slower |
| prometheusAdd | 51.15K | ± 962.69 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.96K | ± 1.72K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.47K | ± 91.44 | ops/s | 10x slower |
| simpleclientInc | 6.29K | ± 409.00 | ops/s | 11x slower |
| simpleclientAdd | 6.04K | ± 53.39 | ops/s | 11x slower |
| openTelemetryAdd | 1.51K | ± 243.41 | ops/s | 44x slower |
| openTelemetryInc | 1.23K | ± 82.89 | ops/s | 54x slower |
| openTelemetryIncNoLabels | 1.21K | ± 23.94 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.52K | ± 550.09 | ops/s | **fastest** |
| simpleclient | 4.41K | ± 17.25 | ops/s | 1.5x slower |
| prometheusNative | 2.94K | ± 218.05 | ops/s | 2.2x slower |
| openTelemetryClassic | 692.73 | ± 19.74 | ops/s | 9.4x slower |
| openTelemetryExponential | 589.86 | ± 22.17 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 490.16K | ± 4.32K | ops/s | **fastest** |
| prometheusWriteToByteArray | 481.68K | ± 4.10K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.60K | ± 1.45K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 475.28K | ± 3.68K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47956.864   ± 1723.245  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1506.358    ± 243.410  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1234.265     ± 82.895  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1214.335     ± 23.945  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51147.965    ± 962.691  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66227.730    ± 361.952  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56662.970    ± 366.035  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6044.822     ± 53.391  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6292.350    ± 409.001  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6468.434     ± 91.445  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        692.730     ± 19.739  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        589.859     ± 22.172  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6518.665    ± 550.087  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2940.006    ± 218.046  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4405.944     ± 17.245  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475278.396   ± 3677.953  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476601.890   ± 1448.380  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481676.387   ± 4101.034  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490157.184   ± 4320.780  ops/s
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

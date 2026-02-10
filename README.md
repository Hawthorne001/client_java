# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-10T12:35:04Z
- **Commit:** [`db7bc71`](https://github.com/Hawthorne001/client_java/commit/db7bc714db240b9e973a8cbd6c31fa0dcd1b9aab)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.05K | ± 1.36K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.38K | ± 478.24 | ops/s | 1.2x slower |
| prometheusAdd | 48.68K | ± 811.77 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 40.78K | ± 5.86K | ops/s | 1.5x slower |
| simpleclientInc | 6.43K | ± 136.73 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 6.21K | ± 291.00 | ops/s | 9.7x slower |
| simpleclientAdd | 5.99K | ± 168.45 | ops/s | 10x slower |
| openTelemetryInc | 1.55K | ± 25.22 | ops/s | 39x slower |
| openTelemetryAdd | 1.29K | ± 28.25 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.28K | ± 55.55 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.37K | ± 54.15 | ops/s | **fastest** |
| simpleclient | 4.51K | ± 73.91 | ops/s | 1.6x slower |
| prometheusNative | 3.10K | ± 163.90 | ops/s | 2.4x slower |
| openTelemetryClassic | 611.52 | ± 13.38 | ops/s | 12x slower |
| openTelemetryExponential | 497.99 | ± 8.54 | ops/s | 15x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 562.72K | ± 2.89K | ops/s | **fastest** |
| prometheusWriteToByteArray | 548.50K | ± 6.77K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 539.21K | ± 5.89K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 529.14K | ± 5.74K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      40781.994   ± 5856.866  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1293.826     ± 28.250  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1547.270     ± 25.216  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1282.052     ± 55.553  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48681.456    ± 811.775  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60052.602   ± 1359.731  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51384.773    ± 478.240  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5994.812    ± 168.452  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6428.614    ± 136.730  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6214.603    ± 291.000  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        611.521     ± 13.379  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        497.992      ± 8.537  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7373.187     ± 54.155  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3096.771    ± 163.900  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4511.710     ± 73.914  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     529143.212   ± 5742.039  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     539214.784   ± 5885.684  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     548500.545   ± 6766.443  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     562720.171   ± 2893.463  ops/s
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

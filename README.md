# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-05T16:41:22Z
- **Commit:** [`058e544`](https://github.com/Hawthorne001/client_java/commit/058e54406ef2edfbe1885b414c8cd2999279cf47)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 64.75K | ± 1.32K | ops/s |
| prometheusNoLabelsInc | 56.36K | ± 1.12K | ops/s |
| prometheusAdd | 51.64K | ± 476.81 | ops/s |
| codahaleIncNoLabels | 48.26K | ± 1.05K | ops/s |
| openTelemetryIncNoLabels | 18.52K | ± 29.19 | ops/s |
| openTelemetryInc | 14.76K | ± 321.50 | ops/s |
| openTelemetryAdd | 12.87K | ± 144.95 | ops/s |
| simpleclientInc | 6.59K | ± 12.11 | ops/s |
| simpleclientAdd | 6.45K | ± 11.94 | ops/s |
| simpleclientNoLabelsInc | 6.34K | ± 15.67 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.29K | ± 25.17 | ops/s |
| prometheusClassic | 5.30K | ± 1.43K | ops/s |
| prometheusClassicSingleThread | 4.58K | ± 41.63 | ops/s |
| simpleclient | 4.36K | ± 28.51 | ops/s |
| prometheusNative | 2.80K | ± 254.99 | ops/s |
| openTelemetryClassic | 824.91 | ± 61.76 | ops/s |
| openTelemetryExponential | 648.91 | ± 50.79 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 23.47K | ± 752.03 | ops/s |
| prometheusWriteToNull | 23.19K | ± 610.50 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 502.21K | ± 3.07K | ops/s |
| prometheusWriteToByteArray | 497.94K | ± 3.39K | ops/s |
| openMetricsWriteToNull | 483.92K | ± 4.21K | ops/s |
| openMetricsWriteToByteArray | 478.76K | ± 4.27K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48262.252   ± 1050.823  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12872.614    ± 144.949  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14764.333    ± 321.499  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18516.049     ± 29.191  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51641.494    ± 476.813  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64747.781   ± 1321.524  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56358.342   ± 1115.370  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6453.133     ± 11.944  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6588.357     ± 12.110  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6337.759     ± 15.670  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        824.912     ± 61.762  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        648.914     ± 50.793  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5297.257   ± 1426.381  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12294.305     ± 25.171  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4579.245     ± 41.630  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2795.383    ± 254.988  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4360.612     ± 28.507  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23468.371    ± 752.029  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23188.278    ± 610.499  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     478762.732   ± 4273.449  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483915.786   ± 4207.428  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     497943.297   ± 3391.013  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     502207.558   ± 3072.229  ops/s
```

## Notes

- **Score** = the JMH primary metric; throughput is higher-is-better and latency is lower-is-better.
- **Error** = 99.9% confidence interval
- Scores for different benchmark methods are not ranked against one another; they may measure different workloads.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |

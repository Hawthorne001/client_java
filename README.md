# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-05T00:26:10Z
- **Commit:** [`a614601`](https://github.com/Hawthorne001/client_java/commit/a614601f037884b8ae7ca6454f2ffb2b5e1e4003)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.12K | ± 1.28K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.08K | ± 768.19 | ops/s | 1.2x slower |
| prometheusAdd | 51.43K | ± 181.10 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.91K | ± 8.44K | ops/s | 1.5x slower |
| simpleclientInc | 6.77K | ± 23.23 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.59K | ± 168.28 | ops/s | 9.9x slower |
| simpleclientAdd | 6.36K | ± 227.85 | ops/s | 10x slower |
| openTelemetryInc | 1.40K | ± 117.67 | ops/s | 47x slower |
| openTelemetryAdd | 1.28K | ± 18.94 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.15K | ± 49.39 | ops/s | 57x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.07K | ± 1.50K | ops/s | **fastest** |
| simpleclient | 4.56K | ± 42.53 | ops/s | 1.1x slower |
| prometheusNative | 3.14K | ± 152.33 | ops/s | 1.6x slower |
| openTelemetryClassic | 685.10 | ± 39.77 | ops/s | 7.4x slower |
| openTelemetryExponential | 553.74 | ± 13.96 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.48K | ± 4.72K | ops/s | **fastest** |
| openMetricsWriteToNull | 481.79K | ± 4.32K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 481.19K | ± 9.21K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 478.40K | ± 4.41K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44906.276   ± 8440.981  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1282.582     ± 18.939  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1400.168    ± 117.673  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1147.669     ± 49.387  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51427.641    ± 181.102  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65120.394   ± 1281.909  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56083.012    ± 768.188  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6362.861    ± 227.850  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6772.978     ± 23.232  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6594.772    ± 168.284  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        685.096     ± 39.769  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        553.738     ± 13.957  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5067.539   ± 1500.898  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3140.577    ± 152.326  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4563.073     ± 42.529  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     478396.506   ± 4413.025  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481789.840   ± 4320.225  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481187.407   ± 9209.723  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493482.774   ± 4719.917  ops/s
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

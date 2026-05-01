# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-01T10:03:10Z
- **Commit:** [`1d99672`](https://github.com/Hawthorne001/client_java/commit/1d996722d26b910992bc9f8f477f9af8f811096d)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.07K | ± 743.57 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.51K | ± 1.11K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 30.16K | ± 1.11K | ops/s | 1.0x slower |
| prometheusAdd | 28.30K | ± 474.54 | ops/s | 1.1x slower |
| simpleclientInc | 6.98K | ± 117.95 | ops/s | 4.4x slower |
| simpleclientNoLabelsInc | 6.84K | ± 149.13 | ops/s | 4.5x slower |
| simpleclientAdd | 6.22K | ± 246.80 | ops/s | 5.0x slower |
| openTelemetryInc | 2.64K | ± 63.79 | ops/s | 12x slower |
| openTelemetryIncNoLabels | 2.64K | ± 159.32 | ops/s | 12x slower |
| openTelemetryAdd | 2.31K | ± 101.78 | ops/s | 13x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.48K | ± 34.67 | ops/s | **fastest** |
| prometheusClassic | 2.59K | ± 505.36 | ops/s | 1.7x slower |
| prometheusNative | 2.11K | ± 132.52 | ops/s | 2.1x slower |
| openTelemetryClassic | 587.26 | ± 32.95 | ops/s | 7.6x slower |
| openTelemetryExponential | 460.78 | ± 29.43 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 318.12K | ± 944.18 | ops/s | **fastest** |
| prometheusWriteToByteArray | 315.44K | ± 1.80K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 299.51K | ± 892.38 | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 297.72K | ± 726.23 | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30161.199   ± 1108.272  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2311.150    ± 101.781  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2644.684     ± 63.790  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2642.948    ± 159.325  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28303.004    ± 474.542  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31074.045    ± 743.572  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30512.623   ± 1106.548  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6222.215    ± 246.802  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6983.758    ± 117.947  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6837.218    ± 149.134  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        587.261     ± 32.954  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        460.779     ± 29.427  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2588.797    ± 505.360  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2110.001    ± 132.521  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4484.503     ± 34.665  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     297716.058    ± 726.232  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     299514.103    ± 892.377  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     315443.916   ± 1800.861  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     318121.652    ± 944.176  ops/s
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

# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-17T15:47:32Z
- **Commit:** [`05ad751`](https://github.com/Hawthorne001/client_java/commit/05ad751a40053f11eae90b9e6cbd741814ca71a7)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.20K | ± 1.41K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.56K | ± 118.35 | ops/s | 1.1x slower |
| prometheusAdd | 51.37K | ± 247.48 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.40K | ± 1.01K | ops/s | 1.3x slower |
| simpleclientInc | 6.75K | ± 76.47 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.49K | ± 173.13 | ops/s | 9.9x slower |
| simpleclientAdd | 6.26K | ± 232.83 | ops/s | 10x slower |
| openTelemetryAdd | 1.42K | ± 221.69 | ops/s | 45x slower |
| openTelemetryInc | 1.36K | ± 239.49 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.30K | ± 171.02 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.07K | ± 942.05 | ops/s | **fastest** |
| simpleclient | 4.58K | ± 25.22 | ops/s | 1.5x slower |
| prometheusNative | 2.85K | ± 332.44 | ops/s | 2.5x slower |
| openTelemetryClassic | 702.33 | ± 27.49 | ops/s | 10x slower |
| openTelemetryExponential | 529.12 | ± 9.91 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 494.92K | ± 752.50 | ops/s | **fastest** |
| prometheusWriteToNull | 493.74K | ± 2.86K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 486.63K | ± 4.74K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 478.31K | ± 4.81K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49401.359   ± 1008.884  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1421.156    ± 221.689  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1360.290    ± 239.490  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1303.330    ± 171.020  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51369.972    ± 247.480  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64197.001   ± 1412.860  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56562.991    ± 118.347  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6257.707    ± 232.831  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6751.869     ± 76.474  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6494.577    ± 173.133  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        702.325     ± 27.491  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        529.119      ± 9.911  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7065.834    ± 942.051  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2846.862    ± 332.444  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4577.340     ± 25.215  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     478305.100   ± 4806.327  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     486634.299   ± 4736.245  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     494922.076    ± 752.501  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493737.046   ± 2863.847  ops/s
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

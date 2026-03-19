# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-19T09:58:44Z
- **Commit:** [`01f53e9`](https://github.com/Hawthorne001/client_java/commit/01f53e945edfc337b9ed13c0b5c28c8a170c3a48)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.43K | ± 1.48K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.38K | ± 211.15 | ops/s | 1.1x slower |
| prometheusAdd | 51.22K | ± 471.40 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.92K | ± 413.66 | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 205.92 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.57K | ± 193.10 | ops/s | 10.0x slower |
| simpleclientAdd | 6.24K | ± 282.69 | ops/s | 10x slower |
| openTelemetryInc | 1.38K | ± 170.15 | ops/s | 48x slower |
| openTelemetryAdd | 1.28K | ± 29.75 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.21K | ± 55.66 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.81K | ± 1.42K | ops/s | **fastest** |
| simpleclient | 4.57K | ± 31.25 | ops/s | 1.3x slower |
| prometheusNative | 2.88K | ± 296.68 | ops/s | 2.0x slower |
| openTelemetryClassic | 726.26 | ± 65.07 | ops/s | 8.0x slower |
| openTelemetryExponential | 586.78 | ± 43.44 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 491.89K | ± 5.71K | ops/s | **fastest** |
| prometheusWriteToByteArray | 490.56K | ± 1.83K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 488.86K | ± 2.55K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 478.06K | ± 2.72K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49915.621    ± 413.655  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1284.506     ± 29.747  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1375.919    ± 170.154  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1207.859     ± 55.656  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51221.813    ± 471.404  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65428.681   ± 1480.391  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57379.845    ± 211.151  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6240.669    ± 282.695  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6656.409    ± 205.922  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6569.673    ± 193.098  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        726.259     ± 65.070  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        586.781     ± 43.444  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5813.864   ± 1416.586  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2881.064    ± 296.682  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4574.737     ± 31.249  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     478063.026   ± 2717.120  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488864.836   ± 2551.872  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     490560.654   ± 1828.300  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     491890.872   ± 5708.019  ops/s
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

# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-22T10:14:52Z
- **Commit:** [`5ce2b57`](https://github.com/Hawthorne001/client_java/commit/5ce2b575272a06b5115f40f3298d5c861cef8bbd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.58K | ± 1.23K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.16K | ± 143.89 | ops/s | 1.1x slower |
| prometheusAdd | 50.50K | ± 229.37 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.49K | ± 1.08K | ops/s | 1.3x slower |
| simpleclientInc | 6.67K | ± 195.21 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.57K | ± 210.74 | ops/s | 9.8x slower |
| simpleclientAdd | 6.56K | ± 10.11 | ops/s | 9.8x slower |
| openTelemetryAdd | 1.40K | ± 248.41 | ops/s | 46x slower |
| openTelemetryInc | 1.39K | ± 215.55 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.21K | ± 17.38 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.99K | ± 1.81K | ops/s | **fastest** |
| simpleclient | 4.55K | ± 32.70 | ops/s | 1.3x slower |
| prometheusNative | 2.87K | ± 276.59 | ops/s | 2.1x slower |
| openTelemetryClassic | 683.81 | ± 28.69 | ops/s | 8.8x slower |
| openTelemetryExponential | 576.62 | ± 33.99 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 500.97K | ± 4.13K | ops/s | **fastest** |
| prometheusWriteToByteArray | 496.88K | ± 1.98K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 493.54K | ± 3.85K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 488.84K | ± 2.32K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49491.918   ± 1083.814  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1398.810    ± 248.414  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1388.149    ± 215.550  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1207.434     ± 17.381  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50495.498    ± 229.367  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64578.210   ± 1231.346  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57160.006    ± 143.892  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6559.881     ± 10.108  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6665.338    ± 195.208  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6570.247    ± 210.742  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        683.809     ± 28.693  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        576.624     ± 33.990  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5993.765   ± 1809.781  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2874.140    ± 276.586  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4551.603     ± 32.696  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     488836.937   ± 2324.013  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     493543.432   ± 3849.948  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     496875.721   ± 1982.621  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     500966.883   ± 4132.767  ops/s
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

# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-01T04:38:22Z
- **Commit:** [`8add981`](https://github.com/Hawthorne001/client_java/commit/8add981e2c57d68aa9a8b497b2496f3ef2904d38)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.90K | ± 53.05 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.44K | ± 353.25 | ops/s | 1.2x slower |
| prometheusAdd | 48.50K | ± 136.80 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 42.26K | ± 1.77K | ops/s | 1.4x slower |
| simpleclientInc | 6.17K | ± 54.64 | ops/s | 9.7x slower |
| simpleclientAdd | 6.14K | ± 46.40 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 5.91K | ± 24.87 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 5.36K | ± 1.17K | ops/s | 11x slower |
| openTelemetryInc | 4.07K | ± 430.19 | ops/s | 15x slower |
| openTelemetryAdd | 3.93K | ± 819.49 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.23K | ± 74.96 | ops/s | **fastest** |
| simpleclient | 4.15K | ± 22.73 | ops/s | 1.7x slower |
| prometheusNative | 3.01K | ± 232.99 | ops/s | 2.4x slower |
| openTelemetryClassic | 727.83 | ± 21.18 | ops/s | 9.9x slower |
| openTelemetryExponential | 563.11 | ± 3.31 | ops/s | 13x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 27.27K | ± 188.34 | ops/s | **fastest** |
| prometheusWriteToNull | 26.93K | ± 775.07 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 578.91K | ± 17.38K | ops/s | **fastest** |
| prometheusWriteToByteArray | 573.59K | ± 5.04K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 546.51K | ± 3.09K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 540.82K | ± 5.54K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42263.938   ± 1774.124  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3930.723    ± 819.487  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4067.444    ± 430.190  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       5358.459   ± 1174.285  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48499.285    ± 136.805  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59898.694     ± 53.047  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51436.421    ± 353.251  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6137.614     ± 46.396  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6168.698     ± 54.639  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5906.393     ± 24.868  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        727.831     ± 21.182  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        563.113      ± 3.306  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7234.123     ± 74.955  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3008.467    ± 232.990  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4148.462     ± 22.735  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27266.678    ± 188.344  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      26931.410    ± 775.065  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     540824.114   ± 5538.675  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     546511.768   ± 3089.586  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     573587.866   ± 5042.717  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     578911.744  ± 17376.147  ops/s
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

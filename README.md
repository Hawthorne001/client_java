# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-30T13:26:37Z
- **Commit:** [`6beb7fd`](https://github.com/Hawthorne001/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.41K | ± 109.16 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.24K | ± 145.32 | ops/s | 1.2x slower |
| prometheusAdd | 50.99K | ± 593.68 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.15K | ± 1.63K | ops/s | 1.4x slower |
| simpleclientInc | 6.72K | ± 13.36 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.54K | ± 145.75 | ops/s | 10x slower |
| simpleclientAdd | 6.27K | ± 355.38 | ops/s | 11x slower |
| openTelemetryAdd | 1.28K | ± 26.70 | ops/s | 52x slower |
| openTelemetryInc | 1.27K | ± 29.17 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.21K | ± 42.46 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.26K | ± 1.93K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 54.78 | ops/s | 1.4x slower |
| prometheusNative | 2.92K | ± 368.57 | ops/s | 2.1x slower |
| openTelemetryClassic | 686.02 | ± 31.80 | ops/s | 9.1x slower |
| openTelemetryExponential | 557.29 | ± 44.71 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 487.35K | ± 3.63K | ops/s | **fastest** |
| prometheusWriteToByteArray | 481.65K | ± 8.47K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 468.27K | ± 8.25K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 465.83K | ± 9.24K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49147.020   ± 1627.350  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1276.850     ± 26.699  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1269.839     ± 29.171  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1206.360     ± 42.459  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50986.742    ± 593.676  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66405.842    ± 109.159  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57243.646    ± 145.321  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6267.010    ± 355.379  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6715.155     ± 13.359  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6542.860    ± 145.750  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        686.016     ± 31.803  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        557.291     ± 44.715  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6260.686   ± 1927.003  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2920.114    ± 368.566  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4430.835     ± 54.783  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     468273.060   ± 8246.435  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     465828.840   ± 9242.897  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481650.765   ± 8468.723  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     487348.442   ± 3626.649  ops/s
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

# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-05T05:13:19Z
- **Commit:** [`574fb73`](https://github.com/Hawthorne001/client_java/commit/574fb73e4d7eec6bbfd483378600579b966631a6)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.28K | ± 1.51K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.89K | ± 299.42 | ops/s | 1.1x slower |
| prometheusAdd | 51.21K | ± 749.05 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.24K | ± 940.64 | ops/s | 1.4x slower |
| simpleclientInc | 6.55K | ± 45.62 | ops/s | 10.0x slower |
| simpleclientAdd | 6.48K | ± 29.31 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.36K | ± 32.64 | ops/s | 10x slower |
| openTelemetryInc | 3.23K | ± 355.91 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.20K | ± 84.28 | ops/s | 20x slower |
| openTelemetryAdd | 2.90K | ± 194.62 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.98K | ± 422.66 | ops/s | **fastest** |
| simpleclient | 4.45K | ± 103.68 | ops/s | 1.1x slower |
| prometheusNative | 2.91K | ± 295.01 | ops/s | 1.7x slower |
| openTelemetryClassic | 755.52 | ± 32.34 | ops/s | 6.6x slower |
| openTelemetryExponential | 579.58 | ± 13.61 | ops/s | 8.6x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.95K | ± 541.11 | ops/s | **fastest** |
| prometheusWriteToNull | 23.38K | ± 834.43 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 503.31K | ± 3.00K | ops/s | **fastest** |
| prometheusWriteToByteArray | 495.77K | ± 4.10K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 474.97K | ± 5.23K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 469.57K | ± 2.77K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48243.066    ± 940.640  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2903.252    ± 194.621  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3234.909    ± 355.909  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3202.722     ± 84.275  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51208.947    ± 749.045  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65275.684   ± 1506.807  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56886.408    ± 299.424  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6475.870     ± 29.311  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6545.743     ± 45.623  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6362.365     ± 32.636  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        755.519     ± 32.344  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        579.579     ± 13.611  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4977.715    ± 422.665  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2914.985    ± 295.009  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4445.781    ± 103.678  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23949.298    ± 541.105  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23377.144    ± 834.431  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469573.475   ± 2773.967  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     474967.021   ± 5232.003  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     495767.320   ± 4097.264  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     503311.220   ± 2999.460  ops/s
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

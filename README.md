# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-12T21:56:36Z
- **Commit:** [`4b69f40`](https://github.com/Hawthorne001/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.51K | ± 623.52 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.91K | ± 190.19 | ops/s | 1.2x slower |
| prometheusAdd | 48.33K | ± 4.70K | ops/s | 1.4x slower |
| codahaleIncNoLabels | 47.85K | ± 1.16K | ops/s | 1.4x slower |
| simpleclientInc | 6.44K | ± 128.35 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.41K | ± 168.18 | ops/s | 10x slower |
| simpleclientAdd | 6.10K | ± 345.73 | ops/s | 11x slower |
| openTelemetryAdd | 1.61K | ± 169.63 | ops/s | 41x slower |
| openTelemetryInc | 1.40K | ± 246.47 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.25K | ± 25.44 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.18K | ± 2.28K | ops/s | **fastest** |
| simpleclient | 4.40K | ± 83.01 | ops/s | 1.2x slower |
| prometheusNative | 3.19K | ± 131.55 | ops/s | 1.6x slower |
| openTelemetryClassic | 679.84 | ± 61.04 | ops/s | 7.6x slower |
| openTelemetryExponential | 583.84 | ± 26.78 | ops/s | 8.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 483.25K | ± 6.30K | ops/s | **fastest** |
| prometheusWriteToByteArray | 481.29K | ± 6.68K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 475.74K | ± 6.76K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 468.60K | ± 4.62K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47850.185   ± 1161.652  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1607.859    ± 169.632  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1397.861    ± 246.468  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1251.707     ± 25.440  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48333.595   ± 4698.144  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66514.057    ± 623.523  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56913.213    ± 190.186  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6097.102    ± 345.727  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6436.321    ± 128.351  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6412.483    ± 168.176  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        679.841     ± 61.044  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        583.841     ± 26.780  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5175.621   ± 2284.124  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3188.933    ± 131.554  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4401.062     ± 83.012  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     468596.544   ± 4621.433  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     475744.101   ± 6757.407  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481287.785   ± 6680.374  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     483247.017   ± 6299.495  ops/s
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

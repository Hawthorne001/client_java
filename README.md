# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-15T17:12:34Z
- **Commit:** [`94b33b7`](https://github.com/Hawthorne001/client_java/commit/94b33b7527ce21b12ff2a3f9cd23c63cdb42e274)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.54K | ± 59.37 | ops/s | **fastest** |
| prometheusNoLabelsInc | 29.86K | ± 1.05K | ops/s | 1.1x slower |
| codahaleIncNoLabels | 29.08K | ± 496.05 | ops/s | 1.1x slower |
| prometheusAdd | 28.62K | ± 145.37 | ops/s | 1.1x slower |
| simpleclientInc | 6.70K | ± 251.09 | ops/s | 4.7x slower |
| simpleclientAdd | 6.64K | ± 69.73 | ops/s | 4.8x slower |
| simpleclientNoLabelsInc | 6.49K | ± 226.26 | ops/s | 4.9x slower |
| openTelemetryIncNoLabels | 2.82K | ± 307.94 | ops/s | 11x slower |
| openTelemetryAdd | 2.51K | ± 225.12 | ops/s | 13x slower |
| openTelemetryInc | 2.40K | ± 71.77 | ops/s | 13x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.44K | ± 54.53 | ops/s | **fastest** |
| prometheusClassic | 3.12K | ± 404.01 | ops/s | 1.4x slower |
| prometheusNative | 2.15K | ± 256.97 | ops/s | 2.1x slower |
| openTelemetryClassic | 570.48 | ± 31.16 | ops/s | 7.8x slower |
| openTelemetryExponential | 424.83 | ± 10.41 | ops/s | 10x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 18.19K | ± 147.22 | ops/s | **fastest** |
| openMetricsWriteToNull | 18.11K | ± 218.86 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 312.79K | ± 2.64K | ops/s | **fastest** |
| prometheusWriteToByteArray | 309.25K | ± 3.16K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 293.24K | ± 2.41K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 291.94K | ± 1.37K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29078.129    ± 496.050  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2514.947    ± 225.118  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2396.298     ± 71.774  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2818.772    ± 307.937  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28617.323    ± 145.367  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31542.005     ± 59.367  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      29856.321   ± 1054.257  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6639.317     ± 69.733  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6695.057    ± 251.094  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6492.521    ± 226.261  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        570.477     ± 31.159  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        424.826     ± 10.413  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3115.716    ± 404.012  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2148.604    ± 256.967  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4444.306     ± 54.532  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      18108.928    ± 218.865  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      18188.333    ± 147.215  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     291936.507   ± 1370.438  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     293235.942   ± 2405.113  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     309253.819   ± 3162.468  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     312788.917   ± 2642.540  ops/s
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

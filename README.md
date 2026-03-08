# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-08T02:44:46Z
- **Commit:** [`dfdec65`](https://github.com/Hawthorne001/client_java/commit/dfdec650b9fb6d7280d1a9c34d799eae195e76a4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.90K | ± 252.87 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.21K | ± 84.32 | ops/s | 1.2x slower |
| prometheusAdd | 51.69K | ± 179.74 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.97K | ± 1.09K | ops/s | 1.4x slower |
| simpleclientInc | 6.71K | ± 183.48 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.48K | ± 166.23 | ops/s | 10x slower |
| simpleclientAdd | 6.40K | ± 233.35 | ops/s | 10x slower |
| openTelemetryAdd | 1.35K | ± 244.26 | ops/s | 49x slower |
| openTelemetryInc | 1.28K | ± 40.39 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.20K | ± 46.81 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.91K | ± 1.07K | ops/s | **fastest** |
| simpleclient | 4.60K | ± 8.01 | ops/s | 1.3x slower |
| prometheusNative | 3.07K | ± 265.29 | ops/s | 1.9x slower |
| openTelemetryClassic | 686.19 | ± 42.34 | ops/s | 8.6x slower |
| openTelemetryExponential | 553.86 | ± 23.61 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.72K | ± 1.37K | ops/s | **fastest** |
| prometheusWriteToByteArray | 487.98K | ± 2.19K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 482.14K | ± 4.49K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 478.23K | ± 3.88K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47970.812   ± 1091.593  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1347.501    ± 244.265  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1279.534     ± 40.394  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1204.671     ± 46.807  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51686.143    ± 179.742  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65902.827    ± 252.873  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57208.619     ± 84.319  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6403.077    ± 233.354  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6712.820    ± 183.485  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6482.900    ± 166.230  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        686.195     ± 42.344  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        553.859     ± 23.612  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5911.408   ± 1068.711  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3068.399    ± 265.287  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4602.355      ± 8.010  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     478230.349   ± 3883.730  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482143.344   ± 4485.324  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487984.072   ± 2192.483  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493719.991   ± 1371.494  ops/s
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

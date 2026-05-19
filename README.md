# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-19T19:22:10Z
- **Commit:** [`94b33b7`](https://github.com/Hawthorne001/client_java/commit/94b33b7527ce21b12ff2a3f9cd23c63cdb42e274)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.92K | ± 1.22K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.13K | ± 1.07K | ops/s | 1.2x slower |
| prometheusAdd | 51.44K | ± 356.25 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.45K | ± 1.13K | ops/s | 1.3x slower |
| simpleclientInc | 6.58K | ± 22.05 | ops/s | 9.9x slower |
| simpleclientAdd | 6.46K | ± 78.19 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.34K | ± 48.91 | ops/s | 10x slower |
| openTelemetryAdd | 3.50K | ± 566.04 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.31K | ± 151.63 | ops/s | 20x slower |
| openTelemetryInc | 2.99K | ± 259.26 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.51K | ± 881.28 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 94.74 | ops/s | 1.2x slower |
| prometheusNative | 3.06K | ± 247.01 | ops/s | 1.8x slower |
| openTelemetryClassic | 766.78 | ± 18.87 | ops/s | 7.2x slower |
| openTelemetryExponential | 691.53 | ± 69.80 | ops/s | 8.0x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.07K | ± 1.19K | ops/s | **fastest** |
| openMetricsWriteToNull | 22.75K | ± 327.63 | ops/s | 1.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 519.07K | ± 6.49K | ops/s | **fastest** |
| prometheusWriteToByteArray | 505.99K | ± 3.75K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 492.14K | ± 1.94K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 488.30K | ± 3.39K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48448.483   ± 1129.264  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3502.872    ± 566.045  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2988.759    ± 259.262  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3312.684    ± 151.634  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51437.278    ± 356.245  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64916.330   ± 1221.229  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56131.824   ± 1070.435  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6460.577     ± 78.193  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6578.415     ± 22.049  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6340.554     ± 48.907  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        766.776     ± 18.865  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        691.529     ± 69.797  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5507.126    ± 881.284  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3055.488    ± 247.014  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4419.714     ± 94.737  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      22746.101    ± 327.635  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24069.320   ± 1190.170  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     488297.127   ± 3389.017  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     492140.851   ± 1943.773  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     505990.935   ± 3749.224  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     519067.726   ± 6491.063  ops/s
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

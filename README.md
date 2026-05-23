# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-23T22:28:29Z
- **Commit:** [`a241c16`](https://github.com/Hawthorne001/client_java/commit/a241c165927d3cbb91b97eedd52de9c9eff595d0)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.95K | ± 1.32K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.93K | ± 367.01 | ops/s | 1.1x slower |
| prometheusAdd | 51.49K | ± 101.47 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.77K | ± 1.52K | ops/s | 1.3x slower |
| simpleclientInc | 6.55K | ± 49.15 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.34K | ± 7.60 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 237.25 | ops/s | 10x slower |
| openTelemetryAdd | 3.49K | ± 380.48 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.21K | ± 103.83 | ops/s | 20x slower |
| openTelemetryInc | 3.21K | ± 58.88 | ops/s | 20x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.16K | ± 1.65K | ops/s | **fastest** |
| simpleclient | 4.37K | ± 84.69 | ops/s | 1.2x slower |
| prometheusNative | 2.52K | ± 143.00 | ops/s | 2.0x slower |
| openTelemetryClassic | 758.82 | ± 17.82 | ops/s | 6.8x slower |
| openTelemetryExponential | 635.07 | ± 93.28 | ops/s | 8.1x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.56K | ± 608.66 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.08K | ± 727.02 | ops/s | 1.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 512.58K | ± 4.38K | ops/s | **fastest** |
| prometheusWriteToByteArray | 506.84K | ± 7.20K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 491.58K | ± 1.64K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 478.30K | ± 3.23K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48771.746   ± 1520.953  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3485.720    ± 380.483  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3212.320     ± 58.877  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3214.336    ± 103.826  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51492.750    ± 101.472  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64953.392   ± 1316.674  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56931.671    ± 367.009  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6319.151    ± 237.245  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6547.774     ± 49.150  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6338.614      ± 7.603  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        758.818     ± 17.822  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        635.074     ± 93.278  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5156.290   ± 1649.670  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2519.191    ± 142.997  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4374.241     ± 84.690  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23077.423    ± 727.020  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24556.877    ± 608.657  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     478295.186   ± 3229.869  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     491581.528   ± 1637.164  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     506841.201   ± 7203.084  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     512578.440   ± 4383.860  ops/s
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

# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-25T05:07:46Z
- **Commit:** [`5699469`](https://github.com/Hawthorne001/client_java/commit/5699469d345b9d3aaf3d6c0e5e76de2959477269)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.15K | ± 1.34K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.84K | ± 507.13 | ops/s | 1.1x slower |
| prometheusAdd | 51.32K | ± 583.93 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.60K | ± 1.45K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.54K | ± 100.51 | ops/s | 10.0x slower |
| simpleclientInc | 6.51K | ± 223.73 | ops/s | 10x slower |
| simpleclientAdd | 5.92K | ± 41.21 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 3.47K | ± 318.48 | ops/s | 19x slower |
| openTelemetryInc | 3.21K | ± 437.22 | ops/s | 20x slower |
| openTelemetryAdd | 3.10K | ± 251.50 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.14K | ± 485.75 | ops/s | **fastest** |
| simpleclient | 4.45K | ± 57.84 | ops/s | 1.2x slower |
| prometheusNative | 2.70K | ± 259.51 | ops/s | 1.9x slower |
| openTelemetryClassic | 758.49 | ± 18.80 | ops/s | 6.8x slower |
| openTelemetryExponential | 719.39 | ± 8.47 | ops/s | 7.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 484.24K | ± 1.83K | ops/s | **fastest** |
| prometheusWriteToByteArray | 478.73K | ± 3.42K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 471.51K | ± 2.87K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 466.04K | ± 2.59K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48601.966   ± 1453.323  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3104.450    ± 251.497  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3210.817    ± 437.216  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3470.994    ± 318.476  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51316.351    ± 583.928  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65152.704   ± 1341.483  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56844.321    ± 507.130  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5921.788     ± 41.214  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6508.624    ± 223.726  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6538.793    ± 100.507  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        758.492     ± 18.799  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        719.391      ± 8.466  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5135.228    ± 485.755  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2701.565    ± 259.511  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4449.212     ± 57.840  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     466043.043   ± 2588.627  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     471514.656   ± 2873.349  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     478731.186   ± 3418.455  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     484235.690   ± 1829.440  ops/s
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

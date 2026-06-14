# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-13T07:41:53Z
- **Commit:** [`9672749`](https://github.com/Hawthorne001/client_java/commit/9672749085f9029ccb7328b3e88e8e78fa29e402)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 76.44K | ± 652.43 | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.35K | ± 994.32 | ops/s | 1.2x slower |
| prometheusAdd | 62.56K | ± 561.59 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 56.72K | ± 355.02 | ops/s | 1.3x slower |
| simpleclientInc | 8.01K | ± 148.62 | ops/s | 9.5x slower |
| simpleclientAdd | 7.74K | ± 176.78 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 7.62K | ± 33.26 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 6.37K | ± 1.39K | ops/s | 12x slower |
| openTelemetryInc | 5.74K | ± 1.36K | ops/s | 13x slower |
| openTelemetryAdd | 4.17K | ± 250.31 | ops/s | 18x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.21K | ± 1.83K | ops/s | **fastest** |
| simpleclient | 5.88K | ± 121.04 | ops/s | 1.2x slower |
| prometheusNative | 3.99K | ± 157.91 | ops/s | 1.8x slower |
| openTelemetryClassic | 934.14 | ± 31.32 | ops/s | 7.7x slower |
| openTelemetryExponential | 719.59 | ± 41.14 | ops/s | 10x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 35.40K | ± 252.76 | ops/s | **fastest** |
| openMetricsWriteToNull | 34.88K | ± 273.46 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 691.81K | ± 5.12K | ops/s | **fastest** |
| prometheusWriteToByteArray | 687.20K | ± 3.41K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 654.60K | ± 7.65K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 636.76K | ± 5.30K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56718.036    ± 355.019  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4167.444    ± 250.308  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5741.303   ± 1360.854  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       6370.289   ± 1388.814  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62558.691    ± 561.587  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76435.675    ± 652.434  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66345.597    ± 994.321  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7743.594    ± 176.780  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       8009.306    ± 148.615  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7621.802     ± 33.256  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        934.139     ± 31.316  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        719.585     ± 41.144  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7213.329   ± 1833.966  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3988.416    ± 157.906  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5880.533    ± 121.038  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      34884.480    ± 273.455  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35399.156    ± 252.762  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     636764.978   ± 5296.588  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     654600.274   ± 7654.272  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     687200.673   ± 3411.353  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     691811.101   ± 5121.684  ops/s
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

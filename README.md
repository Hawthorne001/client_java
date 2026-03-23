# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-23T10:35:53Z
- **Commit:** [`6beb7fd`](https://github.com/Hawthorne001/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.44K | ± 522.36 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.04K | ± 502.93 | ops/s | 1.2x slower |
| prometheusAdd | 51.46K | ± 460.39 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.21K | ± 1.04K | ops/s | 1.4x slower |
| simpleclientInc | 6.63K | ± 239.24 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.55K | ± 208.53 | ops/s | 10x slower |
| simpleclientAdd | 6.41K | ± 191.67 | ops/s | 10x slower |
| openTelemetryAdd | 1.40K | ± 199.70 | ops/s | 47x slower |
| openTelemetryInc | 1.39K | ± 194.84 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.22K | ± 47.57 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.29K | ± 352.79 | ops/s | **fastest** |
| simpleclient | 4.52K | ± 46.88 | ops/s | 1.2x slower |
| prometheusNative | 3.08K | ± 305.23 | ops/s | 1.7x slower |
| openTelemetryClassic | 664.18 | ± 26.67 | ops/s | 8.0x slower |
| openTelemetryExponential | 551.05 | ± 26.31 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 490.03K | ± 2.25K | ops/s | **fastest** |
| prometheusWriteToNull | 487.41K | ± 4.86K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 484.09K | ± 1.88K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 483.00K | ± 4.30K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49212.458   ± 1036.059  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1401.976    ± 199.702  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1391.411    ± 194.838  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1221.758     ± 47.573  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51459.392    ± 460.395  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66443.026    ± 522.356  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57038.619    ± 502.929  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6410.723    ± 191.674  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6633.653    ± 239.245  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6550.223    ± 208.533  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        664.180     ± 26.672  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        551.047     ± 26.315  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5292.177    ± 352.793  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3084.323    ± 305.226  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4517.963     ± 46.881  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     483002.665   ± 4299.762  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     484093.391   ± 1881.355  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     490029.618   ± 2247.731  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     487412.679   ± 4856.120  ops/s
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

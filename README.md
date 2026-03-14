# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-14T07:21:09Z
- **Commit:** [`b81332e`](https://github.com/Hawthorne001/client_java/commit/b81332e3a09e465f956f118a2403e64b83771ae5)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.11K | ± 2.75K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.16K | ± 64.57 | ops/s | 1.1x slower |
| prometheusAdd | 51.62K | ± 165.80 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.21K | ± 1.20K | ops/s | 1.3x slower |
| simpleclientInc | 6.77K | ± 27.72 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 6.27K | ± 63.76 | ops/s | 10x slower |
| simpleclientAdd | 6.23K | ± 276.27 | ops/s | 10x slower |
| openTelemetryAdd | 1.44K | ± 231.96 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.31K | ± 246.16 | ops/s | 48x slower |
| openTelemetryInc | 1.27K | ± 17.91 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.98K | ± 1.15K | ops/s | **fastest** |
| simpleclient | 4.57K | ± 21.68 | ops/s | 1.3x slower |
| prometheusNative | 2.86K | ± 286.95 | ops/s | 2.1x slower |
| openTelemetryClassic | 702.95 | ± 64.34 | ops/s | 8.5x slower |
| openTelemetryExponential | 558.88 | ± 6.68 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 496.09K | ± 2.73K | ops/s | **fastest** |
| openMetricsWriteToNull | 487.29K | ± 2.78K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 483.83K | ± 7.57K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 482.34K | ± 3.89K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49210.870   ± 1197.571  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1440.935    ± 231.957  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1274.277     ± 17.908  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1305.913    ± 246.164  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51618.398    ± 165.796  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63113.985   ± 2748.664  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57164.914     ± 64.568  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6230.427    ± 276.269  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6765.542     ± 27.721  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6273.630     ± 63.756  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        702.952     ± 64.343  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        558.878      ± 6.681  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5982.097   ± 1151.209  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2856.894    ± 286.954  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4566.890     ± 21.676  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     482339.198   ± 3894.694  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     487288.112   ± 2778.197  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     483833.870   ± 7573.134  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     496088.671   ± 2728.706  ops/s
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

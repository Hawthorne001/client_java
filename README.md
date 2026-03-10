# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-10T04:15:03Z
- **Commit:** [`e6eb2f9`](https://github.com/Hawthorne001/client_java/commit/e6eb2f91d6da13485a83c4eab5171f510382f800)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.62K | ± 1.15K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.53K | ± 833.83 | ops/s | 1.2x slower |
| prometheusAdd | 51.66K | ± 58.93 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.89K | ± 2.00K | ops/s | 1.4x slower |
| simpleclientInc | 6.76K | ± 29.66 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.45K | ± 216.98 | ops/s | 10x slower |
| simpleclientAdd | 6.21K | ± 253.25 | ops/s | 11x slower |
| openTelemetryAdd | 1.56K | ± 227.69 | ops/s | 42x slower |
| openTelemetryInc | 1.34K | ± 233.54 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.32K | ± 153.21 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.41K | ± 1.39K | ops/s | **fastest** |
| simpleclient | 4.52K | ± 46.27 | ops/s | 1.2x slower |
| prometheusNative | 2.83K | ± 230.50 | ops/s | 1.9x slower |
| openTelemetryClassic | 698.15 | ± 11.21 | ops/s | 7.8x slower |
| openTelemetryExponential | 534.02 | ± 6.65 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 486.41K | ± 3.82K | ops/s | **fastest** |
| prometheusWriteToByteArray | 482.61K | ± 6.55K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 477.28K | ± 14.73K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 477.16K | ± 3.88K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47893.260   ± 2004.314  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1559.384    ± 227.695  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1337.268    ± 233.543  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1316.985    ± 153.214  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51663.449     ± 58.934  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65620.684   ± 1150.037  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55532.448    ± 833.830  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6206.509    ± 253.252  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6760.797     ± 29.662  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6445.171    ± 216.982  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        698.147     ± 11.208  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        534.022      ± 6.651  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5412.171   ± 1385.758  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2827.645    ± 230.503  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4522.161     ± 46.272  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     477159.978   ± 3878.237  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     477276.797  ± 14725.093  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     482606.344   ± 6548.336  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     486406.465   ± 3821.145  ops/s
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

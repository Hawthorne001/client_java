# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-20T09:20:26Z
- **Commit:** [`ce14377`](https://github.com/Hawthorne001/client_java/commit/ce1437725c9745d247308c5db63f92469c37125d)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.55K | ± 1.71K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.94K | ± 788.38 | ops/s | 1.2x slower |
| prometheusAdd | 50.89K | ± 654.96 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.62K | ± 2.07K | ops/s | 1.3x slower |
| simpleclientInc | 6.58K | ± 16.59 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.29K | ± 41.37 | ops/s | 10x slower |
| simpleclientAdd | 6.27K | ± 262.94 | ops/s | 10x slower |
| openTelemetryAdd | 3.96K | ± 245.71 | ops/s | 17x slower |
| openTelemetryIncNoLabels | 3.34K | ± 398.70 | ops/s | 20x slower |
| openTelemetryInc | 3.14K | ± 115.54 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.03K | ± 416.07 | ops/s | **fastest** |
| simpleclient | 4.46K | ± 60.03 | ops/s | 1.1x slower |
| prometheusNative | 2.89K | ± 233.67 | ops/s | 1.7x slower |
| openTelemetryClassic | 763.35 | ± 15.90 | ops/s | 6.6x slower |
| openTelemetryExponential | 657.65 | ± 82.24 | ops/s | 7.6x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.94K | ± 476.19 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.70K | ± 858.96 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 495.89K | ± 5.68K | ops/s | **fastest** |
| prometheusWriteToByteArray | 487.08K | ± 2.48K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 469.79K | ± 2.98K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 468.78K | ± 3.90K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49620.876   ± 2072.915  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3964.967    ± 245.709  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3137.265    ± 115.545  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3341.782    ± 398.698  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50894.845    ± 654.963  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65546.715   ± 1706.816  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55938.110    ± 788.378  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6267.974    ± 262.941  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6575.572     ± 16.591  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6286.329     ± 41.366  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        763.354     ± 15.898  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        657.645     ± 82.239  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5027.640    ± 416.068  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2885.945    ± 233.672  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4459.390     ± 60.026  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23695.231    ± 858.956  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23937.144    ± 476.195  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469787.483   ± 2983.609  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     468781.750   ± 3902.920  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487078.992   ± 2479.174  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     495889.281   ± 5681.581  ops/s
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

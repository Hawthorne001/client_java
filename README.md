# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-24T17:56:03Z
- **Commit:** [`95e8e8b`](https://github.com/Hawthorne001/client_java/commit/95e8e8b14cb4379211cea10b7d3708454eecd3b9)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.71K | ± 437.15 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.42K | ± 1.44K | ops/s | 1.2x slower |
| prometheusAdd | 51.43K | ± 164.36 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.80K | ± 1.94K | ops/s | 1.3x slower |
| simpleclientInc | 6.74K | ± 107.84 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.60K | ± 120.70 | ops/s | 10x slower |
| simpleclientAdd | 6.28K | ± 193.97 | ops/s | 11x slower |
| openTelemetryAdd | 1.40K | ± 192.64 | ops/s | 48x slower |
| openTelemetryInc | 1.38K | ± 254.35 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.27K | ± 5.21 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.86K | ± 535.96 | ops/s | **fastest** |
| simpleclient | 4.41K | ± 140.90 | ops/s | 1.1x slower |
| prometheusNative | 2.77K | ± 311.93 | ops/s | 1.8x slower |
| openTelemetryClassic | 672.96 | ± 22.52 | ops/s | 7.2x slower |
| openTelemetryExponential | 524.58 | ± 13.78 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.36K | ± 4.52K | ops/s | **fastest** |
| prometheusWriteToByteArray | 482.35K | ± 3.36K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 479.76K | ± 3.49K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 468.70K | ± 5.00K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49803.283   ± 1943.879  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1399.711    ± 192.637  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1378.683    ± 254.349  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1269.730      ± 5.212  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51433.132    ± 164.359  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66706.656    ± 437.152  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56416.128   ± 1443.775  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6276.683    ± 193.974  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6738.783    ± 107.845  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6596.959    ± 120.699  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        672.958     ± 22.520  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        524.580     ± 13.779  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4859.243    ± 535.955  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2772.541    ± 311.928  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4410.891    ± 140.904  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     468695.876   ± 4996.609  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     479764.229   ± 3487.994  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     482348.663   ± 3360.036  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489357.799   ± 4522.033  ops/s
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

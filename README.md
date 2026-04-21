# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-21T02:51:43Z
- **Commit:** [`4b69f40`](https://github.com/Hawthorne001/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.11K | ± 345.65 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.19K | ± 234.75 | ops/s | 1.2x slower |
| prometheusAdd | 50.52K | ± 1.44K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.82K | ± 1.82K | ops/s | 1.4x slower |
| simpleclientInc | 6.54K | ± 145.71 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.45K | ± 207.77 | ops/s | 10x slower |
| simpleclientAdd | 6.16K | ± 231.29 | ops/s | 11x slower |
| openTelemetryAdd | 1.35K | ± 83.52 | ops/s | 49x slower |
| openTelemetryInc | 1.24K | ± 28.74 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.18K | ± 74.39 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.43K | ± 1.68K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 38.48 | ops/s | 1.2x slower |
| prometheusNative | 2.66K | ± 71.82 | ops/s | 2.0x slower |
| openTelemetryClassic | 650.30 | ± 15.83 | ops/s | 8.4x slower |
| openTelemetryExponential | 546.62 | ± 18.32 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 480.93K | ± 2.86K | ops/s | **fastest** |
| openMetricsWriteToNull | 476.96K | ± 2.18K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 476.82K | ± 2.24K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 475.45K | ± 4.58K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48823.623   ± 1817.652  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1352.643     ± 83.522  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1238.824     ± 28.739  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1181.447     ± 74.392  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50519.155   ± 1440.020  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66114.651    ± 345.654  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57194.849    ± 234.753  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6157.349    ± 231.289  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6536.854    ± 145.708  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6447.204    ± 207.767  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        650.301     ± 15.828  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        546.624     ± 18.319  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5430.096   ± 1679.260  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2663.775     ± 71.818  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4430.594     ± 38.476  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     476819.235   ± 2244.544  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476958.795   ± 2182.160  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     475447.634   ± 4580.772  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     480927.975   ± 2862.440  ops/s
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

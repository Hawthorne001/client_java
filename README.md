# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-28T14:44:56Z
- **Commit:** [`6beb7fd`](https://github.com/Hawthorne001/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 31.18K | ± 264.85 | ops/s | **fastest** |
| prometheusInc | 30.71K | ± 1.52K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 28.90K | ± 615.94 | ops/s | 1.1x slower |
| prometheusAdd | 27.48K | ± 1.17K | ops/s | 1.1x slower |
| simpleclientInc | 6.82K | ± 63.37 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.73K | ± 225.11 | ops/s | 4.6x slower |
| simpleclientAdd | 6.45K | ± 216.83 | ops/s | 4.8x slower |
| openTelemetryIncNoLabels | 1.45K | ± 117.71 | ops/s | 21x slower |
| openTelemetryAdd | 1.43K | ± 103.32 | ops/s | 22x slower |
| openTelemetryInc | 1.36K | ± 70.76 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.43K | ± 86.77 | ops/s | **fastest** |
| prometheusClassic | 3.02K | ± 288.41 | ops/s | 1.5x slower |
| prometheusNative | 2.15K | ± 155.33 | ops/s | 2.1x slower |
| openTelemetryClassic | 520.13 | ± 10.95 | ops/s | 8.5x slower |
| openTelemetryExponential | 386.61 | ± 9.51 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 313.38K | ± 1.02K | ops/s | **fastest** |
| prometheusWriteToByteArray | 311.43K | ± 1.31K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 294.10K | ± 1.56K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 291.69K | ± 1.52K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28899.038    ± 615.940  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1426.628    ± 103.324  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1361.967     ± 70.755  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1452.085    ± 117.709  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27476.550   ± 1171.557  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30712.461   ± 1522.335  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31181.174    ± 264.847  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6447.114    ± 216.826  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6820.186     ± 63.372  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6725.896    ± 225.107  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        520.134     ± 10.948  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        386.614      ± 9.505  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3021.953    ± 288.412  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2149.581    ± 155.329  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4434.375     ± 86.773  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     291694.286   ± 1521.560  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     294101.138   ± 1556.425  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     311430.411   ± 1310.924  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     313380.841   ± 1023.627  ops/s
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

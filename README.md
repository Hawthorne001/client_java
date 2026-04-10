# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-10T19:48:01Z
- **Commit:** [`0fa1ad7`](https://github.com/Hawthorne001/client_java/commit/0fa1ad7dcb71f7f02e19ee9604c07d9c48802f04)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.28K | ± 1.98K | ops/s | **fastest** |
| prometheusNoLabelsInc | 49.74K | ± 1.92K | ops/s | 1.2x slower |
| prometheusAdd | 47.99K | ± 457.33 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.42K | ± 798.26 | ops/s | 1.3x slower |
| simpleclientInc | 6.20K | ± 116.20 | ops/s | 9.4x slower |
| simpleclientNoLabelsInc | 6.15K | ± 202.54 | ops/s | 9.5x slower |
| simpleclientAdd | 5.70K | ± 392.58 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.52K | ± 58.38 | ops/s | 38x slower |
| openTelemetryInc | 1.46K | ± 64.12 | ops/s | 40x slower |
| openTelemetryAdd | 1.40K | ± 65.89 | ops/s | 42x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.63K | ± 1.44K | ops/s | **fastest** |
| simpleclient | 4.38K | ± 25.99 | ops/s | 1.3x slower |
| prometheusNative | 3.15K | ± 75.40 | ops/s | 1.8x slower |
| openTelemetryClassic | 610.34 | ± 9.24 | ops/s | 9.2x slower |
| openTelemetryExponential | 518.05 | ± 11.89 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 553.15K | ± 6.10K | ops/s | **fastest** |
| openMetricsWriteToNull | 535.32K | ± 8.07K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 534.41K | ± 7.34K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 531.26K | ± 6.57K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44424.778    ± 798.258  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1397.666     ± 65.894  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1459.286     ± 64.119  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1522.007     ± 58.384  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47991.925    ± 457.328  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58282.547   ± 1975.515  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      49736.235   ± 1920.155  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5702.012    ± 392.584  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6197.744    ± 116.195  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6154.163    ± 202.539  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        610.339      ± 9.240  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        518.054     ± 11.888  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5633.984   ± 1444.047  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3153.143     ± 75.403  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4380.362     ± 25.985  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     531259.260   ± 6565.673  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     535321.115   ± 8067.800  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     534408.696   ± 7344.777  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     553145.477   ± 6097.760  ops/s
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

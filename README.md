# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-09T18:52:05Z
- **Commit:** [`0fa1ad7`](https://github.com/Hawthorne001/client_java/commit/0fa1ad7dcb71f7f02e19ee9604c07d9c48802f04)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.26K | ± 2.34K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.26K | ± 225.08 | ops/s | 1.1x slower |
| prometheusAdd | 51.00K | ± 540.01 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.78K | ± 666.03 | ops/s | 1.3x slower |
| simpleclientInc | 6.54K | ± 164.99 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.48K | ± 203.53 | ops/s | 9.9x slower |
| simpleclientAdd | 6.33K | ± 225.11 | ops/s | 10x slower |
| openTelemetryInc | 1.41K | ± 276.81 | ops/s | 46x slower |
| openTelemetryAdd | 1.39K | ± 44.01 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.31K | ± 114.12 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.38K | ± 1.16K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 24.83 | ops/s | 1.2x slower |
| prometheusNative | 3.08K | ± 261.23 | ops/s | 1.7x slower |
| openTelemetryClassic | 694.30 | ± 47.91 | ops/s | 7.7x slower |
| openTelemetryExponential | 563.67 | ± 5.50 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 486.48K | ± 3.03K | ops/s | **fastest** |
| openMetricsWriteToNull | 482.66K | ± 1.95K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 478.26K | ± 9.01K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 476.15K | ± 4.08K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49775.204    ± 666.031  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1385.725     ± 44.008  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1411.267    ± 276.806  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1314.972    ± 114.121  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51002.362    ± 540.005  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64261.284   ± 2342.346  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57257.092    ± 225.078  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6326.314    ± 225.112  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6541.955    ± 164.987  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6478.961    ± 203.525  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        694.298     ± 47.915  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        563.667      ± 5.503  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5380.054   ± 1164.415  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3083.646    ± 261.229  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4413.541     ± 24.830  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     476145.257   ± 4079.659  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482657.637   ± 1946.213  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     478258.306   ± 9009.226  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     486480.735   ± 3032.063  ops/s
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

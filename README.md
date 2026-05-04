# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-04T12:01:51Z
- **Commit:** [`188e434`](https://github.com/Hawthorne001/client_java/commit/188e434f25be73f75a463239b5cb4d54a8f72cca)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.55K | ± 534.94 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.12K | ± 194.43 | ops/s | 1.2x slower |
| prometheusAdd | 51.26K | ± 242.91 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.15K | ± 1.61K | ops/s | 1.4x slower |
| simpleclientInc | 6.42K | ± 151.23 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.40K | ± 163.18 | ops/s | 10x slower |
| simpleclientAdd | 6.27K | ± 262.22 | ops/s | 11x slower |
| openTelemetryAdd | 3.35K | ± 188.34 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.16K | ± 308.98 | ops/s | 21x slower |
| openTelemetryInc | 3.08K | ± 216.60 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.75K | ± 639.28 | ops/s | **fastest** |
| simpleclient | 4.47K | ± 70.05 | ops/s | 1.1x slower |
| prometheusNative | 3.11K | ± 98.28 | ops/s | 1.5x slower |
| openTelemetryClassic | 785.23 | ± 22.11 | ops/s | 6.1x slower |
| openTelemetryExponential | 615.66 | ± 66.22 | ops/s | 7.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.50K | ± 3.24K | ops/s | **fastest** |
| openMetricsWriteToByteArray | 481.47K | ± 3.03K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 480.44K | ± 3.75K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.17K | ± 3.66K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48148.402   ± 1614.094  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3352.215    ± 188.339  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3077.481    ± 216.600  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3161.416    ± 308.979  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51263.747    ± 242.914  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66553.499    ± 534.938  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57119.889    ± 194.428  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6270.982    ± 262.219  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6415.759    ± 151.234  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6404.847    ± 163.180  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        785.227     ± 22.113  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        615.657     ± 66.219  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4754.183    ± 639.283  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3108.493     ± 98.284  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4468.962     ± 70.052  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     481465.036   ± 3026.871  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476173.128   ± 3659.687  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     480443.231   ± 3750.291  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489501.010   ± 3243.105  ops/s
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

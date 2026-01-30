# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-01-30T05:07:50Z
- **Commit:** [`8c1cf17`](https://github.com/Hawthorne001/client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.11K | ± 489.67 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.03K | ± 325.16 | ops/s | 1.2x slower |
| prometheusAdd | 51.34K | ± 195.10 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.27K | ± 151.56 | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.63K | ± 122.09 | ops/s | 10.0x slower |
| simpleclientInc | 6.56K | ± 120.24 | ops/s | 10x slower |
| simpleclientAdd | 6.20K | ± 311.01 | ops/s | 11x slower |
| openTelemetryAdd | 1.52K | ± 216.88 | ops/s | 43x slower |
| openTelemetryInc | 1.36K | ± 208.25 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.31K | ± 202.73 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.31K | ± 331.39 | ops/s | **fastest** |
| simpleclient | 4.56K | ± 29.47 | ops/s | 1.2x slower |
| prometheusNative | 3.09K | ± 55.53 | ops/s | 1.7x slower |
| openTelemetryClassic | 672.40 | ± 37.50 | ops/s | 7.9x slower |
| openTelemetryExponential | 538.43 | ± 35.89 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 529.26K | ± 3.30K | ops/s | **fastest** |
| prometheusWriteToByteArray | 525.53K | ± 3.57K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 508.43K | ± 7.05K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 508.10K | ± 2.67K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47269.788    ± 151.561  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1524.264    ± 216.879  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1357.370    ± 208.251  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1309.520    ± 202.726  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51341.932    ± 195.100  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66106.124    ± 489.671  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57026.403    ± 325.165  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6199.729    ± 311.007  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6562.677    ± 120.240  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6631.243    ± 122.092  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        672.403     ± 37.498  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        538.431     ± 35.886  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5309.679    ± 331.393  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3086.320     ± 55.529  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4560.934     ± 29.472  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     508425.807   ± 7048.491  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     508095.306   ± 2671.800  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     525527.217   ± 3566.801  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     529264.297   ± 3297.900  ops/s
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

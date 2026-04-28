# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-28T07:51:58Z
- **Commit:** [`dec8e5b`](https://github.com/Hawthorne001/client_java/commit/dec8e5b15a1c48c54be6b81517f2cb334bc0ee60)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.77K | ± 980.29 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.00K | ± 658.53 | ops/s | 1.2x slower |
| prometheusAdd | 48.56K | ± 53.31 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.61K | ± 1.56K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.24K | ± 29.86 | ops/s | 9.4x slower |
| simpleclientInc | 6.12K | ± 135.16 | ops/s | 9.6x slower |
| simpleclientAdd | 6.02K | ± 170.26 | ops/s | 9.8x slower |
| openTelemetryIncNoLabels | 5.31K | ± 843.85 | ops/s | 11x slower |
| openTelemetryInc | 5.02K | ± 957.85 | ops/s | 12x slower |
| openTelemetryAdd | 3.73K | ± 1.15K | ops/s | 16x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.70K | ± 1.28K | ops/s | **fastest** |
| simpleclient | 4.21K | ± 41.36 | ops/s | 1.4x slower |
| prometheusNative | 3.16K | ± 55.71 | ops/s | 1.8x slower |
| openTelemetryClassic | 708.36 | ± 7.10 | ops/s | 8.1x slower |
| openTelemetryExponential | 574.27 | ± 11.31 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 556.46K | ± 2.95K | ops/s | **fastest** |
| prometheusWriteToByteArray | 546.04K | ± 5.85K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 533.85K | ± 8.07K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 529.42K | ± 2.43K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43613.421   ± 1561.418  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3727.344   ± 1151.492  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5019.963    ± 957.852  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       5305.037    ± 843.848  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48563.436     ± 53.307  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58772.568    ± 980.291  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51003.715    ± 658.529  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6022.540    ± 170.257  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6116.815    ± 135.157  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6239.926     ± 29.858  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        708.358      ± 7.105  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        574.268     ± 11.309  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5702.445   ± 1280.969  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3161.229     ± 55.714  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4206.635     ± 41.356  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     529423.564   ± 2433.342  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     533852.420   ± 8074.255  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     546035.762   ± 5847.990  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     556458.473   ± 2945.874  ops/s
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

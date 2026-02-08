# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-08T10:47:31Z
- **Commit:** [`5cfa5c0`](https://github.com/Hawthorne001/client_java/commit/5cfa5c08cf169dc5854b16d5fb457e37dc7885a3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.19K | ± 1.15K | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.76K | ± 962.63 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 30.11K | ± 1.44K | ops/s | 1.0x slower |
| prometheusAdd | 28.57K | ± 128.50 | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 7.03K | ± 176.25 | ops/s | 4.4x slower |
| simpleclientInc | 6.98K | ± 29.03 | ops/s | 4.5x slower |
| simpleclientAdd | 6.61K | ± 63.74 | ops/s | 4.7x slower |
| openTelemetryIncNoLabels | 1.37K | ± 67.22 | ops/s | 23x slower |
| openTelemetryAdd | 1.35K | ± 71.27 | ops/s | 23x slower |
| openTelemetryInc | 1.33K | ± 55.12 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.50K | ± 89.83 | ops/s | **fastest** |
| prometheusClassic | 3.92K | ± 1.79K | ops/s | 1.1x slower |
| prometheusNative | 1.98K | ± 96.86 | ops/s | 2.3x slower |
| openTelemetryClassic | 525.32 | ± 41.75 | ops/s | 8.6x slower |
| openTelemetryExponential | 397.92 | ± 11.58 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 314.37K | ± 802.42 | ops/s | **fastest** |
| prometheusWriteToByteArray | 308.67K | ± 1.41K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 294.22K | ± 945.97 | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 292.08K | ± 1.07K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30105.303   ± 1444.268  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1351.086     ± 71.272  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1329.492     ± 55.123  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1373.053     ± 67.223  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28566.771    ± 128.498  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31187.156   ± 1149.631  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30755.434    ± 962.633  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6610.750     ± 63.735  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6975.092     ± 29.035  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7027.203    ± 176.249  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        525.318     ± 41.749  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        397.922     ± 11.581  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3919.541   ± 1789.625  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1975.767     ± 96.860  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4503.130     ± 89.829  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     292083.320   ± 1067.875  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     294219.188    ± 945.970  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     308667.624   ± 1405.048  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     314367.930    ± 802.422  ops/s
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

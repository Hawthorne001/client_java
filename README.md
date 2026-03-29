# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-29T15:19:31Z
- **Commit:** [`6beb7fd`](https://github.com/Hawthorne001/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.33K | ± 312.96 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.67K | ± 590.19 | ops/s | 1.2x slower |
| prometheusAdd | 51.43K | ± 403.40 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.19K | ± 1.60K | ops/s | 1.4x slower |
| simpleclientInc | 6.64K | ± 115.90 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.44K | ± 144.15 | ops/s | 10x slower |
| simpleclientAdd | 6.25K | ± 209.22 | ops/s | 11x slower |
| openTelemetryAdd | 1.45K | ± 196.36 | ops/s | 46x slower |
| openTelemetryInc | 1.30K | ± 143.67 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.16K | ± 84.15 | ops/s | 57x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.09K | ± 1.44K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 58.78 | ops/s | 1.4x slower |
| prometheusNative | 3.00K | ± 318.97 | ops/s | 2.0x slower |
| openTelemetryClassic | 674.55 | ± 8.18 | ops/s | 9.0x slower |
| openTelemetryExponential | 572.82 | ± 18.48 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.64K | ± 2.02K | ops/s | **fastest** |
| prometheusWriteToByteArray | 483.60K | ± 2.68K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 482.83K | ± 2.29K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 472.37K | ± 3.24K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48185.699   ± 1596.742  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1451.458    ± 196.355  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1303.343    ± 143.669  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1158.901     ± 84.154  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51426.957    ± 403.403  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66334.036    ± 312.960  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56672.491    ± 590.193  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6247.942    ± 209.223  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6639.084    ± 115.900  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6440.585    ± 144.152  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        674.548      ± 8.180  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        572.817     ± 18.480  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6094.971   ± 1435.855  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3002.581    ± 318.974  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4438.121     ± 58.778  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     472371.155   ± 3238.391  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482828.680   ± 2291.974  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     483598.228   ± 2682.296  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488644.415   ± 2019.328  ops/s
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

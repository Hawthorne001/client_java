# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-02T15:57:31Z
- **Commit:** [`deb782f`](https://github.com/Hawthorne001/client_java/commit/deb782f9fce60ffb1308a98b661c0a1ccb79a82b)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.39K | ± 1.26K | ops/s | **fastest** |
| prometheusNoLabelsInc | 54.20K | ± 2.61K | ops/s | 1.2x slower |
| prometheusAdd | 51.52K | ± 196.34 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.18K | ± 929.74 | ops/s | 1.3x slower |
| simpleclientInc | 6.56K | ± 233.99 | ops/s | 9.8x slower |
| simpleclientAdd | 6.24K | ± 201.00 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.23K | ± 7.39 | ops/s | 10x slower |
| openTelemetryAdd | 1.34K | ± 54.94 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.31K | ± 130.50 | ops/s | 49x slower |
| openTelemetryInc | 1.24K | ± 10.91 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.48K | ± 1.42K | ops/s | **fastest** |
| simpleclient | 4.45K | ± 56.24 | ops/s | 1.2x slower |
| prometheusNative | 2.69K | ± 129.65 | ops/s | 2.0x slower |
| openTelemetryClassic | 678.55 | ± 26.34 | ops/s | 8.1x slower |
| openTelemetryExponential | 545.55 | ± 8.82 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 484.53K | ± 4.24K | ops/s | **fastest** |
| prometheusWriteToByteArray | 481.74K | ± 3.83K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 475.86K | ± 2.69K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 463.16K | ± 5.33K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48175.910    ± 929.738  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1335.521     ± 54.942  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1235.476     ± 10.906  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1305.717    ± 130.504  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51522.503    ± 196.345  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64394.199   ± 1260.501  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      54197.300   ± 2608.743  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6238.854    ± 201.003  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6560.953    ± 233.993  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6231.518      ± 7.389  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        678.545     ± 26.337  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        545.550      ± 8.822  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5476.146   ± 1421.330  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2688.288    ± 129.648  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4446.528     ± 56.239  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     463157.909   ± 5332.264  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     475856.448   ± 2694.969  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481737.896   ± 3831.295  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     484525.007   ± 4235.120  ops/s
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

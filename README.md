# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-13T21:15:06Z
- **Commit:** [`4b69f40`](https://github.com/Hawthorne001/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.30K | ± 893.99 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.17K | ± 471.17 | ops/s | 1.1x slower |
| prometheusAdd | 47.86K | ± 341.93 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 41.05K | ± 4.83K | ops/s | 1.4x slower |
| simpleclientInc | 6.15K | ± 185.33 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 5.98K | ± 216.34 | ops/s | 9.9x slower |
| simpleclientAdd | 5.68K | ± 412.68 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.40K | ± 130.04 | ops/s | 42x slower |
| openTelemetryInc | 1.38K | ± 34.59 | ops/s | 43x slower |
| openTelemetryAdd | 1.37K | ± 33.29 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.06K | ± 323.82 | ops/s | **fastest** |
| simpleclient | 4.32K | ± 64.40 | ops/s | 1.2x slower |
| prometheusNative | 3.10K | ± 153.95 | ops/s | 1.6x slower |
| openTelemetryClassic | 638.71 | ± 14.42 | ops/s | 7.9x slower |
| openTelemetryExponential | 540.02 | ± 25.59 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 536.16K | ± 4.46K | ops/s | **fastest** |
| prometheusWriteToByteArray | 528.25K | ± 4.96K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 521.44K | ± 7.81K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 514.40K | ± 3.32K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      41046.213   ± 4825.266  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1365.670     ± 33.288  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1384.660     ± 34.589  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1404.782    ± 130.038  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47856.703    ± 341.932  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59300.601    ± 893.995  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52166.548    ± 471.172  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5682.161    ± 412.682  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6145.149    ± 185.329  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5978.139    ± 216.339  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        638.705     ± 14.423  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        540.023     ± 25.592  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5062.137    ± 323.816  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3096.183    ± 153.955  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4323.914     ± 64.404  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     514396.042   ± 3319.541  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     521441.368   ± 7812.074  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     528250.512   ± 4955.936  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     536158.446   ± 4458.598  ops/s
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

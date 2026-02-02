# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-02T06:43:35Z
- **Commit:** [`421033a`](https://github.com/Hawthorne001/client_java/commit/421033a2f72ef0c52d77fae6eb1b346c81b1fdb3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.60K | ± 1.37K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.67K | ± 1.16K | ops/s | 1.2x slower |
| prometheusAdd | 51.55K | ± 276.64 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.62K | ± 610.02 | ops/s | 1.3x slower |
| simpleclientInc | 6.67K | ± 213.73 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.60K | ± 190.80 | ops/s | 9.9x slower |
| simpleclientAdd | 6.46K | ± 171.19 | ops/s | 10x slower |
| openTelemetryAdd | 1.32K | ± 49.16 | ops/s | 50x slower |
| openTelemetryInc | 1.25K | ± 64.36 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.24K | ± 38.82 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.13K | ± 106.60 | ops/s | **fastest** |
| simpleclient | 4.55K | ± 33.18 | ops/s | 1.1x slower |
| prometheusNative | 3.08K | ± 54.67 | ops/s | 1.7x slower |
| openTelemetryClassic | 680.44 | ± 21.57 | ops/s | 7.5x slower |
| openTelemetryExponential | 554.39 | ± 29.08 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 536.89K | ± 4.99K | ops/s | **fastest** |
| prometheusWriteToByteArray | 530.82K | ± 3.68K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 510.47K | ± 3.15K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 508.29K | ± 7.35K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49620.258    ± 610.024  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1323.771     ± 49.164  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1252.555     ± 64.356  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1238.263     ± 38.815  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51554.428    ± 276.643  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65599.972   ± 1373.253  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56665.131   ± 1159.530  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6458.280    ± 171.192  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6665.618    ± 213.728  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6595.234    ± 190.796  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        680.439     ± 21.570  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        554.394     ± 29.077  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5128.690    ± 106.596  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3079.594     ± 54.666  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4545.556     ± 33.183  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     510467.851   ± 3151.293  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     508287.667   ± 7347.868  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     530820.574   ± 3679.682  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     536894.356   ± 4985.597  ops/s
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
